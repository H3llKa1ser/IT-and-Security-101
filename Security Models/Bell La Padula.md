# Bell La Padula

### Confidentiality Model

### Developed by David Elliot Bell and Len LaPadula

#### 1) This model focuses on data confidentiality and access to classified information

#### 2) A formal model developed for the DoD (Department of Defense) multilevel security policy

#### 3) This format model divides entities in an information system into subjects and objects

#### 4) Model is built on the concept of a state machine with different allowable states

## The rules to enforce confidentiality

### 1) Tranquility property: Security labels cannot be arbitrarily changed

### 2) Simple Security property - "no read up": A subject cannot read data from a security level higher than subjects security level

### 3) Star Security property - "no write down": A subject cannot write data to a security level lower than the subject's security level

### 4) Strong star property -"no read/write up or down": A subject with read/write privilege can perform read/write functions ONLY at the subject's security levels
