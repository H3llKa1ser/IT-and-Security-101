# Virtual network connection types

A virtual network is a virtual, isolated portion of the Azure public network. By default, traffic cannot be routed between two virtual networks. However, it's possible to connect virtual networks, either within a single region or across two regions, so that traffic can be routed between them.

# Virtual Network Peering

Virtual network peering. Virtual network peering connects two Azure virtual networks. Once peered, the virtual networks appear as one for connectivity purposes. Traffic between virtual machines in the peered virtual networks is routed through the Microsoft backbone infrastructure, through private IP addresses only. No public internet is involved. You can also peer virtual networks across Azure regions (global peering).

VPN gateways. A VPN gateway is a specific type of virtual network gateway that is used to send traffic between an Azure virtual network and an on-premises location over the public internet. You can also use a VPN gateway to send traffic between Azure virtual networks. Each virtual network can have at most one VPN gateway. You should enable Azure Distributed denial of service (DDoS) Protection Standard on any perimeter virtual network.

Virtual network peering provides a low-latency, high-bandwidth connection. There is no gateway in the path, so there are no extra hops, ensuring low latency connections. It's useful in scenarios such as cross-region data replication and database failover. Because traffic is private and remains on the Microsoft backbone, also consider virtual network peering if you have strict data policies and want to avoid sending any traffic over the internet.

VPN gateways provide a limited bandwidth connection and are useful in scenarios where you need encryption but can tolerate bandwidth restrictions. In these scenarios, customers are also not as latency-sensitive.

# Gateway Transit

Virtual network peering and VPN Gateways can also coexist via gateway transit.

Gateway transit enables you to use a peered virtual network's gateway for connecting to on-premises, instead of creating a new gateway for connectivity. As you increase your workloads in Azure, you need to scale your networks across regions and virtual networks to keep up with the growth. Gateway transit allows you to share an ExpressRoute or VPN gateway with all peered virtual networks and lets you manage the connectivity in one place. Sharing enables cost-savings and reduction in management overhead.

With gateway transit enabled on virtual network peering, you can create a transit virtual network that contains your VPN gateway, Network Virtual Appliance, and other shared services. As your organization grows with new applications or business units and as you spin up new virtual networks, you can connect to your transit virtual network using peering. This prevents adding complexity to your network and reduces management overhead of managing multiple gateways and other appliances.

## Configuring connections

Virtual network peering and VPN gateways both support the following connection types:

1) Virtual networks in different regions.

2) Virtual networks in different Microsoft Entra tenants.

3) Virtual networks in different Azure subscriptions.

4) Virtual networks that use a mix of Azure deployment models (Resource Manager and classic).

## Comparison of virtual network peering and VPN Gateway

| Item                     | Virtual network peering                                      | VPN Gateway                                                   |
|--------------------------|------------------------------------------------------------|--------------------------------------------------------------|
| **Limits**               | Up to 500 virtual network peerings per virtual network    | One VPN gateway per virtual network. The maximum number of tunnels per gateway depends on the gateway SKU. |
| **Pricing model**        | Ingress/Egress                                            | Hourly + Egress                                              |
| **Encryption**           | Software-level encryption is recommended.                 | Custom IPsec/IKE policy can be applied to new or existing connections. |
| **Bandwidth limitations** | No bandwidth limitations.                                | Varies based on SKU.                                         |
| **Private?**            | Yes. Routed through Microsoft backbone and private. No public internet involved. | Public IP involved, but routed through Microsoft backbone if Microsoft global network is enabled. |
| **Transitive relationship** | Peering connections are non-transitive. Transitive networking can be achieved using NVAs or gateways in the hub virtual network. | If virtual networks are connected via VPN gateways and BGP is enabled in the virtual network connections, transitivity works. |
| **Initial setup time**   | Fast                                                      | ~30 minutes                                                  |
| **Typical scenarios**    | Data replication, database failover, and other scenarios needing frequent backups of large data. | Encryption-specific scenarios that are not latency sensitive and do not need high throughput. |


