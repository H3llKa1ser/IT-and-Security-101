# Message Authentication Codes (MAC)

## Integrity

### Data could be modified:

#### 1) Accidentally through corruption

#### 2) Intentionally through malicious alteration

### Hash: Only good for accidental modification

### MAC: Provides reasonable authenticity and integrity, not strong enough to be non-repudiation (because it uses a summetric key)

### Digital Signatures: Can detect both malicious and accidental modification, but requires an overhead. Provides TRUE non-repudiation.

## Message + Symmetric Number + Hashing Algorithm = HMAC (Hashing Message Authentication Codes)

### Integrity and (reasonable) authenticity

### A MAC does not provide true non-repudiation (symmetric)
