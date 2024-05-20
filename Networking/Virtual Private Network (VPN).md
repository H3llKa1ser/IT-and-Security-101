# Virtual Private Network (VPN)

### A virtual private network (VPN) is not necessarily an encrypted tunnel. It is simply a point-to-point connection between two hosts that allows them to communicate. Secure communications can, of course, be provided by the VPN, but only if the security protocols have been selected and correctly configured to provide a trusted path over an untrusted network, such as the internet. Remote users employ VPNs to access their organization’s network, and depending on the VPN’s implementation, they may have most of the same resources available to them as if they were physically at the office. As an alternative to expensive dedicated point-to-point connections, organizations use gateway-to-gateway VPNs to securely transmit information over the internet between sites or even with business partners. 

### The two most common protocols used to establish VPN connections are:

#### 1) IPSec

#### 2) SSL/TLS

### IPsec’s ESP is a perfect protocol for setting up secure tunnels between different networks or a computer and a network. ESP can provide security and integrity of all data transmitted between two points; moreover, even the IP address can be hidden in tunnel mode. Note that the system must be behind a VPN concentrator for the IP address to be hidden. Cisco VPN systems offer IPsec.

### Although SSL was created to secure HTTP traffic, SSL/TLS has found its way to establish secure VPN connections with OpenVPN. Using various tools and libraries built around TLS, OpenVPN offers different authentication and encryption mechanisms to establish VPN connections.

### Some older protocols that can be used to establish VPN connections are no longer considered secure. One example is Point to Point Tunneling Protocol (PPTP), which is no longer considered secure.
