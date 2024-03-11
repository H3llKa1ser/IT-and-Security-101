# Network Topologies

## Bus

### A LAN with central cable (bus) to which all nodes connect

### ADVANTAGES

#### 1) Adding Nodes

#### 2) Node failures don't affect the rest

### DISADVANTAGES

#### 1) Bus failure

## Tree

### All devices connect to a branching table

### ADVANTAGES

#### 1) Adding Nodes

#### 2) Node failures don't affect the rest

### DISADVANTAGES

#### 1) Cable failure

## Ring

### A closed loop topology. Data is transmitted in one direction only.

### ADVANTAGES

#### 1) Maximum wait time

#### 2) Can be used as LAN or Network backbone

### DISADVANTAGES

#### 1) Single Point of Failure

## Mesh

### All nodes are connected to every other node

### ADVANTAGES

#### 1) High level of redundancy

### DISADVANTAGES

#### 1) Very Expensive

## Star 

### All nodes are connected to a central device such as hub, switch or router

### ADVANTAGES

#### 1) Few cables

#### 2) Easy to deploy

#### 3) Nodes can easily be added or removed

### DISADVANTAGES

#### 1) The central piece is a single point of failure

# Topology Concepts

## Unicast, Multicast and Broadcast

### Unicast: Send a packet to one person

### Multicast: Send to selected people

### Broadcast: Send to everybody

## Circuit-Switched Network

### Dedicated Circuit between endpoints

### Endpoints have exclusive use of the circuit and bandwidth

### Example: Telephones

## Packet-Switched Network

### Do not use dedicated connections

### Packets are transmitted on a shared network

### Network devices find the best path

### All packets (eventually) need to be in the correct order

## Virtual Circuits

### Provides a connection between endpoints that acts as if it was a physical circuit

#### 1) Permament Virtual Circuit: The carrier configures the circuit's routes

#### 2) Switched Virtual Circuit: Configured dynamically by the routers

# Carrier Sense Multiple Access (CSMA)

### A protocol which uses the absense/presence of a signal on a medium as permission to speak

## 2 Variations:

#### 1) (CSMA/CA) Carrier Sense Multiple Access with Collision Avoidance: Requires devices to announce transmitting by using a jamming signal

#### 2) (CSMA/CD) Carrier Sense Multiple Access with Collision Detection: Listens for a carrier before transmitting data

### Token Passing: Only one device may transmit at a time. Devices can only transmit if they possess the token.

### Ethernet (IEEE 802.3): Played a major role of LANs in the 80s. Supports coaxial cable, unshielded twisted pair and fiber optics.

### Token Ring (IEEE 802.5): Each device gets data from its neighbor upstream and passes it downstream. Devices can only transmit when they have the ring.

### Fiber Distributed Data Interface (FDDI): Token passing architecture using two rings. Information flows in opposite directions.
