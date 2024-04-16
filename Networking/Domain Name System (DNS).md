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

#### 9) SoA Records: Start of Authority provides address of server authoritative for the zone

#### 10) CAA Record: Specifies which certificate authorities are allowed to issue SSL certificates for a domain

# DNS request and response process

### Here's a simplified example of a DNS request and response process:

1. **DNS Request**:
   - Suppose a user wants to access a website by typing its domain name into their web browser, for example, "www.example.com."
   - The user's device, typically a computer or smartphone, sends a DNS query to a DNS resolver (usually provided by the user's Internet Service Provider or ISP). This query asks the resolver to translate the domain name "www.example.com" into an IP address.

2. **DNS Resolution**:
   - The DNS resolver receives the query and checks its cache to see if it already has the corresponding IP address for "www.example.com." If it does, it returns the IP address to the user's device, and the process ends here.
   - If the resolver doesn't have the IP address in its cache, it acts as a client itself and sends a DNS query to the root name servers, asking for the IP address of the authoritative name servers responsible for the ".com" top-level domain.

3. **Root Name Servers**:
   - The root name servers respond to the resolver's query with the IP addresses of the name servers responsible for the ".com" top-level domain.

4. **Top-Level Domain (TLD) Name Servers**:
   - The resolver then sends a query to one of the name servers responsible for the ".com" TLD, asking for the IP address of the authoritative name servers for "example.com."

5. **Authoritative Name Servers**:
   - The ".com" name server responds with the IP addresses of the name servers authoritative for the "example.com" domain.
   - The resolver then sends a query directly to one of these authoritative name servers, asking for the IP address of "www.example.com."

6. **Final Response**:
   - The authoritative name server for "example.com" responds to the resolver's query with the IP address of "www.example.com."
   - The resolver caches this IP address for future use and sends it back to the user's device.
   - Now equipped with the IP address, the user's device can establish a connection to the web server hosting "www.example.com" and retrieve the requested web page.

### Throughout this process, various DNS servers communicate to resolve the domain name into its corresponding IP address, allowing the user's device to access the desired website.


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
