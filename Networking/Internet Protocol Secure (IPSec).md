# Internet Protocol Secure (IPSec)

### Provides the framework for services such as encryption, authentication, integrity. (Any of these services may be provided)

### IPSec provides encapsulation, not encryption

### What is encapsulated can be protected through the protocols within IPSec.

## IPSec is an encapsulation framework.

## Tunnel VS Transport mode dictates what portion of the IP packet is to be encapsulated.

### 1) Tunnel mode: Whole packet is encapsulated

### 2) Transport mode: ONLY the payload is encapsulated

## IPSec Sub-Protocols

### 1) Authentication Header (AH): Provides integrity, authrnticity and non-repudiation through the use of an ICV (Integrity Check Value).

### The ICV is run on the entire packet (header, data ,trailer) except for particular fields, in the header that are dynamic (like TTL, etc). NO CONFIDENTIALITY!

### 2) Encapsulating Security Payload (ESP): Provides authenticity and integrity through a MAC (NO NON-REPUDIATION since a MAC is symmetric).

### The main service provided is ENCRYPTION! ICV is run on payload only.

### 3) Internet Key Exchange (IKE): No security services! Just management of secure connection

#### 1) Oakley: Uses Diffie Hellman to agree upon a key

#### 2) Internet Security Association and Key Managemnent Protocol (ISAKMP): Manages keys, security associations (SAs), and Security Parameters Index (SPI)

# Security Associations and SPIs example:

#### 1) Destination Address: 192.168.1.1

#### 2) Security Parameter Index (SPI): 1A2B3C4D

#### 3) IPSec Transform: AH, HMAC-MD5

#### 4) Key: 1234ABCDE5

#### 5) Additional SA Attributes: One day or 100MB

## These make up for a Security Association (SA)
