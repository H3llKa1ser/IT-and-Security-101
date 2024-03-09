# Message Authentication Codes (MAC)

### A small block of data that is generated using a secret key and then appended to the message

### Integrity

### Data could be modified:

#### 1) Accidentally through corruption

#### 2) Intentionally through malicious alteration

### Hash: Only good for accidental modification

### MAC: Provides reasonable authenticity and integrity, not strong enough to be non-repudiation (because it uses a summetric key)

### Digital Signatures: Can detect both malicious and accidental modification, but requires an overhead. Provides TRUE non-repudiation.

## Message + Symmetric Number + Hashing Algorithm = HMAC (Hashing Message Authentication Codes)

### Cryptographic hash function that uses a symmetric key value and is used for data integrity and origin authentication

### Integrity and (reasonable) authenticity

### A MAC does not provide true non-repudiation (symmetric)
