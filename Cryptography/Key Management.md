# Key Management

### The most important part of any cryptographic implementation

### "A cryptosystem should be secure even if everything about the system, except the key is public knowledge" - Auguste Kerckhoff

# Key Management Applications

### 1) XML Key Management specification 2.0: Protocols for distributingand registering public keys.

### 2) ANSI X9.17: Developed to address the need of financial institutions. Uses Data Keys (DKs) and Key-encrypting Keys (KKMs).

# Key Distribution and Management

### Secure keys depend on Automated Key Generation, Randomness and Length

#### 1) Automated Key Generation: Key Enforcement Policy

#### 2) Randomness: The randomness of zeroes and ones

#### 3) Key Length: The longer the key, the more difficult it is

### Key Wrapping: The process of using key encrypting keys (KEK) to protect session keys.

#### 1) Good for sending keys over an untrusted transport

#### 2) Supports symmetric and asymmetric ciphers

### Out-of-Band: Key exchange that uses a medium other than that through which secure messages will be sent. Not very scalable.

### Key Distribution Center (KDC)

#### 1) Contains users public keys with a valid certificate

#### 2) Two keys: Master keys and Session keys

#### 3) KERBEROS

# Key Aspects

### Key Storage

#### 1) Encryption

#### 2) Expiration Date

#### 3) Backups

#### 4) Recovery

### Key Recovery

#### 1) Multiparty

#### 2) Common Directories

#### 3) Password Wallets

### Key Escrow

#### 3rd party holds key

### Web of Trust

#### Authenticity of a public key and its owner
