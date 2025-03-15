# Azure Virtual Network

Azure Virtual Network is a service that provides the fundamental building block for your private network in Azure. An instance of the service (a virtual network) enables many types of Azure resources to securely communicate with each other, the internet, and on-premises networks. These Azure resources include virtual machines (VMs).

A virtual network is similar to a traditional network that you'd operate in your own datacenter. But it brings extra benefits of the Azure infrastructure, such as scale, availability, and isolation.

## Why use an Azure virtual network?

Key scenarios that you can accomplish with a virtual network include:

1) Communication of Azure resources with the internet.

2) Communication between Azure resources.

3) Communication with on-premises resources.

4) Filtering of network traffic.

5) Routing of network traffic.

6) Integration with Azure services.

### Communicate with the internet

All resources in a virtual network can communicate outbound with the internet, by default. You can also use a public IP address, NAT gateway, or public load balancer to manage your outbound connections. You can communicate inbound with a resource by assigning a public IP address or a public load balancer.

When you're using only an internal standard load balancer, outbound connectivity is not available until you define how you want outbound connections to work with an instance-level public IP address or a public load balancer.

### Communicate between Azure resources

Azure resources communicate securely with each other in one of the following ways:

1) Virtual network: You can deploy VMs and other types of Azure resources in a virtual network. Examples of resources include App Service Environments, Azure Kubernetes Service (AKS), and Azure Virtual Machine Scale Sets.

2) Virtual network service endpoint: You can extend your virtual network's private address space and the identity of your virtual network to Azure service resources over a direct connection. Examples of resources include Azure Storage accounts and Azure SQL Database. Service endpoints allow you to secure your critical Azure service resources to only a virtual network.

3) Virtual network peering: You can connect virtual networks to each other by using virtual peering. The resources in either virtual network can then communicate with each other. The virtual networks that you connect can be in the same, or different, Azure regions.

### Communicate with on-premises resources

You can connect your on-premises computers and networks to a virtual network by using any of the following options:

1) Point-to-site virtual private network (VPN): Established between a virtual network and a single computer in your network. Each computer that wants to establish connectivity with a virtual network must configure its connection. This connection type is useful if you're just getting started with Azure, or for developers, because it requires few or no changes to an existing network. The communication between your computer and a virtual network is sent through an encrypted tunnel over the internet.

2) Site-to-site VPN: Established between your on-premises VPN device and an Azure VPN gateway that's deployed in a virtual network. This connection type enables any on-premises resource that you authorize to access a virtual network. The communication between your on-premises VPN device and an Azure VPN gateway is sent through an encrypted tunnel over the internet.

3) Azure ExpressRoute: Established between your network and Azure, through an ExpressRoute partner. This connection is private. Traffic doesn't go over the internet.

### Filter network traffic

You can filter network traffic between subnets by using either or both of the following options:

1) Network security groups: Network security groups and application security groups can contain multiple inbound and outbound security rules. These rules enable you to filter traffic to and from resources by source and destination IP address, port, and protocol.

2) Network virtual appliances: A network virtual appliance is a VM that performs a network function, such as a firewall or WAN optimization.

### Route network traffic

Azure routes traffic between subnets, connected virtual networks, on-premises networks, and the internet, by default. You can implement either or both of the following options to override the default routes that Azure creates:

1) Route tables: You can create custom route tables that control where traffic is routed to for each subnet.

2) Border gateway protocol (BGP) routes: If you connect your virtual network to your on-premises network by using an Azure VPN gateway or an ExpressRoute connection, you can propagate your on-premises BGP routes to your virtual networks.

### Integrate with Azure services

Integrating Azure services with an Azure virtual network enables private access to the service from virtual machines or compute resources in the virtual network. You can use the following options for this integration:

1) Deploy dedicated instances of the service into a virtual network. The services can then be privately accessed within the virtual network and from on-premises networks.

2) Use Azure Private Link to privately access a specific instance of the service from your virtual network and from on-premises networks.

3) Access the service over public endpoints by extending a virtual network to the service, through service endpoints. Service endpoints allow service resources to be secured to the virtual network.

## Limits

There are limits to the number of Azure resources that you can deploy. Most Azure networking limits are at the maximum values. However, you can increase certain networking limits.

## Virtual networks and availability zones

Virtual networks and subnets span all availability zones in a region. You don't need to divide them by availability zones to accommodate zonal resources. For example, if you configure a zonal VM, you don't have to take into consideration the virtual network when selecting the availability zone for the VM. The same is true for other zonal resources.

## Pricing

There's no charge for using Azure Virtual Network. It's free of cost. Standard charges apply for resources, such as VMs and other products. To learn more, see Virtual Network pricing and the Azure pricing calculator.

