# Attacks on cryptography

### 1) Ciphertext Only: Attacker has captured encrypted text on the network. Usually means all the attacker can do is brute force.

### 2) Known Plain Text: The attacker has captured ciphertext, but also knows what a portion of the message is in plain text (like an automatic signature)

### 3) Chosen Plaintext: Attacker can see the full text encrypted and decrypted. Usually, the attacker has initiated the message.

### 4) Chosen Ciphertext: An attacker can see whatever they want in plaintext or ciphertext. They have compromised a workstation. Sometimes called a lunchtime or midnight attack.

### 5) Meet In The Middle: These attacks are targeted towards algorithms like 3DES where there are multiple keys. An attacker tries to learn what each key does individually.

### 6) Differential Cryptanalysis: Also called a side channel attack. This attack uses the study of how differences in an input can affect the resultant difference at the output

### 7) Linear cryptanalysis: A known plaintext attack that uses liner approximations to describe the behavior of the block cipher

### 8) Algebraic attack: Exploits vulnerabilities within the intrinsic algebraic structure of mathematical functions

### 9) Rainbow table: A lookup table of sorted hash outputs. Hash values are saved to refer to at a later time

### 10) Frequency analysis: Used to identify weaknesses within cryptosystems by locating patterns in resulting ciphertext. Works well with other types of attacks.

### 11) Birthday attack: Attack that exploits the mathematics behind the birthday problem in the probability theory forces collisions within hash functions.

### 12) Dictionary attack: Encrypts all of the words in a dictionary and checks if the hash matches the password hash.

### 13) Replay attack: Occurs when an attacker intercepts authentication information and replays the information to gain access to a security system.
