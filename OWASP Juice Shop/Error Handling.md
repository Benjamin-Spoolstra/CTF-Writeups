# Error Handling

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Easy
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A10:2025 Mishandling of Exceptional Conditions](https://owasp.org/Top10/2025/A10_2025-Mishandling_of_Exceptional_Conditions/) category on the OWASP Top 10. An unauthenticated attacker can trigger verbose server errors that reveal sensitive system information such as server, framework, and library versions as well as internal resource paths. These errors could be used to discover more serious vulnerabilities and pivot towards internal resources if not properly configured. 

---

### Solution

To start this challenge an attacker needs to find or trigger a verbose server error. 

<img width="1721" height="873" alt="Screenshot 2026-08-27 151740" src="https://github.com/user-attachments/assets/75b5c7a4-1bf4-44d0-8455-a3910688f33c" />

The easiest way to accomplish this goal is to access log files restricted by the server's access controls in the `/ftp` directory, which can be found through the `robots.txt` file. 

<img width="1712" height="872" alt="Screenshot 2026-08-28 183425" src="https://github.com/user-attachments/assets/03a5b689-4769-4c69-bd54-6b9f8f5dfdc5" />

After going to the `suspicious_error.yml` file you will see a verbose server error printed to the screen, which reveals sensitive internal information such as JavaScript library versions, server resource paths, and the server's version and type.

<img width="1713" height="875" alt="Screenshot 2026-08-28 183411" src="https://github.com/user-attachments/assets/07576e80-523d-4a4f-ba1e-f586901bc86a" />

An attacker could potentially use this information as the foundation for a more critical attack such as privilege escalation or information disclosures.

Implementing graceful, vague error messages in the event a server fails ensures critical backend information isn't disclosed to malicious users or threat actors, while still providing developers a useful guide when testing their applications.

