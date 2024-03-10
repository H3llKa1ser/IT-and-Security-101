# Public Key Infrastructure (PKI)

### A set of system, software and communication protocols required for public key cryptography

### The primary purposes are:

#### 1) Publish public keys/certificates

#### 2) Certify that a key is tied to an individual or entity

#### 3) Provide verification of the validity of a public key

## Certificates

### X.509 v.4 standard

### Provides authenticity of a server's public key

### Necessary to avoid Man In The Middle (MiTM) attacks with servers using SSL/TLS

### Digitally signed by a Certificate Authority 

#### 1) Certificate Authority (CA): A component of a PKI that creates and maintains digital certificates throughout their lifecycles

#### 2) Registration Authority (RA): Verifies an entity's identity and determines whether they are entitled to have a public key certificate issued

#### 3) Certificate Repository

#### 4) Certificate Revocation List (CRL): List that is maintained by the CA of a PKI that contains information revoked digital certificates

## Certificate Revocation

### CRL: CA publishes CRL. Client is responsible for downloading to see if a certificate has been revoked.

### OCSP (Online Certificate Status Protocol): Streamlines the process of verifying whether or not a certificate has been revoked.
