# AD Tier Model

## Least privilege model

### One of the toughest challenges you'll face when implementing a Windows domain infrastructure is correctly assigning privileges to each user/service. As a domain admin, you will be faced with questions such as:

 - Should all/some users have administrative rights over their PCs?
 - Should domain administrative users be able to log in to any domain PC?
 - Who needs to be part of the Domain Administrators group?
 - How should we provide accounts for external users as contractors?

### While there's no answer to fit all cases, most administrators will start by implementing a baseline that follows the least privilege model. In simple terms, the least privilege model consists of assigning each user/service strictly the privileges they need to perform their usual tasks and nothing more.

### Having our identity management built upon this model is advantageous for the following reasons:

 - We will stop legitimate users from abusing excessive privileges to access sensitive information.
 - If a user's credentials are compromised, attackers will be heavily limited to only performing tasks permitted to the compromised user. This will prevent or at least complicate lateral movement and privilege escalation techniques.
 - If a user executes malware, its propagation will likely be limited by the strict privileges of the compromised account.
