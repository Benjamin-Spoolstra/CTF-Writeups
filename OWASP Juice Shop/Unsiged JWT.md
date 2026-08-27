# Unsigned JWT

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Hard
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A08:2025 Software or Data Integrity Failures](https://owasp.org/Top10/2025/A08_2025-Software_or_Data_Integrity_Failures/) category on the OWASP Top 10. An authenticated attacker can forge a valid JWT authentication token for any user on the application. This forgery is possible due to the lack of server-side signature validation and enforcements. An attacker can remove the `HS256` signature completely and the application will still accept it. Forged JWT attacks can lead to user impersonation and privilege escalation if applicable to highly-privileged accounts.

---

### Solution

To start this challenge an attacker must obtain a valid JWT. This can be done by logging into the shop with any user account. 

<img width="1716" height="872" alt="Screenshot 2026-08-27 151813" src="https://github.com/user-attachments/assets/f7782719-eaca-4282-891f-c10472b09b8a" />

Once logged in the attacker can capture the login request and copy a valid JWT.

<img width="1715" height="876" alt="Screenshot 2026-08-27 152026" src="https://github.com/user-attachments/assets/8f79f4bf-0e0c-41e4-8321-072768da0d7e" />

After obtaining a valid JWT they can decode it using a JWT decoder like `JWT.io`. This service reverses the Base64URL encoding algorithm to extract the raw JSON headers and body, which can be modified.

<img width="1717" height="868" alt="Screenshot 2026-08-27 152057" src="https://github.com/user-attachments/assets/c287dd84-813b-492b-ac9c-b95b74387f0f" />

The `HS256` algorithm can be stripped from the token and changed to `none`, and the user email associated with the token can be modified to match the targeted, non-existent user account.

<img width="1717" height="870" alt="Screenshot 2026-08-27 152156" src="https://github.com/user-attachments/assets/6de132df-d33f-4cb9-9589-4a0c1ee6e74f" />

The new token must be assembled from encoding the header and body of the forged token separately using a Base64 encoding service like `Phcode.io`. 

<img width="1717" height="878" alt="Screenshot 2026-08-27 152240" src="https://github.com/user-attachments/assets/c562f764-01f3-4339-9b9d-ac81549b5d78" />

### Header Portion
<img width="1718" height="876" alt="Screenshot 2026-08-27 152305" src="https://github.com/user-attachments/assets/beca50f4-2970-4aa2-b328-0a7490bff8c6" />
### Body Portion
<img width="1717" height="871" alt="Screenshot 2026-08-27 152323" src="https://github.com/user-attachments/assets/6b6cc45b-d17e-42d7-b842-f018c472f293" />
<img width="1715" height="877" alt="Screenshot 2026-08-27 152349" src="https://github.com/user-attachments/assets/ef742ca0-5f48-4ad3-8023-8fc5dce0db17" />
<img width="1715" height="872" alt="Screenshot 2026-08-27 152431" src="https://github.com/user-attachments/assets/7d08f274-edec-4fd7-be58-0fa2e7ae45af" />

After assembling the new token it can be injected back into the captured login request and forwarded to the server.

<img width="1717" height="871" alt="Screenshot 2026-08-27 152504" src="https://github.com/user-attachments/assets/a83115a1-98ce-4d9e-9d46-32c9cfac17f2" />

The server won't validate the new token, and will update the attacker's session to the same one as the impersonated user. 

<img width="1718" height="870" alt="Screenshot 2026-08-27 152523" src="https://github.com/user-attachments/assets/c0bc148d-a1bf-448f-924f-a5a93f08d121" />

Implementing server-side JWT signature validations is essential to ensure user impersonation and data theft cannot be accomplished via authentication bypasses. 

## Tools Used
- `JWT.io` - a popular web development tool for decoding, verifying, and generating new JSON Web Tokens (JWTs)
- `Phcode.io` - a free, online Base64 encoding and decoding tool


