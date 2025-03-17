# User-Defined Routes (UDRs)

You can create custom, or user-defined (static), routes in Azure to override Azure's default system routes, or to add more routes to a subnet's route table. In Azure, you create a route table, then associate the route table to zero or more virtual network subnets. Each subnet can have zero or one route table associated to it. To learn about the maximum number of routes you can add to a route table and the maximum number of user-defined route tables you can create per Azure subscription, see Azure limits. When you create a route table and associate it to a subnet, the table's routes are combined with the subnet's default routes. If there are conflicting route assignments, user-defined routes override the default routes.

You can specify the following next hop types when creating a user-defined route:

1) Virtual appliance: A virtual appliance is a virtual machine that typically runs a network application, such as a firewall. To learn about various preconfigured network virtual appliances you can deploy in a virtual network, see the Azure Marketplace. When you create a route with the virtual appliance hop type, you also specify a next hop IP address. The IP address can be:

The private IP address of a network interface attached to a virtual machine. Any network interface attached to a virtual machine that forwards network traffic to an address other than its own must have the Azure Enable IP forwarding option enabled for it. The setting disables Azure's check of the source and destination for a network interface. Learn more about how to enable IP forwarding for a network interface. Though Enable IP forwarding is an Azure setting, you may also need to enable IP forwarding within the virtual machine's operating system for the appliance to forward traffic between private IP addresses assigned to Azure network interfaces. If the appliance needs to route traffic to a public IP address, it must either proxy the traffic or perform network address translation (NAT) from the source's private IP address to its own private IP address. Azure then performs NAT to a public IP address before sending the traffic to the Internet. To determine required settings within the virtual machine, see the documentation for your operating system or network application. To understand outbound connections in Azure, see Understanding outbound connections.

The private IP address of an Azure internal load balancer. A load balancer is often used as part of a high availability strategy for network virtual appliances.

You can define a route with 0.0.0.0/0 as the address prefix and a next hop type of virtual appliance. This configuration allows the appliance to inspect the traffic and determine whether to forward or drop the traffic. If you intend to create a user-defined route that contains the 0.0.0.0/0 address prefix, read 0.0.0.0/0 address prefix first.

2) Virtual network gateway: Specify when you want traffic destined for specific address prefixes routed to a virtual network gateway. The virtual network gateway must be created with type VPN. You can't specify a virtual network gateway created as type ExpressRoute in a user-defined route because with ExpressRoute, you must use BGP for custom routes. You can't specify Virtual Network Gateways if you have VPN and ExpressRoute coexisting connections either. You can define a route that directs traffic destined for the 0.0.0.0/0 address prefix to a route-based virtual network gateway. On your premises, you might have a device that inspects the traffic and determines whether to forward or drop the traffic. If you intend to create a user-defined route for the 0.0.0.0/0 address prefix, read 0.0.0.0/0 address prefix first. Instead of configuring a user-defined route for the 0.0.0.0/0 address prefix, you can advertise a route with the 0.0.0.0/0 prefix via BGP, if you've enabled BGP for a VPN virtual network gateway.

3) None: Specify when you want to drop traffic to an address prefix, rather than forwarding the traffic to a destination. If you haven't fully configured a capability, Azure may list None for some of the optional system routes. For example, if you see None listed as the Next hop IP address with a Next hop type of Virtual network gateway or Virtual appliance, it may be because the device isn't running, or isn't fully configured. Azure creates system default routes for reserved address prefixes with None as the next hop type.

4) Virtual network: Specify the Virtual network option when you want to override the default routing within a virtual network.

5) Internet: Specify the Internet option when you want to explicitly route traffic destined to an address prefix to the Internet, or if you want traffic destined for Azure services with public IP addresses kept within the Azure backbone network. See Routing example, for an example of why you might create a route with the Virtual network hop type.

You can't specify Virtual network peering or VirtualNetworkServiceEndpoint as the next hop type in user-defined routes. Routes with the Virtual network peering or VirtualNetworkServiceEndpoint next hop types are only created by Azure, when you configure a virtual network peering, or a service endpoint.

## Service Tags for user-defined routes

