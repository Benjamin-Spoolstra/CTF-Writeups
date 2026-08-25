# Confidential Document

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Easy
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A02:2025 - Security Misconfiguration](https://owasp.org/Top10/2025/A02_2025-Security_Misconfiguration/) category in the OWASP Top 10. It demonstrates a common web server misconfiguration called directory listing that reveals internal server resources to unauthenticated users.
Attackers can potentially utilize the information exfiltrated from directory listing misconfigurations to inflict more serious damage on an application or hosting organization.

---

### Solution

To start this challenge it's clear to an attacker that the `/ftp` directory can be found by going to it directly.

However, it's important to understand the vulnerability underlying this challenge.

If web servers have directory listing enabled it exposes potentially sensitive, internal files to unauthenticated, external users on the public internet. 

Even if the `/ftp` endpoint wasn't specified in the challenge description an attacker could fuzz the application for common directories and identify the same exposed ftp service.  

<img width="1712" height="877" alt="Screenshot 2026-08-24 161428" src="https://github.com/user-attachments/assets/9633899e-0802-4c4d-a94f-64186d17a987" />

In the case of this application the directory can also be found in the `robots.txt` file, which is a well-known location to check during application reconnaissance.

Going to the ftp directory reveals a list of sensitive internal logs and proprietary information, including the cited acquisitions file.

<img width="1715" height="873" alt="Screenshot 2026-08-24 161458" src="https://github.com/user-attachments/assets/5797fd88-d4fd-416a-9e0a-8a1c3323f8bf" />

Unsurprisingly the acquisitions file can be accessed and read by unauthenticated users.

<img width="1716" height="877" alt="Screenshot 2026-08-24 161520" src="https://github.com/user-attachments/assets/c0f8061d-7cef-40f0-8424-289b567389f9" />

The underlying lesson to web developers is that security via obscurity isn't security at all. Ensure that all internal directories and services not intended for public use are locked behind extensive access controls.








