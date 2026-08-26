# Vulnerable Library

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Medium
---

### Overview

This challenge demonstrates vulnerabilities that can arise from using outdated libraries and dependencies in application codebases. It directly corresponds to the [A03:2025 Software Supply Chain Failures](https://owasp.org/Top10/2025/A03_2025-Software_Supply_Chain_Failures/) category on the OWASP Top 10. By utilizing a poisoned null byte attack attackers can retrieve a copy of the packages backup, and analyze it using automated software composition analysis (SCA) to identify well-known critical vulnerabilities within outdated dependencies. The goal of this challenge is to analyze the application's dependencies and submit a report informing the shop owners of their use of vulnerable, outdated dependences. 

---

### Solution

To start this challenge an attacker must gain access to the backend packages backup file.

<img width="1716" height="876" alt="Screenshot 2026-08-25 175841" src="https://github.com/user-attachments/assets/f8c7fc17-0b55-46aa-ba59-17dcc14f06f5" />

This can be done by navigating to the hidden `/ftp` directory that displays a key `packages.json.bak` file.

<img width="1717" height="877" alt="Screenshot 2026-08-25 175859" src="https://github.com/user-attachments/assets/f157e6e5-240d-40ad-bb05-b05371853aa8" />

Accessing it directory leads to an improper file type server error. This error can be bypassed by performing a poisoned null byte injection attack by double URL encoding the null byte (%00). 

After injecting the null byte the file is automatically downloaded to the attacker's machine.

<img width="1718" height="872" alt="Screenshot 2026-08-25 175919" src="https://github.com/user-attachments/assets/2aba540c-13c3-4bbc-9f77-d401971baec3" />

Upon the file's analysis multiple libraries are visible. With some brief research several are identified to have well-known CVEs with high CVSS scores.

<img width="1718" height="871" alt="Screenshot 2026-08-25 175950" src="https://github.com/user-attachments/assets/3d456deb-db38-4960-a7d0-a4e0775c16c4" />

These vulnerable libraries are reported to the shop owners and this solves the challenge.

<img width="1712" height="871" alt="Screenshot 2026-08-25 180207" src="https://github.com/user-attachments/assets/9d266a86-bf0f-421b-9539-9851592258ae" />

This challenge highlights the importance of conducting automated SCA during application development to catch vulnerabilities in outdated libraries and patching them before shipping to production. These libraries serve as a backdoor entrance for attacks to take elevated or full levels of control over the application, which can threaten the confidentiality and integrity of consumer information at a wide scale.






