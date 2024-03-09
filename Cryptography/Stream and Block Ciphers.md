# Stream and Block Ciphers

### Stream-based Ciphers: When encryption is performed, it happens on a bit-by-bit basis

### Mix the plaintext with a keystream to produce the ciphertext (Example: XOR operation)

### Block Ciphers: Operate on chunks of text instead of one byte at a time

### Blocks are often 64, 128, 192 bit sizes and so on. (Add 64 every time)

### Use a combination of substitution and transposition

#### Substitution: The process of exchanging one letter or byte for another

#### Transposition: The process of reordering the plaintext to hide the message

## Stream VS Block

### Stream:

#### 1) Weaker 

#### 2) Less Intensive

#### 3) Used in Hardware

### Block:

#### 1) Stronger

#### 2) Computationally Intensive

#### 3) Used in Software

## Block Cipher Modes

### 1) Electronic Code Book (ECB): Each block is encrypted independently 

### 2) Cipher Block Chaining (CBC): The result of encrypting one block of data is fed back into the process (IV) to encrypt the next block

### 3) Cipher Feedback (CFB): Each block of keystream comes from encrypting the previous block of ciphertext

### 4) Output feedback (OFB): The keystream is generated independently of the message

### 5) Counter (CTR): Uses the formula Encrypt (Base+N) as a keystream generator where Base is a starting 64 bit number and N is a simple incrementing function
