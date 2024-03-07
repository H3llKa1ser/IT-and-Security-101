# Generic Routing Encapsulation (GRE)

## Point to point link between two networks. It adds an extra IP header to the original packet. Much more frequently used in the past to encapsulate AppleTalk, IPX and other protocols.

### 1) Data encapsulation: GRE tunnels encapsulate packets that allow protocols to traverse an incompatible network.

### For example, to route IPv4 packets across a network that only uses IPv6.

### 2) Simplicity: GRE tunnels lack mechanisms related to flow control and securoty by default. This lack of features can ease the configuration process. 

### However, you probably don;t want to transfer data in an unencrypted form across a public network, thereefore, GRE tunnels can be supplemented by the IPSec suite of protocols for security purposes.

### In addition, GRE tunnels can forward data from non-contiguous networks through a single tunnel, which is something VPNs cannot do.

### 3) Multicast Traffic Forwarding: GRE tunnels can be used to forward multicast traffic whereas a VPN cannot. Because of this, multicast traffic such as advertisements sent by routing protocols can be easily transfered between remote sites when using a GRE tunnel.
