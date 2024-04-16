# Subnetting

### Subnetting is the process of dividing a single, large network into smaller sub-networks, known as subnets. This practice helps in efficiently utilizing the available IP addresses and managing network traffic more effectively.

### In IPv4 networking, IP addresses are divided into two parts: the network portion and the host portion. Subnetting involves borrowing bits from the host portion to create subnets, allowing for the creation of multiple smaller networks within a larger one. This process enables better organization, security, and management of network resources.

### Subnetting is typically performed by manipulating the subnet mask associated with an IP address. The subnet mask determines which portion of the IP address is used for the network and which portion is used for hosts within that network.

#### For example, if you have the IP address 192.168.1.0 with a subnet mask of 255.255.255.0 (which is commonly expressed as /24 in CIDR notation), it means that the first 24 bits are used for the network, and the remaining 8 bits are used for hosts. By adjusting the subnet mask, you can create smaller subnets with fewer host addresses or larger subnets with more host addresses, depending on your network requirements.

### Subnetting is an essential skill for network administrators and engineers as it allows them to design and manage complex networks efficiently.

# Subnet Mask

### A subnet mask is a 32-bit number used in conjunction with an IP address to identify which part of the address represents the network portion and which part represents the host portion. It's essentially a binary pattern that divides an IP address into network and host portions.

### In IPv4 networking, the subnet mask consists of four octets, each represented in decimal format (e.g., 255.255.255.0) or in binary format (e.g., 11111111.11111111.11111111.00000000). The subnet mask is applied bitwise to the IP address. Wherever there's a "1" in the subnet mask, the corresponding bit in the IP address is considered part of the network address. Wherever there's a "0" in the subnet mask, the corresponding bit in the IP address is considered part of the host address.

#### For example, consider the IP address 192.168.1.100 with a subnet mask of 255.255.255.0. Applying the subnet mask bitwise, we can see that the first 24 bits are used for the network address (192.168.1) and the last 8 bits are used for host addressing (the ".100" in this case).

### Subnet masks can vary in length, allowing for the creation of smaller or larger subnets. Longer subnet masks (e.g., 255.255.255.128 or /25 in CIDR notation) create smaller subnets with fewer available host addresses, while shorter subnet masks (e.g., 255.255.255.0 or /24 in CIDR notation) create larger subnets with more available host addresses.

### Understanding subnet masks is crucial for subnetting, which is the process of dividing a network into smaller subnets to improve efficiency and manageability.

