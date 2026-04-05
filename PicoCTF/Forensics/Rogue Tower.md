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

[image:1]

#### Step 2: Locate the IMSI

The first important clue was in the HTTP `GET /api/register` request. In the packet details, the `User-Agent` header included the device IMSI, which was needed later as the XOR key source.

[image:2]

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

[image:3]

Looking at the packet data across those requests revealed the full Base64 string assembled from the uploads:

```text
R19WWHthcE1FBlJCC2pVBVtaakMIQgVEaAVXAgANV1cAS==
```

The screenshots show the payload being delivered in multiple chunks rather than as one continuous message, which is why it had to be reconstructed before decoding.

[image:4]

[image:5]

[image:6]

[image:7]

[image:8]

[image:9]

#### Step 4: Decode in CyberChef

After combining the Base64 string, I pasted it into CyberChef and applied the following operations:

1. **From Base64**
2. **XOR** with key `76578566`
3. **UTF-8** output

This decoded the hidden message and revealed the flag.

[image:10]

### Tools Used

- **Wireshark** — Used to inspect the PCAP, find the IMSI in the HTTP headers, and recover the split upload data.
- **CyberChef** — Used to Base64-decode the collected payload and XOR-decrypt it with the IMSI-derived key.

### Flag

```text
picoCTF{r0gu3_c3ll_t0w3r_3b588aa7}
```
