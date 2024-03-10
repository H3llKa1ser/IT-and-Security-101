# Attacks on cryptography

### 1) Ciphertext Only: Attacker has captured encrypted text on the network. Usually means all the attacker can do is brute force.

### 2) Known Plain Text: The attacker has captured ciphertext, but also knows what a portion of the message is in plain text (like an automatic signature)

### 3) Chosen Plaintext: Attacker can see the full text encrypted and decrypted. Usually, the attacker has initiated the message.

### 4) Chosen Ciphertext: An attacker can see whatever they want in plaintext or ciphertext. They have compromised a workstation. Sometimes called a lunchtime or midnight attack.

### 5) Meet In The Middle: These attacks are targeted towards algorithms like 3DES where there are multiple keys. An attacker tries to learn what each key does individually.
