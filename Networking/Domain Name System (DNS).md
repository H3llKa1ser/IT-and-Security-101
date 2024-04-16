# Domain Name System (DNS)

## Ports: 53/TCP, 53/UDP

### DNS is a hierarchical distributed naming system for any resource connected to the internet or a private network

### A global databaser, scalable, dynamic database that translates domain names to IP addresses

# DNS Record Types

#### 1) A record: Resolve to IPv4 addresses

#### 2) AAAA Record: Resolve to IPv6 addresses

#### 3) CNAME Record: Resolve to another domain name

#### 4) MX Record: Resolve to addresses of servers that handle email for the domain we are querying

#### 5) PTR Record: Resolves from name to IP (Reverse DNS lookups)

#### 6) TXT Records: Any text-based data can be stored

#### 7) NS Record: Lists name servers for the zone

#### 8) SRV Records: Service records

#### 9) SoA: Start of Authority provides address of server authoritative for the zone

# Key Terms

### Resolver: A DNS client that sends DNS messages to obtain information about the requested domain name space

### Recursion: The action taken when a DNS server is asked to query behalf of a DNS resolver

### Authoritative Server: A DNS Server that responds to query messages with information stored in resource records for a domain name space stored on the server

### Recursive Resolver: A DNS server that recursively queries for the information asked in the DNS query

### FQDN: A Fully Qualified Domain Name is the absolute name of a device within the distributed DNS database

### RR: A Resource Record

### Zone: A database that contains information about the domain name space stored on an authoritative server

# DNS Attacks

### DNS Denial-of-Service (DoS) Attacks: An attacker delivers traffic to the victim by reflecting it off of a third party

### Query or Request Redirection: The DNS query is intercepted and modified in transit to the DNS server

### DNS Cache-Poisoning: Malicious data is injected into DNS servers

### Zone enumeration: Users use DNS diagnostic commands to learn about the websites architecture

### DNS Fast Flux: The ability to move distributed services to different computers quickly

### Taking over the Registration of a Domain: Change the authoritative DNS server
