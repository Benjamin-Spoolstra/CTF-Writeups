# Forge Coupon

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Hard
---

### Overview

This challenge corresponds to the [A04:2025 Cryptographic Failures](https://owasp.org/Top10/2025/A04_2025-Cryptographic_Failures/) category on the OWASP Top 10. It demonstrates a fundamental cryptographic implementation flaw where predictable or hardcoded encoding algorithms are used with weak parameters to generate coupon codes. These coupons can be forged by reverse engineering the encoding algorithm and forging a valid coupon code with up to any discount percentage. 

---

### Solution

To start this challenge an attacker must obtain a valid coupon code and analyze its structure.

<img width="1717" height="877" alt="Screenshot 2026-08-25 184140" src="https://github.com/user-attachments/assets/56baa49b-8181-48bb-bd9e-fbc59c28190c" />

After obtaining a valid coupon code from the shop's public BlueSky page the attacker can begin analyzing the encoding for known signatures.

<img width="1717" height="867" alt="Screenshot 2026-08-25 184210" src="https://github.com/user-attachments/assets/e552bc37-7c32-4a63-aab2-b2af9de1b60c" />

The coupon can be identified to be encoded with the common z85 encoding algorithm, which is confirmed in the packages backup file to be used by the application. 

<img width="1717" height="876" alt="Screenshot 2026-08-25 184154" src="https://github.com/user-attachments/assets/ee83e63f-62b2-4984-9ae5-f12bfd985927" />

After inserting the coupon into a decoding application the full structure can be seen.

<img width="1720" height="872" alt="Screenshot 2026-08-25 184223" src="https://github.com/user-attachments/assets/de3da429-85a5-424e-ae3c-f109093eac5e" />

Modifying the amount of the coupon at the end of the structure allows the attacker to arbitrarily assign themselves a coupon of any chosen amount. 

Encoding the new coupon completes the forging process.

<img width="1718" height="872" alt="Screenshot 2026-08-25 184239" src="https://github.com/user-attachments/assets/496eee74-3335-4eb0-bf97-bc071405c011" />

All that's left is for the attacker to purchase items from the shop on any account and the discount will be successfully applied.

<img width="1713" height="876" alt="Screenshot 2026-08-25 184315" src="https://github.com/user-attachments/assets/e577280e-1526-4d08-ade1-ed1cbd5dd7fb" />
<img width="1712" height="872" alt="Screenshot 2026-08-25 184333" src="https://github.com/user-attachments/assets/5d3d036c-074a-425e-82b6-ffad338e7512" />

This challenge exposes how improper cryptographic implementations can be easily defeated by basic reverse engineering and signature analysis. It is best to use robust encryption algorithms (like AES-256 or AES-512) when creating bits of information that perform meaningful actions on the application, such as coupon codes or gift cards.

## Tools

`Dencode` - An online data encoding and decoding tool