You can now specify a service tag as the address prefix for a user-defined route instead of an explicit IP range. A service tag represents a group of IP address prefixes from a given Azure service. Microsoft manages the address prefixes encompassed by the service tag and automatically updates the service tag as addresses change. Thus minimizing the complexity of frequent updates to user-defined routes and reducing the number of routes you need to create. You can currently create 25 or less routes with service tags in each route table. With this release, using service tags in routing scenarios for containers is also supported.

## Exact Match

The system gives preference to the route with the explicit prefix when there's an exact prefix match between a route with an explicit IP prefix and a route with a Service Tag. When multiple routes with Service Tags have matching IP prefixes, routes are evaluated in the following order:

1) Regional tags (for example, Storage.EastUS, AppService.AustraliaCentral)

2) Top level tags (for example, Storage, AppService)

3) AzureCloud regional tags (for example, AzureCloud.canadacentral, AzureCloud.eastasia)

4) The AzureCloud tag

To use this feature, specify a Service Tag name for the address prefix parameter in route table commands. For example, in PowerShell you can create a new route to direct traffic sent to an Azure Storage IP prefix to a virtual appliance by using:

    $param = @{ Name = 'StorageRoute' AddressPrefix = 'Storage' NextHopType = 'VirtualAppliance' NextHopIpAddress = '10.0.100.4' } New-AzRouteConfig @param

The same command for the Azure CLI is:

    az network route-table route create \ --resource-group MyResourceGroup \ --route-table-name MyRouteTable \ --name StorageRoute \ --address-prefix Storage \ --next-hop-type VirtualAppliance \ --next-hop-ip-address 10.0.100.4

## Next hop types across Azure tools

The name displayed and referenced for next hop types is different between the Azure portal and command-line tools, and the Resource Manager and classic deployment models. The following table lists the names used to refer to each next hop type with the different tools and deployment models.

| Next Hop Type                      | Azure CLI and PowerShell (Resource Manager) | Azure Classic CLI and PowerShell (Classic) |
|------------------------------------|--------------------------------------------|--------------------------------------------|
| Virtual network gateway            | VirtualNetworkGateway                      | VPNGateway                                |
| Virtual network                    | VNetLocal                                  | VNETLocal (not available in classic CLI)  |
| Internet                           | Internet                                   | Internet (not available in classic CLI)   |
| Virtual appliance                   | VirtualAppliance                           | VirtualAppliance                          |
| None                               | None                                      | Null (not available in classic CLI)       |
| Virtual network peering             | Virtual network peering                    | Not applicable                            |
| Virtual network service endpoint    | VirtualNetworkServiceEndpoint              | Not applicable                            |

## Border gateway protocol (BGP)

An on-premises network gateway can exchange routes with an Azure virtual network gateway by using the BGP. Using BGP with an Azure virtual network gateway is dependent on the type you selected when you created the gateway:

1) ExpressRoute: You must use BGP to advertise on-premises routes to the Microsoft Edge router. You can't create UDRs to force traffic to the ExpressRoute virtual network gateway if you deploy a virtual network gateway deployed as the type ExpressRoute. You can use UDRs for forcing traffic from the express route to, for example, a network virtual appliance.

2) VPN: Optionally, you can use BGP. For more information, see BGP with site-to-site VPN connections.

When you exchange routes with Azure by using BGP, a separate route is added to the route table of all subnets in a virtual network for each advertised prefix. The route is added with Virtual network gateway listed as the source and next hop type.

You can disable ExpressRoute and Azure VPN Gateway route propagation on a subnet by using a property on a route table. When you disable route propagation, the system doesn't add routes to the route table of all subnets with virtual network gateway route propagation disabled. This process applies to both static routes and BGP routes. Connectivity with VPN connections is achieved by using custom routes with a next hop type of Virtual network gateway. For more information, see Disable virtual network gateway route propagation.

#### NOTE: Route propagation shouldn't be disabled on GatewaySubnet. The gateway won't function if this setting is disabled.

## How Azure selects a route

When outbound traffic is sent from a subnet, Azure selects a route based on the destination IP address by using the longest prefix match algorithm. For example, a route table has two routes. One route specifies the 10.0.0.0/24 address prefix, and the other route specifies the 10.0.0.0/16 address prefix.

