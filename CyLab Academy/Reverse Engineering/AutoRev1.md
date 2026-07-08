# AutoRev1

---

### Challenge Details

> **Platform:** CyLab Academy  
> **Category:** `Reverse Engineering`  
> **Difficulty:** Medium  
> **Points:** 200

---


### Overview

AutoRev1 is a reverse engineering challenge that requires exploiting a misconfiguration in a remote service. The remote service sends a binary-encoded value in each message, and requests the decimal equivalent of the binary be provided as the answer. The goal is to automate the responses fast enough to return 20 binaries in under 20 seconds and recover the flag.

---

### Solution

#### Loading the Challenge Instance

The first step was launching the challenge instance from picoCTF and connecting to the remote service using `netcat`.

<img width="1919" height="869" alt="step1" src="https://github.com/user-attachments/assets/18a6d61c-0185-4844-959c-c5ea786a237f" />

#### Netcat Connection and Initial Interaction

After connecting with `netcat`, the service printed a new binary blob each round along with a decimal value at the start of the message. After converting the provided binary I noticed that it corrosponded to the provided decimal value at the beginning of the message. This made it clear that the task was to extract the decimal secret from each prompt and send it back before the one-second limit expired.  

<img width="1919" height="861" alt="step2" src="https://github.com/user-attachments/assets/bcc5f671-1e87-4064-8e5d-4499712490ba" />

#### Entering a Test Value

A manual test input was attempted first to verify the interaction format. The service accepted input, but the round still depended on speed, which confirmed that manual solving would not be reliable for all 20 rounds.  

<img width="1919" height="869" alt="step3" src="https://github.com/user-attachments/assets/cb7018c8-6751-442d-a9d2-9d78d4ed8c16" />

#### Value Entered Too Slow

When the response was entered by hand, the service reported that it was too slow. That confirmed the challenge was designed around automation rather than manual conversion.  

<img width="1919" height="870" alt="step4" src="https://github.com/user-attachments/assets/06a0f35c-c7f9-42a1-b7c5-2461300f9e2b" />

#### Automating with Python

To solve the challenge consistently, a Python script was written to connect to the service, read each prompt, extract the decimal secret with a regular expression, and send it back automatically. The script loops through all 20 rounds and then checks the final output for the flag.  

```python
import socket
import re
import time

def solve():
    # Connection details
    host = 'mysterious-sea.picoctf.net'
    port = 63787

    # Regex to find the decimal secret (the number appearing before the binary)
    # It looks for a sequence of digits followed by text about the binary
    secret_pattern = re.compile(rb'(\\d+)\\s+Here\\'s the next binary')

    try:
        # Create socket and connect
        with socket.create_connection((host, port)) as s:
            print(f"[*] Connected to {host}:{port}")

            for i in range(1, 21):
                data = b""
                # Keep reading until we see the prompt
                while b"What's the secret?:" not in data:
                    chunk = s.recv(4096)
                    if not chunk:
                        break
                    data += chunk

                # Search for the decimal secret in the received data
                match = secret_pattern.search(data)
                if match:
                    secret = match.group(1)
                    print(f"[+] Round {i}: Sending secret {secret.decode()}")

                    # Send the secret followed by a newline
                    s.sendall(secret + b"\\n")
                else:
                    print(f"[!] Could not find secret in Round {i}")
                    break

            # After 20 rounds, read the final response to get the flag
            time.sleep(1)  # Brief pause to ensure server processes last input
            final_data = s.recv(4096).decode(errors='ignore')

            flag = re.search(r'picoCTF\\{.*\\}', final_data)
            if flag:
                print(f"\\n[***] FLAG FOUND: {flag.group(0)}")
            else:
                print("\\n[!] Rounds complete, but flag not found in output:")
                print(final_data)

    except Exception as e:
        print(f"[!] Error: {e}")

if __name__ == "__main__":
    solve()
```
<img width="1919" height="865" alt="step5" src="https://github.com/user-attachments/assets/535e1ad6-1b5c-425b-bdf4-585f5f708d11" />

#### Running the Script

Once the script was saved, it was executed against the challenge server. The output showed each round being solved automatically, which bypassed the speed limit that caused the manual attempt to fail.  

<img width="1917" height="866" alt="step6" src="https://github.com/user-attachments/assets/31525851-6d4a-4cd2-995a-b6adaebd6782" />

#### Outputting the Flag

After the final round, the server returned the flag and the script printed it successfully. The output confirms the automation worked end-to-end and completed the challenge.  

<img width="1919" height="866" alt="step7" src="https://github.com/user-attachments/assets/6d5ba306-1112-45bf-b4bd-4677f389043b" />

### Tools Used

- `netcat`: Used to inspect the challenge service manually.
- `Python socket`: Used to automate the remote connection and responses.
- `Python re`: Used to parse the decimal secret and final flag.
- `Python time`: Used to pause briefly before reading the final server output.

### Flag
```text
picoCTF{4u7o_r3v_g0_brrr_78c345aa}
```
