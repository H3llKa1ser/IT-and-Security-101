# Hashing (Cryptographic Hash Functions)

### Hashing takes an input set of data (of almost arbitrary size) and returns a fixed-length result called the hash value. A hash function is the algorithm used to perform this transformation. When used with cryptographically strong hash algorithms, this is the most common method of ensuring message integrity today.

### Hashes have many uses in computing and security, one of which is to create a message digest by applying such a hash function to the plaintext body of a message. 

### To be useful and secure, a cryptographic hash function must demonstrate five main properties: 

#### 1) Useful: It is easy to compute the hash value for any given message.

#### 2) Nonreversible: It is computationally infeasible to reverse the hash process or otherwise derive the original plaintext of a message from its hash value (unlike an encryption process, for which there must be a corresponding decryption process).

#### 3) Content integrity assurance: It is computationally infeasible to modify a message such that re-applying the hash function will produce the original hash value. 

#### 4) Unique: It is computationally infeasible to find two or more different, sensible messages that hash to the same value.

#### 5) Deterministic: The same input will always generate the same hash, when using the same hashing algorithm.

### Cryptographic hash functions have many applications in information security, including digital signatures, message authentication codes and other forms of authentication. They can also be used for fingerprinting, to detect duplicate data or uniquely identify files, and as checksums to detect accidental data corruption. The operation of a hashing algorithm is demonstrated in this image.

### This is an example of a simple hashing function. The originator wants to send a message to the receiver and ensure that the message is not altered by noise or lost packets as it is transmitted. The originator runs the message through a hashing algorithm that generates a hash, or a digest of the message. The digest is appended to the message and sent together with the message to the recipient. Once the message is delivered, the receiver will generate their own digest of the received message (using the same hashing algorithm). The digest of the received message is compared with the digest sent by the originator. If the digests are the same, the received message is the same as the sent message.

### The problem with a simple hash function like this is that it does not protect against a malicious attacker that would be able to change both the message and the hash/digest by intercepting it in transit. The general idea of a cryptographic hash function can be summarized with the following formula:

#### variable data input + hashing algorithm = fixed bit size data output (the digest)

### Even the slightest change in the input message results in a completely different hash value.

### Hash functions are very sensitive to any changes in the message. Because the size of the hash digest does not vary according to the size of the message, a person cannot tell the size of the message based on the digest.

## Hashing Deep Dive

### Hashing puts data through a hash function or algorithm to create an alphanumeric set of figures, or a digest, that means nothing to people who might view it. No matter how long the input is, the hash digest will be the same number of characters. Any minor change in the input, a misspelling, or upper case or lower case, will create a completely different hash digest. So you can use the hash digest to confirm that the input exactly matches what is expected or required, for instance, a password.

### For example, we pay our rent through automatic withdrawal, and it’s $5,000 a month. Perhaps someone at the bank or at the rental office thinks they can just change it to $50,000 and keep the extra money. They think no one will notice if they just add another zero to the number. However, that change will completely change the digest. Since the digest is different, it will indicate that someone corrupted the information by changing the value of the automatic withdrawal, and it will not go through. Hashing is an extra layer of defense.

### Before we go live with a software product provided by a third party, for instance, we have to make sure no one has changed anything since it was tested by you and the programmer. They will usually send you the digest of their code and you compare that to the original. This is also known as a Checksum. If you see a discrepancy, that means something has changed. Then the security coders will compare the original one and the new one, and sometimes it’s very tedious, but they have software that can do it for them. If it’s something a little more intricate, they may need to go line by line and find out where the bugs are or if some lines need to be fixed. Often these problems are not intentional; they sneak in when you are making final adjustments to the software.

### An incident occurred at the University of Florida many years ago, where a very reputable software source, Windows 2000 or Millennium, was provided to 50,000 students via CD-ROMs, and the copies were compromised. The problems were detected when the digests did not match on a distribution file.


## Birthday Paradox AKA Hash Collision

### >50% chance 2 people share a birthday within a group of 23 people

#### (n(n-1)/2)

#### Hashes MUST NOT be susceptible to this


## Salting

### Random data used as an additional input to a hashing function

### Prevents dictionary attacks and rainbow table attacks
