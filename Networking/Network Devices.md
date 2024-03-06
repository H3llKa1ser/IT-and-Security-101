# Network Devices

## Hubs (Layer 1)

### Cheap devices that send all data out all ports all the time. Network card examines the frame to determine the destination MAC address and removes the data from the network if the destination matches its own MAC.

### Sniffers attached to a network connected by hubs have access to all data all the time.

### ONE OF MANY REASONS WE NO LONGER USE HUBS

## Switches (Layer 2)

### Layer 2 device that uses MAC addresing to direct traffic for more efficient traffic control. A switch also isolates traffic into Collision domains.

### A sniffer plugged into a switch would have very little traffic to examine unless the port is set to port scan/mirroring. Broadcast traffic still is passed throughout the enite network.

### ** Bridges were predecessors to switches and operate at layer 2 **

## Routers (Layer 3)

### Layer 3 device that isolates traffic into separate networks (or subnetworks) so that broadcast traffic is isolated and is not passed from network to network.

### The router uses IP addressses to identify each network and to route between them. The biggest drawback to using a router is that is EXPENSIVE.
