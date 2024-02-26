# Ports and Protocols (Applications/Services)

### There are physical ports that you connect wires to and logical ports that determine where the data/traffic goes. 

#### 1) Physical ports: Physical ports are the ports on the routers, switches, servers, computers, etc. that you connect the wires, e.g., fiber optic cables, Cat5 cables, etc., to create a network.

#### 2) Logical ports: When a communication connection is established between two systems, it is done using ports. A logical port (also called a socket) is little more than an address number that both ends of the communication link agree to use when transferring data. Ports allow a single IP address to be able to support multiple simultaneous communications, each using a different port number. In the Application Layer of the TCP/IP model (which includes the Session, Presentation, and Application Layers of the OSI model) reside numerous application- or service-specific protocols. Data types are mapped using port numbers associated with services. For example, web traffic (or HTTP) is port 80. Secure web traffic (or HTTPS) is port 443. Table 5.4 highlights some of these protocols and their customary or assigned ports. You’ll note that in several cases a service (or protocol) may have two ports assigned, one secure and one insecure. When in doubt, systems should be implemented using the most secure version as possible of a protocol and its services.

##### 1) Well-known ports (0–1023): These ports are related to the common protocols that are at the core of the Transport Control Protocol/Internet Protocol (TCP/IP) model, Domain Name Service (DNS), Simple Mail Transfer Protocol (SMTP), etc.

##### 2) Registered ports (1024–49151): These ports are often associated with proprietary applications from vendors and developers. While they are officially approved by the Internet Assigned Numbers Authority (IANA), in practice many vendors simply implement a port of their choosing. Examples include Remote Authentication Dial-In User Service (RADIUS) authentication (1812), Microsoft SQL Server (1433/1434) and the Docker REST API (2375/2376).

##### 3) Dynamic or private ports (49152–65535): Whenever a service is requested that is associated with well-known or registered ports, those services will respond with a dynamic port that is used for that session and then released.

# Secure Ports

### Some network protocols transmit information in clear text, meaning it is not encrypted and should not be used. Clear text information is subject to network sniffing. This tactic uses software to inspect packets of data as they travel across the network and extract text such as usernames and passwords. Network sniffing could also reveal the content of documents and other files if they are sent via insecure protocols

### Examples:

#### 1) FTP port 21

#### 2) Telnet port 23

#### 3) SMTP port 25

#### 4) Time port 37

#### 5) DNS port 53

#### 6) HTTP port 80

#### 7) IMAP port 143

#### 8) SNMP port 161/162

#### 9) SMB port 445

#### 10) LDAP port 389

## Secure Alternatives:

#### 1) SFTP port 22

#### 2) SSH port 22

#### 3) SMTP port 587 (with TLS)

#### 4) NTP port 123

#### 5) DoT port 853 (DNS over TLS)

#### 6) HTTPS port 443

#### 7) IMAP port 993 IMAP for SSL/TLS

#### 8) SNMPv3 port 161/162

#### 9) NFS port 2049

#### 10) LDAPS port 636

