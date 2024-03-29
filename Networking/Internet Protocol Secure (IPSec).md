# Internet Protocol Secure (IPSec)

### Provides the framework for services such as encryption, authentication, integrity. (Any of these services may be provided)

### IPSec provides encapsulation, not encryption

### What is encapsulated can be protected through the protocols within IPSec.

## IPSec is an encapsulation framework.

## Tunnel VS Transport mode dictates what portion of the IP packet is to be encapsulated.

### 1) Tunnel mode: Whole packet is encapsulated

### 2) Transport mode: ONLY the payload is encapsulated

## IPSec Sub-Protocols

### 1) Authentication Header (AH): Used to identify the sender and ensure the transmitteed data has not been altered. Uses hashes and sequence numbers.

### Provides integrity, authenticity and non-repudiation through the use of an ICV (Integrity Check Value).

### The ICV is run on the entire packet (header, data ,trailer) except for particular fields, in the header that are dynamic (like TTL, etc). NO CONFIDENTIALITY!

### 2) Encapsulating Security Payload (ESP): Consists of

#### Header: Seq. number and Security Associations

#### Payload: Encrypted part of the packet

#### Trailer: Padding if required

#### Authentication: Hash value of the packet

### Provides authenticity and integrity through a MAC (NO NON-REPUDIATION since a MAC is symmetric).

### The main service provided is ENCRYPTION! ICV is run on payload only.

### 3) Internet Key Exchange (IKE): Authentication part of IPSec

#### PHASE 1: Authentication using:

#### A shared secret

#### Public Key Encryption

#### Revised Mode of Public Key Encryption

#### PHASE 2: Security Associations are established

### No security services! Just management of secure connection

#### 1) Oakley: Uses Diffie Hellman to agree upon a key

#### 2) Internet Security Association and Key Managemnent Protocol (ISAKMP): Manages keys, security associations (SAs), and Security Parameters Index (SPI)

# Security Associations and SPIs example:

#### 1) Destination Address: 192.168.1.1

#### 2) Security Parameter Index (SPI): 1A2B3C4D

#### 3) IPSec Transform: AH, HMAC-MD5

#### 4) Key: 1234ABCDE5

#### 5) Additional SA Attributes: One day or 100MB

## These make up for a Security Association (SA)
