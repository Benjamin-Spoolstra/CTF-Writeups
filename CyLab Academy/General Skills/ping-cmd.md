# ping-cmd

---

### Challenge Details

> **Platform:** CyLab Academy  
> **Category:** `General Skills`  
> **Difficulty:** Easy  
> **Points:** 200

---

### Overview 

This challenge manipulates a remote service to reference its internal file system rather than pinging the Google DNS IP address like it's supposed to.

---

### Solution

This challenge looks to be a little more difficult than the obvious CTFs where the answer is a google search away.
<img width="1713" height="873" alt="Screenshot 2026-08-13 180527" src="https://github.com/user-attachments/assets/3707a69e-5bff-43fa-953d-acffe26a4aef" />

To start off this challenge connect to the remote server using Netcat and analyze it's behavior.
<img width="1716" height="875" alt="Screenshot 2026-08-13 180843" src="https://github.com/user-attachments/assets/6aadc836-e4ef-458e-b47c-065221c64bd8" />

Notice that the Google DNS server is the only allowed server that can be successfully pinged. Since the controls around the IP address are confirmed other gaps must be checked.

Consider adding commands after the IP address since the process is being executed in a shell session.

In the provided screenshot I tried inserting `&& echo "test"` which is a Linux command that outputs the word `test` to the terminal. This command tests if the server executes user input on the backend as it will be outputted in the final results.

<img width="1715" height="876" alt="Screenshot 2026-08-13 180855" src="https://github.com/user-attachments/assets/0a20a7d9-80fa-4c3c-81b6-8e0542527cdc" />

Finally after reading the file system and noticing a peculiar `flag.txt` file you can read its contents to the terminal.

Overall, this challenge was a fun test of creativity and out of the box thinking. Players weren't given much outside confirming the server was running on a shell session, so having a basic understanding of Linux and shells was essential to completing this challenge.

### Tools Used

- `Netcat`: A command-line networking utility used to send and receive data using TCP or UDP.

### Flag

```text
picoCTF{p1nG_c0mm@nd_3xpL0it_su33essFuL_773788ba}
```
