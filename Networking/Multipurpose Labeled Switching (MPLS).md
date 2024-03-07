# Multipurpose Labeled Switching (MPLS)

## Label Edge Router (LER)

### A label edge router (LER, also known as edge LSR or "ingress node") is a router that operates at the edge of an MPLS network and acts as the entry and exit points for the network. These edge router places an MPLS label on an incoming packet and sends it forward into the MPLS domain. The same job is performed upon receiving a labeled packet which is destined to exit the MPLS domain, the LER removes the label and forwards the IP packet using normal IP address.

## Provider Router

### In an MPLS based virtual private network (VPN) environment, LERs that function as ingress and/or egress routers to the VPN are often called Provider Edge (PE) routers. Devices that function only as transit routers are similarly called Provider (P) routers. The job of a provider router is significantly easier than that of a Provider Edge router, so they can be less complex and may be more dependable because of this.

## Label Distribution Protocol (LDP)

### Labels are distributed between LERs and LSRs using the Label Distribution Protocol (LDP). LSRs in an MPLS network regularly exchange label and reachability information with each other using standardized procedures in order to build a complete picture of the network they can then use to forward packets. CE is the "Customer Edge", the customer device or router a PE router talks.
