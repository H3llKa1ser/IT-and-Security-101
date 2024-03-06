# Secure/Multipurpose Internet Mail Extensions (S/MIME)

## P.A.I.N. Attributes

### 1) Privacy: Receiver's public key

### 2) Authenticity: Sender's private key 

### 3) Integrity: Hash/Checksum/CRC: NEITHER SYMMETRIC NOR ASYMMETRIC

### 4) Non-repudiation: Hash encrypted by sender's private key

# Digital Envelopes in S/MIME

### S/MIME

#### 1) Standards based secure email by creating a digital envelope

### Sender functions:

#### 1) Calculate hash value on message

#### 2) Encrypt message with session key

#### 3) Encrypt hash value with private key

#### 4) Encrypt session key with receiver's public key

### Receiver functions:

#### 1) Decrypt session key with private key

#### 2) Decrypt hsah value with sender's public key

#### 3) Decrypt message

#### 4) Calculate hash value and compare with one sent
