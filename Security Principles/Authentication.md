# Authentication

### When users have stated their identity, it is necessary to validate that they are the rightful owners of that identity. This process of verifying or proving the user’s identification is known as authentication. Simply put, authentication is a process to prove the identity of the requestor.

### There are three common methods of authentication:

#### 1) Something you know: Passwords or passphrases

#### 2) Something you have: Tokens, memory cards, smart cards

#### 3) Something you are: Biometrics, measurable characteristics

# Methods of authentication

### There are two types of authentication. Using only one of the methods of authentication stated previously is known as single-factor authentication (SFA) . Granting users access only after successfully demonstrating or displaying two or more of these methods is known as multi-factor authentication (MFA) . 

### Common best practice is to implement at least two of the three common techniques for authentication: 

#### 1) Knowledge-based

#### 2) Token-based

#### 3) Characteristic-based

### Knowledge-based authentication uses a passphrase or secret code to differentiate between an authorized and unauthorized user. If you have selected a personal identification number (PIN), created a password or some other secret value that only you know, then you have experienced knowledge-based authentication. The problem with using this type of authentication alone is that it is often vulnerable to a variety of attacks. For example, the help desk might receive a call to reset a user’s password. The challenge is ensuring that the password is reset only for the correct user and not someone else pretending to be that user. For better security, a second or third form of authentication that is based on a token or characteristic would be required prior to resetting the password. The combined use of a user ID and a password consists of two things that are known, and because it does not meet the requirement of using two or more of the authentication methods stated, it is not considered MFA.
