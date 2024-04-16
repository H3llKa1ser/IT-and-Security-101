# Dynamic Host Configuration Protocol (DHCP)

### Automatically assigns IP addresses to workstations

### The address given is leased for a period of time

### Address lease is referred to as a TTL (Time to Live)

## Detailed Definition

### DHCP stands for Dynamic Host Configuration Protocol. It's a network management protocol used to dynamically assign IP addresses and other network configuration parameters to devices on a network. DHCP simplifies the process of configuring network settings by automating the assignment of IP addresses, subnet masks, default gateways, DNS servers, and other parameters.

### Here's how DHCP typically works:

1. **DHCP Server**: A DHCP server is a device (often a router or a dedicated server) on the network that is configured to provide IP addresses and other network configuration information to DHCP clients.

2. **DHCP Client**: A DHCP client is any device on the network that needs an IP address and other network settings to communicate. This could be a computer, smartphone, printer, or any other network-enabled device.

3. **IP Address Lease**: When a DHCP client connects to the network, it sends out a DHCP request broadcast message to discover DHCP servers available on the network. DHCP servers respond with DHCP offer messages, each containing an IP address lease along with other configuration parameters.

4. **IP Address Assignment**: The DHCP client selects one of the offered IP addresses and sends a DHCP request message to the chosen DHCP server, requesting to lease that IP address. If the DHCP server accepts the request, it sends a DHCP acknowledgment (ACK) message to the client, confirming the lease and providing the IP address and other configuration settings.

5. **Lease Renewal**: DHCP leases are not permanent; they have a finite duration. DHCP clients must periodically renew their leases to maintain their network connectivity. If a lease expires without renewal, the IP address is returned to the DHCP server's pool of available addresses and can be assigned to another client.

### By automating the process of IP address assignment and configuration, DHCP greatly simplifies network administration tasks. It eliminates the need for manual IP address assignment, reduces the likelihood of conflicts, and allows for more efficient use of IP addresses within a network. DHCP is widely used in both small home networks and large enterprise environments.

