# Reflected XSS

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Easy
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A05:2025 Injection](https://owasp.org/Top10/2025/A05_2025-Injection/) category on the OWASP Top 10. An unauthenticated attacker can exploit a reflected Cross-Site Scripting (XSS) vulnerability in the product search functionality to steal user cookies and execute unintended actions on behalf of another user on the application. This vulnerability comes down to improper input sanitization. It is essential for web applications to sanitize and validate user input before sending it downstream to ensure malicious inputs aren't executed or reflected. 

---

### Solution

To start this challenge an attacker is tasked with looking for a reflected Cross-Site Scripting (XSS) vulnerability in the application. 

They're given a specific payload to use to trigger the vulnerability via an alert popup using JavaScript.

<img width="1717" height="876" alt="Screenshot 2026-08-26 145703" src="https://github.com/user-attachments/assets/33b8cafb-93f9-416e-b743-017238cfe347" />

One of the easiest ways to find XSS vectors is by analyzing the local JavaScript files in an application. 

They can reveal additional endpoints that interact with a backend system, including the specific ways inputted data is treated.

However, JavaScript files can often be large, so knowing what areas of the application to look in is essential for reducing the time taken to uncover XSS vulnerabilities. 

An experienced attacker may theorize that the product search functionality on this application is a prime suspect, since it reflects the search query of the user.

<img width="1711" height="875" alt="Screenshot 2026-08-26 151416" src="https://github.com/user-attachments/assets/318f2d71-3ade-403d-b362-99209e98d142" />

Looking at the `main.js` file a suspicious `search(e)` function can be identified near the bottom of the file. This function is unique because the inputs are not parameterized like the proceeding functions, which is a common sign XSS may be possible.

With this finding an attacker can test the provided payload on the search functionality to confirm if the data is reflected and executed.

<img width="1717" height="872" alt="Screenshot 2026-08-26 150016" src="https://github.com/user-attachments/assets/11ee9174-537c-487f-9ea8-903fb8190374" />

After receiving a JavaScript alert popup XSS is confirmed by the attacker. This vulnerability could be exploited for use in account takeover or session theft attacks, but it is more than enough for this challenge.

Overall, reflected XSS attacks are a result of insecure coding that improperly trusts user input. It is a best practice to sanitize and validate user input using parameterization or encoding methods to ensure data is not treated literally in a downstream system, such as a database or web server. 




