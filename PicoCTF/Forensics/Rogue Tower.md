# Rogue Tower

---

### Challenge Details

> **Platform:** PicoCTF  
> **Category:** `Forensics`  
> **Difficulty:** Medium  
> **Points:** 300

---

### Overview

This challenge involved analyzing a packet capture from a suspicious cellular tower to identify the compromised device and recover an exfiltrated flag. The key idea was to inspect HTTP traffic, identify how the payload was split across multiple requests, and then reconstruct it using the IMSI-derived XOR key.

---

### Solution

#### Step 1: Download the PCAP

I started by downloading the provided network capture and opening it in Wireshark for analysis. The capture contained DNS lookups, HTTP registration traffic, and several `POST /upload` requests that stood out as likely exfiltration traffic.

<img width="1919" height="866" alt="Step1" src="https://github.com/user-attachments/assets/b5f51d1b-496b-400a-8328-9419f27ffda8" />

#### Step 2: Locate the IMSI

The first important clue was in the HTTP `GET /api/register` request. In the packet details, the `User-Agent` header included the device IMSI, which was needed later as the XOR key source.

<img width="1919" height="1019" alt="Step2" src="https://github.com/user-attachments/assets/18e830b0-2c58-4f32-82b1-a0d648c96268" />

The IMSI shown in the capture was:

```text
310410176578566
```

From this, I extracted the XOR key used in CyberChef:

```text
76578566
```

#### Step 3: Reconstruct the Split Payload

The next part was to inspect the repeated HTTP `POST /upload` requests. Each request carried only a small chunk of data, and the hint confirmed that the exfiltrated data was split across multiple HTTP POSTs.

<img width="1919" height="1015" alt="Step3-1" src="https://github.com/user-attachments/assets/b5058ea1-2e4f-4517-bf97-14bcdc4c94e3" />

Looking at the packet data across those requests revealed the full Base64 string assembled from the uploads:

```text
R19WWHthcE1FBlJCC2pVBVtaakMIQgVEaAVXAgANV1cAS==
```

The screenshots show the payload being delivered in multiple chunks rather than as one continuous message, which is why it had to be reconstructed before decoding.

<img width="1919" height="1018" alt="step3-2" src="https://github.com/user-attachments/assets/70fea485-41e7-466a-a3f1-fdfc1bf53d1d" />
<img width="1919" height="1019" alt="step3-3" src="https://github.com/user-attachments/assets/115867b8-5c64-44d1-9f3a-dcf153a423cb" />
<img width="1919" height="1018" alt="step3-4" src="https://github.com/user-attachments/assets/e3fe92ef-a4d3-4536-aafe-e1cfaec3a0af" />
<img width="1919" height="1021" alt="step3-5" src="https://github.com/user-attachments/assets/0b90112e-31d2-4eaa-907f-2f57f283016b" />
<img width="1919" height="1021" alt="step3-6" src="https://github.com/user-attachments/assets/23ef099a-4290-416d-80e4-c480c91a3387" />

#### Step 4: Decode in CyberChef

After combining the Base64 string, I pasted it into CyberChef and applied the following operations:

1. **From Base64**
2. **XOR** with key `76578566`
3. **UTF-8** output

This decoded the hidden message and revealed the flag.

<img width="1919" height="874" alt="step4" src="https://github.com/user-attachments/assets/7165e0bb-baa8-409d-8d94-1dd584e867e2" />

### Tools Used

- **Wireshark**: Used to inspect the PCAP, find the IMSI in the HTTP headers, and recover the split upload data.
- **CyberChef**: Used to Base64-decode the collected payload and XOR-decrypt it with the IMSI-derived key.

### Flag

```text
picoCTF{r0gu3_c3ll_t0w3r_3b588aa7}
```
