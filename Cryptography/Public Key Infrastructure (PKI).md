# Public Key Infrastructure (PKI)

## Certificates

### X.509 v.4 standard

### Provides authenticity of a server's public key

### Necessary to avoid Man In The Middle (MiTM) attacks with servers using SSL/TLS

### Digitally signed by a Certificate Authority 

#### 1) Certificate Authority (CA)

#### 2) Registration Authority (RA)

#### 3) Certificate Repository

#### 4) Certificate Revocation List (CRL)

## Certificate Revocation

### CRL: CA publishes CRL. Client is responsible for downloading to see if a certificate has been revoked.

### OCSP (Online Certificate Status Protocol): Streamlines the process of verifying whether or not a certificate has been revoked.
