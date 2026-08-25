# Admin Section

---

### Challenge Details

> **Platform:** OWASP Juice Shop                                     
> **Category:** `Web Exploitation`  
> **Difficulty:** Medium
---

### Overview

This challenge on the OWASP Juice Shop corresponds to the [A01:2025 - Broken Access Control](https://owasp.org/Top10/2025/A01_2025-Broken_Access_Control/) category on the OWASP Top 10. An unauthenticated attacker is able to access the administration section of the shop by chaining a SQL Injection attack in the login portal with a directory fuzzing attack. 

---

### Solution

To start this challenge it's important to consider where administration sections within applications typically exist. They're usually on the main application server, which is accessed through a hidden directory or file that is locked behind server-side access controls. 

<img width="1712" height="872" alt="Screenshot 2026-08-24 160734" src="https://github.com/user-attachments/assets/f5de0241-7f9c-4ca0-b468-855993aa2621" />

With this in mind, an attacker can try fuzzing the app for common administration directories and locations. This will surface a `/#/administration` endpoint locked behind server-side access controls. If an attacker accesses the endpoint directly they'll receive an HTTP 403 response code.

HTTP 403 response codes occur due to the requestor not having the necessary level of privileges to access the requested resource. This informs the attacker that they need to elevate their privileges to an administrator role to see the contents of the directory.

The most straightforward method to escalate privileges is to abuse the login portal. This method that doesn't require any advanced exploitation.

<img width="1712" height="871" alt="Screenshot 2026-08-24 160751" src="https://github.com/user-attachments/assets/b8035c57-36da-40da-a621-12835524f31e" />

However, it's clear that an attacker isn't provided any administrator-level credentials. So how would they access an administrator account?

This is where another common web vulnerability becomes useful to test. 

SQL Injections are SQL database vulnerabilities that allow unauthenticated attackers to bypass access controls or leak confidential information.

They occur due to improper input sanitization by developers who append user inputs to direct SQL database queries. 

Testing for SQL Injection vulnerabilities is a typically straightforward process.

An attacker can use a single quote `'` as a basic input test to observe the application's behavior. This scenario assumes that this shop is authenticating users based on the username and password fields stored in a SQL database, which is typical in basic web applications. 

By entering a single quote into the username field an attacker can observe an unusual response message. The typical response is `Invalid username or password` for incorrect login combinations on this application, but this message is `[object Object]`. 

<img width="1713" height="871" alt="Screenshot 2026-08-24 160809" src="https://github.com/user-attachments/assets/359b2bdc-5dcc-4855-891d-f0a1455ebf5c" />

The unusual error message confirms that the application is appending user input into a direct SQL database query. This confirms the attacker's suspicions that the login is using a SQL database, and verifies that the conditions needed for a SQL Injection vulnerability to exist. 

The next step is to test a common SQL Injection payload. 

`' OR 1=1--'` is a SQL payload that injects a logical operator into the backend SQL query, which returns always true. The `--` at the end of the statement is a SQL comment, which will cause the application to ignore the rest of the query.

<img width="1716" height="877" alt="Screenshot 2026-08-24 160842" src="https://github.com/user-attachments/assets/669d6f78-2e53-46f0-8fb9-047577fb8f5d" />

After inputting the payload into the username field an attacker is successfully logged in as the first account in the SQL database, which is an administrator account. 

<img width="1713" height="865" alt="Screenshot 2026-08-24 160915" src="https://github.com/user-attachments/assets/8d00bea6-f7bf-4c38-b1b2-56b36bb41610" />

Now that they are in the application with the necessary level of privileges they can directly access the administration section and solve the challenge. 

<img width="1712" height="875" alt="Screenshot 2026-08-24 160959" src="https://github.com/user-attachments/assets/89c933ea-eee4-4297-8175-1fd9c4dde440" />

In the administration panel all users with their associated comments registered to the application are visible.

This challenge demonstrates fundamental broken access control and input sanitization vulnerabilities that, when chained, allow unauthenticated attackers to escalate to application administrators, which threatens the confidentiality and integrity of the application's data. 


