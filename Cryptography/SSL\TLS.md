# Secure Sockets Layer/Transport Layer Security (SSL/TLS)

### Implementation steps example (Arrows in this example represent the traffic flow between the client and the server):

#### 1) Client browses to "example.com" -->

#### 2) "example" sends its public key <--

#### Encrypted with "example"'s public key 1234567 Symmetric session key -->

#### 3) Client's web browser generates a symmetric session key

#### 4) Client uses server's public key to encrypt the symmetric session key and sends it to the server

#### 5) Server uses its private key to decrypt the symmetric key

### Now that both parties know the symmetric key, they use symmetric encryption to encrypt the remainder of the communication
