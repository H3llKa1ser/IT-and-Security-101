# Security Groups

### They are also considered "security principals" and can have privileges over resources on the network.

### Group can have both users and machines as members. If needed, groups can include other groups as well.

## SECURITY GROUP -> DESCRIPTION

#### 1) Domain Admins

 - Users of this group have administrative privileges over the entire domain. By default they can administer any computer on the domain, including DCs.

#### 2) Server Operators

 - They can administer domain controllers. They cannot change any administrative group members.

#### 3) Backup Operators

 - They can access any file regardless of their permissions. They are used to perform backups of data on computers.

#### 4) Account Operators

 - They can create or modify accounts in the domain.

#### 5) Domain Users

 - Existing user accounts in the domain.

#### 6) Domain Computers

 - Existing computers in the domain.

#### 7) Domain Controllers

 - Existing DCs in the domain.
