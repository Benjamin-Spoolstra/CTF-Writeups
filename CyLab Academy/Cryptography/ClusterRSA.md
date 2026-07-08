# ClusterRSA

---

### Challenge Details

> **Platform:** CyLab Academy  
> **Category:** `Cryptography`  
> **Difficulty:** Medium  
> **Points:** 400

---

### Overview

This challenge presents an RSA-encrypted message and hints that the modulus was built from more than the usual two primes. The goal is to factor the modulus, rebuild the private key parameters, and decrypt the ciphertext to recover the flag.

---

### Solution

#### Downloading RSA-encrypted Message

The challenge starts with a downloadable message file containing the RSA values needed to solve the problem. I see that the challenge description discusses a "crowded" encryption and that someone got "greedy" with the encryption. This likely means that the task is centered on decrypting an multi-prime RSA-encrypted message.

<img width="1919" height="862" alt="step1" src="https://github.com/user-attachments/assets/e11e88e6-ca6c-461d-948b-6db04c31bcec" />

#### Viewing the RSA Parameters

After opening the message file, the important values are the modulus \(n\), public exponent \(e\), and ciphertext \(ct\). These are the core components of an RSA encryption algorithm and can be used to recover the private key assuming the modulus can be factored.

<img width="1426" height="726" alt="step2" src="https://github.com/user-attachments/assets/abf86502-f612-469e-b0fc-61b462ff344d" />

The values were:

```text
n = 8749002899132047699790752490331099938058737706735201354674975134719667510377522805717156720453193651
e = 65537
ct = 3891662771105467488888140657249806558204248580982414398721303729411975827561400201060615350757604497
```

#### Factoring the Modulus

The hint strongly suggests a clustered or multi-prime RSA setup, so I submitted to FactorDB to recover its prime factors. The result below shows the factorization is four prime factors rather than the usual two.

<img width="1919" height="867" alt="step3" src="https://github.com/user-attachments/assets/edda4414-061a-4f47-912b-07a7c9e9420f" />

The factors were:

```text
9671406556917033397931773
9671406556917033398314601
9671406556917033398439721
9671406556917033398454847
```

#### Reconstructing the Private Key and Decrypting using Python

With the prime factors known, the private exponent can be recovered by computing Euler's totient from all factors, then taking the modular inverse of \(e\) modulo \(phi(n)\). Once \(d\) is known, the ciphertext can be decrypted back into the original message.

The Python script used was:

```python
n = 8749002899132047699790752490331099938058737706735201354674975134719667510377522805717156720453193651
e = 65537
ct = 3891662771105467488888140657249806558204248580982414398721303729411975827561400201060615350757604497

factors = 

phi = 1
for p in factors:
    phi *= (p - 1)

d = pow(e, -1, phi)  # Python 3.8+ built-in modular inverse
m = pow(ct, d, n)

# Replaces long_to_bytes
flag = m.to_bytes((m.bit_length() + 7) // 8, 'big').decode()
print(flag)
```

The screenshot below shows the successful script output after decryption.

<img width="1919" height="867" alt="step4" src="https://github.com/user-attachments/assets/298f08b4-4d53-41e5-b0de-2ce710a5d103" />

### Tools Used

- `Python`: For modular inverse and RSA decryption.
- `FactorDB`: For factoring the multi-prime RSA modulus.

### Flag

```text
picoCTF{mul71_rsa_c5d0a11c}
```
