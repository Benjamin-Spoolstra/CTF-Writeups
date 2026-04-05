# ClusterRSA

---

### Challenge Details

> **Platform:** PicoCTF  
> **Category:** `Cryptography`  
> **Difficulty:** Medium  
> **Points:** 400

---

### Overview

This challenge presents an RSA-encrypted message and hints that the modulus was built from more than the usual two primes. The goal is to factor the modulus, rebuild the private key parameters, and decrypt the ciphertext to recover the flag.

### Solution

#### Downloading RSA-encrypted Message

The challenge starts with a downloadable message file containing the RSA values needed to solve the problem. The screenshot below shows the challenge prompt and confirms that the task is centered on decrypting an RSA-encrypted message.

[image:4]

#### Viewing the RSA Parameters

After opening the message file, the important values are the modulus \(n\), public exponent \(e\), and ciphertext \(ct\). The screenshot below shows those values extracted from the file and used directly in the decryption script.

[image:2]

The values were:

```text
n = 8749002899132047699790752490331099938058737706735201354674975134719667510377522805717156720453193651
e = 65537
ct = 3891662771105467488888140657249806558204248580982414398721303729411975827561400201060615350757604497
```

#### Factoring the Modulus

The hint strongly suggests a clustered or multi-prime RSA setup, so the modulus was submitted to FactorDB to recover its prime factors. The screenshot below shows the factorization result listing four prime factors rather than the usual two.

[image:3]

The factors were:

```text
9671406556917033397931773
9671406556917033398314601
9671406556917033398439721
9671406556917033398454847
```

#### Reconstructing the Private Key

With the prime factors known, the private exponent can be recovered by computing Euler's totient from all factors, then taking the modular inverse of \(e\) modulo \(\phi(n)\). Once \(d\) is known, the ciphertext can be decrypted back into the original message.

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

[image:5]

### Tools Used

- `Python` for modular inverse and RSA decryption.
- `FactorDB` for factoring the multi-prime RSA modulus.

### Flag

```text
picoCTF{mul71_rsa_c5d0a11c}
```
picoCTF{mul71_rsa_c5d0a11c}
```
