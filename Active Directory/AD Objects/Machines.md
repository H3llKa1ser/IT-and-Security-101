# Machines (AD)

### Every computer that joins the Active Directory domain, a machine object will be created.

### Machines are also considered "security principals" and are assigned an account just as any regular user.

### This account has somewhat limited rights within the domain itself.

### Machine accounts themselves are local administrators on the assigned computer, they are generally not suppossed to be accessed by anyone except the computer itself, but you can use it to login if you have the password.

## Machine Account Identifier:

 - Machine named DC01

 - Machine account DC01$

## NOTE: Machine account passwords are automatically rotated out and are generally comprised of 120 characters.
