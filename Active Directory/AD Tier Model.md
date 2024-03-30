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

## The problem with excessive privileges

### As networks grow, it is common to find accounts with more privileges than they should. There are many reasons why this may happen, including:

 - Users may be assigned privileges individually rather than based on their roles. This becomes hard to maintain as the company grows.
 - Privileges aren't revoked for users who leave the company.
 - Users who have moved through different positions in the company may still carry the privileges of their older roles. This problem is known as privilege creep.
 - No efforts have been made to reduce the default privileges assigned to users in the network.

### A significant number of overly privileged accounts can quickly become a problem. To get a better idea of why, take the following scenario into account:

 - 1) An attacker gains an initial foothold into your network using a recently published zero-day exploit. As a result, he gets local administrative privileges on the compromised host.
 - 2) Using tools like mimikatz, the attacker dumps the cached credentials of users who have recently logged into the machine. One of such credentials corresponds to the user "John".
 - 3) The attacker realises that "John" is a member of the Helpdesk group. Because of poor security practices, Helpdesk users have administrative privileges over all machines in the domain.
 - 4) The attacker now has administrative access to all computers through John's account.

### While many questionable security practices led to the compromise of the network in our example, had user John had a more restrictive set of privileges, the damage done by the attacker could have been contained to a portion of the network instead of affecting all machines.

### Correctly restricting the privileges of our domain users allows us to contain the damage done by an attacker should they steal a set of valid credentials.
