# AD Tier Model

### To limit the impact of lateral movement or privilege escalation vectors, Microsoft proposes the implementation of the AD Tier Model, which segments the network into three tiers:

 - Tier 0: Contains the Domain Controllers and every other server with administrative control over the Windows domain, including Exchange servers, CA servers and identity management solutions.
 - Tier 1: Contains all servers that provide services to the business but have no administrative control over the Windows domain, including application servers, database servers, file-sharing servers and much more.
 - Tier 2: Contains regular users' workstations and other end-user devices.

# Tiered Administrator Accounts

### By separating machines into tiers, we can create administrative credentials with access to their respective tier only to limit the impact of a compromise. Users needing administrative privileges over several tiers will have different credentials to access each separately.

## Note: Users are assigned to tiers for administrative purposes only. Regular users will not be part of a tier.

## Note 2: If a user holds several credentials for different tiers, each should have a different password. Having the same password defeats their purpose!

## Establishing Boundaries Between Tiers

### For the tiered model to work as expected, we must ensure that users are restricted to their respective tiers. Creating tiered accounts is the first step, but more is needed. For example, a user might mistakenly use their tier 1 credentials to log into a tier 2 workstation. If the workstation was somehow under an attacker's control, the user's credentials could be stolen by several means, including:

 - The attacker could try to dump cached domain credentials from the machine using mimikatz or similar methods.
 - The attacker could use a keylogger to try and capture the user's password.
 - The attacker could use internal phishing strategies to trick users into revealing their passwords.

### As a result, the attacker would gain a tier 1 credential and elevate their privileges on the network.

### Avoiding such scenarios can be attained by enforcing strict boundaries between tiers. Users shouldn't be allowed to log into a lower tier than the one they are meant to access, not even by mistake.

### Limits between tiers should obey the following principles:

 - Assets in higher tiers can control other assets in the same or lower tiers. Notice that this refers to the capacity of modifying assets in Active Directory rather than administering machines in lower tiers. For example, a tier 1 user could change the GPOs associated with tier 2 assets or reset passwords for tier 2 users. On the other hand, they should never be able to modify tier 0 assets, as this would lead to privilege escalation paths.
 - Users should never log into lower-tier machines. Since Windows caches credentials for users that log into a machine, having a higher-tier user log into a lower-tier machine would also enable privilege escalation paths. Users can optionally log into higher tiers only if strictly needed and use specific services. Interactive logons across tiers are not permitted.
   
