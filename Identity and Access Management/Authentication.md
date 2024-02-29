# Authentication

### Proving a claimed identity

#### 1) Something you know (Password, security question, etc)

#### 2) Something you have (key, card, Yubikey, etc)

#### 3) Something you are (Retina scan, fingerprint, etc)

## The strongest authentication is multi-factor (MFA) a combination of the 2.

### Mutual authentication is desirable as well

## ANY single means of authentication can be spoofed

##  Type 1: Something you know

### Examples: Passwords/Passphrases/Cognitive password

### Traditional best practices

#### 1) 8 characters

#### 2) Change on a regular basis

#### 3) Upper and lower

#### 4) Include Alphanumerics and non-alphanumeric

#### 5) Enforce password history

#### 6) Consider brute-force and dictionary attacks

#### 7) Ease of cracking cognitive passwords

#### 8) Graphic Image

#### 9) Enable clipping levels and respond accordingly

## Type 2: Something you have 

#### 1) Token Devices

#### 2) Smart Card

#### 3) Memory Card

#### 4) Hardware Key

#### 5) Cryptographic Key

#### 6) Certificate

#### 7) Cookies

### Token Devices: One-Time password generators

### Password that is used only once that is it no longer valid

#### 1) One-Time Password (OTP) reduces vulnerability associated with sniffing passwords

#### 2) Simple device to implement

#### 3) Can be costly

#### 4) Users can lose or damage

#### 5) Two types: Synchronous/Asynchronous

## Synchronous Token Devices

#### 1) Rely upon synchronizing with authentication server. Frequently time based, but could be event based

#### 2) If damaged, or battery fails, must be re-synchronised

#### 3) Authentication server knows what "password" to expect based on time or event 

## Asynchronous Token Devices

#### 1) Challenge response

#### 2) User logs in

#### 3) Authentication returns a challenge to the user

#### 4) User types challenge string into token device and presses enter

#### 5) Token device returns a reply 

#### 6) Only that specific user's token device could respond with the expected reply

#### 7) More complex than synchronous

## Static Password Tokens

### The device contains a password that is physically hidden (not visible to the possesor) but that is transmitted for each authentication

## Synchronous Dynamic Password Token:

### A timer is used to rotate through various combinations produced by a cryptographic algorithm. The token and the authentication server must have synchronized clocks.

## Asynchronous Password Token: A one-time password is generated without the use of a clock, from either a one-time pad or a cryptographic algorithm

#### 1) Challenge value displayed on computer

#### 2) User enters challenge value into token device

#### 3) Token presents a different value to the user

#### 4) User gives value to computer

#### 5) Value is sent to server

## Challenge Response Token: The authentication server encrypts a challenge with a public key, the device proves it possesses a copy of the matching private key by providing the decrypted challenge

## Memory Cards

#### 1) Hold information, does NOT process

#### 2)  A memory card holds authentication info. Usually you'll want to pair this with a PIN. WHY?

#### 3) A credit card or ATM card is a type of memory card, so is a key/swipe card

#### 4) Usually insecure, easily copied

## Contant cards: Need to be inserted into a smart card reader with a direct connection. E.G. Credit card with a chip reader

## Contactless cards: Requires close proximity to a reader. Both have antennae and use radio frequency. E.G. Apple Pay, Tap to pay

## Type 3: Something you are/do

### Biometrics

#### 1) Physiological (Static): Should not significantly change over time. Bound to a user's physiological traits. E.G. Fingerprint, hand geometry, iris, retina, vascular, hand, etc

#### 2) Behavior-based (Dynamic): Based on behavioral traits. E.G. Voice, signature, keyboard cadence, etc.

### Even though these can be modified temporarily, they are very difficult to modify for any significant length of time.

### Biometric concerns:

#### 1) User acceptance

#### 2) Many users feel biometrics are intrusive

#### 3) Retina scans can reveal healthcare information

#### 4) Time for enrollment and verification can make users resistant

#### 5) Cost/benefit analysis

#### 6) No way to revoke biometrics

# Multifactor Authentication (MFA)

### Authentication consists of 3 categories as explained above:

#### 1) Something you know

#### 2) Something you have

#### 3) Something you are

### Multifactor authentication: ANY 2 of the 3 categories

## Examples:

### MFA = Password + smart card

### NOT MFA = Retina scan + voice recognition (It's the same category so it is not classified as MFA)

## Dual control (AKA Split-knowledge)

### Requiring 2 people to perform an action
