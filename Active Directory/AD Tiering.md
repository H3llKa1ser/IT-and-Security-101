# AD Tier Model

### To limit the impact of lateral movement or privilege escalation vectors, Microsoft proposes the implementation of the AD Tier Model, which segments the network into three tiers:

 - Tier 0: Contains the Domain Controllers and every other server with administrative control over the Windows domain, including Exchange servers, CA servers and identity management solutions.
 - Tier 1: Contains all servers that provide services to the business but have no administrative control over the Windows domain, including application servers, database servers, file-sharing servers and much more.
 - Tier 2: Contains regular users' workstations and other end-user devices.
