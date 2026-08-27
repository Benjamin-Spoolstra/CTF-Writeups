# Password Strength

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Easy
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A07:2025 Authentication Failures](https://owasp.org/Top10/2025/A07_2025-Authentication_Failures/) category on the OWASP Top 10. An unauthenticated attacker can brute force the password of the administrator account using well-known passwords and wordlists. This exposes the Juice Shop to a complete takeover and compromise, which directly threatens the confidentiality, integrity, and availability of customer information. Some of the information exposed includes full names, email addresses, full addresses, and credit card numbers. 

---

### Solution

To start this challenge an attacker needs to capture the Juice Shop's login request and create a ffuf bruteforcing template from it.

<img width="1717" height="871" alt="Screenshot 2026-08-27 141705" src="https://github.com/user-attachments/assets/9a701812-5d11-4f63-9b04-6c57f36c9632" />

Using a basic `top1050.txt` wordlist from the popular Github repository `Seclists` an attacker can fuzz the application and eventually find the correct password.

<img width="1717" height="875" alt="Screenshot 2026-08-27 141511" src="https://github.com/user-attachments/assets/cb5a58c3-adb0-4d6f-b1b3-7a541beea282" />

After confirming the password from the brute forcing an attacker can login as the application's administrator and complete the challenge.

<img width="1716" height="876" alt="Screenshot 2026-08-27 141817" src="https://github.com/user-attachments/assets/5dd064ba-d2f5-41d6-80f0-aef704034a54" />

<img width="1720" height="875" alt="Screenshot 2026-08-27 141841" src="https://github.com/user-attachments/assets/523a2e06-013f-40ca-babc-177348f1d3e4" />

This challenge demonstrates the need to use strong passwords on highly-privileged accounts. Ideally, strong passwords are ones that are more than 12-16 characters in length with a mix of capital letters, lowercase letters, numbers, and special symbols that aren't easily guessable.

If you want a creative way to check if you're password is strong try searching for it through the wordlists featured on `Seclists`. If it's included in any of those wordlists or a combination of such you should probably change it.

## Tools Used
- `ffuf` - a popular, open-source, web application fuzzing tool written in Go
