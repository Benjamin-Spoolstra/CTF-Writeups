# Payback Time

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Medium
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A06:2025 Insecure Design](https://owasp.org/Top10/2025/A06_2025-Insecure_Design/) category on the OWASP Top 10. An authenticated attacker can exploit a business logic flaw in the checkout system that arbitrarily credit funds toward their account. This vulnerability is due to a lack of server-side inventory validations, which would restrict values of stock being purchased to only positive numbers.

---

### Solution

To start this challenge an attacker needs to add any item to their cart.

<img width="1716" height="876" alt="Screenshot 2026-08-26 151718" src="https://github.com/user-attachments/assets/b243de85-66ee-4a0b-95f4-2c7f4ffe4fb6" />

After doing this they can attempt to remove the item, but capture the removal request with a proxy before it reaches the server.

<img width="1713" height="875" alt="Screenshot 2026-08-26 151912" src="https://github.com/user-attachments/assets/d023eb83-6a50-449c-834e-8ff041f9538f" />

The attacker can modify the request body to change the amount of the item from a positive number to a negative number. 

<img width="1717" height="877" alt="Screenshot 2026-08-26 151951" src="https://github.com/user-attachments/assets/195c646c-63fe-4745-a43a-550b1fce35d3" />

They can then forward this request to the server, which will successfully update the item count to the specified amount.

<img width="1717" height="876" alt="Screenshot 2026-08-26 152008" src="https://github.com/user-attachments/assets/8f69cc05-f56d-4ef2-a875-ca0391a0fdd7" />

Finally, the attacker can checkout, and receive a credit to their account for the number of items purchased.

<img width="1721" height="876" alt="Screenshot 2026-08-26 152037" src="https://github.com/user-attachments/assets/e825741f-3c3f-4261-923d-d0ffa9ebc169" />

The vulnerability in this challenge results from a lack of server-side item amount validations, which allows attackers to arbitrarily drain funds from the application.

## Tools Used
- `Burp Suite` - a popular, commercial web application proxy that facilitates industry-grade web application security testing