Azure directs traffic destined for 10.0.0.5 to the next hop type specified in the route with the 10.0.0.0/24 address prefix. This process occurs because 10.0.0.0/24 is a longer prefix than 10.0.0.0/16, even though 10.0.0.5 falls within both address prefixes.

Azure directs traffic destined for 10.0.1.5 to the next hop type specified in the route with the 10.0.0.0/16 address prefix. This process occurs because 10.0.1.5 isn't included in the 10.0.0.0/24 address prefix, which makes the route with the 10.0.0.0/16 address prefix the longest matching prefix.

If multiple routes contain the same address prefix, Azure selects the route type based on the following priority:

1) User-defined route

2) BGP route

3) System route

#### NOTE:  System routes for traffic related to virtual network, virtual network peerings, or virtual network service endpoints are preferred routes. They're preferred, even if BGP routes are more specific. Routes with a virtual network service endpoint as the next hop type can't be overridden, even when you use a route table.

When traffic is destined for an IP address outside the address prefixes of any other routes in the route table, Azure selects the route with the User source. Azure makes this choice because UDRs are a higher priority than system default routes.

## 0.0.0.0/0 address prefix

A route with the 0.0.0.0/0 address prefix gives instructions to Azure. Azure uses these instructions to route traffic destined for an IP address that doesn't fall within the address prefix of any other route in a subnet's route table. When a subnet is created, Azure creates a default route to the 0.0.0.0/0 address prefix, with the Internet next hop type. If you don't override this route, Azure routes all traffic destined to IP addresses not included in the address prefix of any other route to the internet.

The exception is that traffic to the public IP addresses of Azure services remains on the Azure backbone network and isn't routed to the internet. When you override this route with a custom route, traffic destined for addresses not within the address prefixes of any other route in the route table is directed. The destination depends on whether you specify a network virtual appliance or virtual network gateway in the custom route.

When you override the 0.0.0.0/0 address prefix, outbound traffic from the subnet flows through the virtual network gateway or virtual appliance. The following changes also occur with Azure default routing:

1) Azure sends all traffic to the next hop type specified in the route, including traffic destined for public IP addresses of Azure services.

When the next hop type for the route with the 0.0.0.0/0 address prefix is Internet, traffic from the subnet destined to the public IP addresses of Azure services never leaves the Azure backbone network, regardless of the Azure region in which the virtual network or Azure service resource exist.

When you create a UDR or a BGP route with a Virtual network gateway or Virtual appliance next hop type, all traffic is sent to the next hop type specified in the route. This includes traffic sent to public IP addresses of Azure services for which you haven't enabled service endpoints.

When you enable a service endpoint for a service, Azure creates a route with address prefixes for the service. Traffic to the service doesn't route to the next hop type in a route with the 0.0.0.0/0 address prefix. The address prefixes for the service are longer than 0.0.0.0/0.

2) You can no longer directly access resources in the subnet from the internet. You can access resources in the subnet from the internet indirectly. The device specified by the next hop type for a route with the 0.0.0.0/0 address prefix must process inbound traffic. After the traffic traverses the device, the traffic reaches the resource in the virtual network. If the route contains the following values for the next hop type:

Virtual appliance: The appliance must:

Be accessible from the internet.
Have a public IP address assigned to it.
Not have a network security group rule associated to it that prevents communication to the device.
Not deny the communication.
Be able to network address translate and forward, or proxy the traffic to the destination resource in the subnet and return the traffic back to the internet.

Virtual network gateway: If the gateway is an ExpressRoute virtual network gateway, an internet-connected device on-premises can network address translate and forward, or proxy the traffic to the destination resource in the subnet, via ExpressRoute private peering.

If your virtual network is connected to an Azure VPN gateway, don't associate a route table to the gateway subnet that includes a route with a destination of 0.0.0.0/0. Doing so can prevent the gateway from functioning properly. For more information, see Why are certain ports opened on my VPN gateway?.

# Diagram


![image](https://github.com/user-attachments/assets/80ac5018-6bdb-4788-af35-e10f8a9dcf47)
