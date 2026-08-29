# Access Log

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Easy
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A09:2025 Security Logging & Alerting Failures](https://owasp.org/Top10/2025/A09_2025-Security_Logging_and_Alerting_Failures/) category on the OWASP Top 10. An unauthenticated attacker can access the application's internal server logs over the public internet. They are stored in well-known server paths that can be discovered quickly using fuzzing tools like ffuf or feroxbuster using common wordlists in the `Seclists` repository. Attackers could potentially utilize the information gathered from these logs to enumerate users, escalate privileges, exploit server permissions, or conduct targeted Denial of Service (DoS) attacks.

---

### Solution

To start this challenge an attacker needs to map out hidden paths and assets in the Juice Shop application to expose the targeted log directory.

<img width="1718" height="878" alt="Screenshot 2026-08-28 182614" src="https://github.com/user-attachments/assets/c31277f1-725a-4f40-8fde-618f4115465f" />

After a bit of tuning an attacker can recognize that any response that isn't 474 characters long is a valid, unique file stored on the server.

<img width="1713" height="876" alt="Screenshot 2026-08-28 182638" src="https://github.com/user-attachments/assets/e9a63dbb-e2a6-4391-bc07-334f058b0349" />

Using `ffuf` and the `common.txt` wordlist from the `Seclists` repository an attacker can uncover a hidden `/support/logs` database that stores the application's access logs. 

<img width="1715" height="876" alt="Screenshot 2026-08-28 182711" src="https://github.com/user-attachments/assets/38372767-864a-43a4-963d-ce160bf64a04" />

By downloading the most recent one an attacker can gather user IP addresses, user agent strings, and requested resources to potentially uncover more sensitive data.

<img width="1717" height="877" alt="Screenshot 2026-08-28 182818" src="https://github.com/user-attachments/assets/7edbac37-dcbc-4313-a6b7-9464a61cccb8" />

This challenge demonstrates the necessity of proper access controls across all endpoints on an application, as security through obscurity isn't security at all with modern web fuzzers. 

## Tools Used
- `ffuf` - a popular web application fuzzer written in Go that discovers hidden web content 

