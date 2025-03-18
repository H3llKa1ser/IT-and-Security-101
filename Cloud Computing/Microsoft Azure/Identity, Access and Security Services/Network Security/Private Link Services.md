# Private Link Services

Azure Private Link service is the reference to your own service that is powered by Azure Private Link. Your service that is running behind Azure Standard Load Balancer can be enabled for Private Link access so that consumers to your service can access it privately from their own VNets. Your customers can create a private endpoint inside their virtual network and map it to this service. This example explains concepts related to the service provider side.

![image](https://github.com/user-attachments/assets/8399813d-bca5-4029-a885-0a8a67c2696a)

## Workflow

![image](https://github.com/user-attachments/assets/5da49477-3b31-4bd7-b131-8e0026bbab34)

## Create your Private Link Service

Configure your application to run behind a standard load balancer in your virtual network. If you already have your application configured behind a standard load balancer, you can skip this step.

Create a Private Link Service referencing the load balancer above. In the load balancer selection process, choose the frontend IP configuration where you want to receive the traffic. Choose a subnet for NAT IP addresses for the Private Link Service. It's recommended to have at least eight NAT IP addresses available in the subnet. All consumer traffic will appear to originate from this pool of private IP addresses to the service provider. Choose the appropriate properties/settings for the Private Link Service.

## Share your service

After you create a Private Link service, Azure will generate a globally unique named moniker called alias based on the name you provide for your service. You can share either the alias or resource URI of your service with your customers offline. Consumers can start a Private Link connection using the alias or the resource URI.

## Manage your connection requests

After a consumer initiates a connection, the service provider can accept or reject the connection request. All connection requests will be listed under the privateendpointconnections property on the Private Link service.

## Delete your service

If the Private Link service is no longer in use, you can delete it. However, before you delete the service, ensure that there are no private endpoint connections associated with it. You can reject all connections and delete the service.

## Details

Private Link service can be accessed from approved private endpoints in any public region. The private endpoint can be reached from the same virtual network and regionally peered virtual networks. The private endpoint can be reached from globally peered virtual networks and on premises using private VPN or ExpressRoute connections.

Upon creation of a Private Link Service, a network interface is created for the lifecycle of the resource. This interface isn't manageable by the customer.

The Private Link Service must be deployed in the same region as the virtual network and the Standard Load Balancer.

A single Private Link Service can be accessed from multiple Private Endpoints belonging to different virtual networks, subscriptions and/or Active Directory tenants. The connection is established through a connection workflow.

Multiple Private Link services can be created on the same Standard Load Balancer using different front-end IP configurations. There are limits to the number of Private Link services you can create per Standard Load Balancer and per subscription. For details, see Azure limits.

Private Link service can have more than one NAT IP configurations linked to it. Choosing more than one NAT IP configurations can help service providers to scale. Today, service providers can assign up to eight NAT IP addresses per Private Link service. With each NAT IP address, you can assign more ports for your TCP connections and thus scale out. After you add multiple NAT IP addresses to a Private Link service, you can't delete the NAT IP addresses. This restriction is in place to ensure that active connections aren't impacted while deleting the NAT IP addresses.

## Alias

Alias is a globally unique name for your service. It helps you mask the customer data for your service and at the same time creates an easy-to-share name for your service. When you create a Private Link service, Azure generates an alias for your service that you can share with your customers. Your customers can use this alias to request a connection to your service.

The alias is composed of three parts: Prefix.GUID.Suffix

Prefix is the service name. You can pick your own prefix. After "Alias" is created, you can't change it, so select your prefix appropriately.
GUID will be provided by platform. This GUID (globally unique identifier) makes the name globally unique.
Suffix is appended by Azure: region.azure.privatelinkservice
Complete alias: Prefix. {GUID}.region.azure.privatelinkservice

## Control service exposure

The Private Link service provides you with three options in the Visibility setting to control the exposure of your service. Your visibility setting determines whether a consumer can connect to your service. Here are the visibility setting options, from most restrictive to least restrictive:

1) Role-based access control only: If your service is for private consumption from different virtual networks that you own, use role-based access control inside subscriptions that are associated with the same Active Directory tenant. Cross tenant visibility is permitted through role-based access control.

2) Restricted by subscription: If your service will be consumed across different tenants, you can restrict the exposure to a limited set of subscriptions that you trust. Authorizations can be pre-approved.

3) Anyone with your alias: If you want to make your service public and allow anyone with your Private Link service alias to request a connection, select this option.

## Control service access

Consumers having exposure controlled by visibility setting to your Private Link service can create a private endpoint in their virtual networks and request a connection to your Private Link service. The private endpoint connection will be created in a Pending state on the Private Link service object. The service provider is responsible for acting on the connection request. You can either approve the connection, reject the connection, or delete the connection. Only connections that are approved can send traffic to the Private Link service.

The action of approving the connections can be automated by using the auto-approval property on the Private Link service. Auto-Approval is an ability for service providers to preapprove a set of subscriptions for automated access to their service. Customers will need to share their subscriptions offline for service providers to add to the auto-approval list. Auto-approval is a subset of the visibility array.

Visibility controls the exposure settings whereas auto-approval controls the approval settings for your service. If a customer requests a connection from a subscription in the auto-approval list, the connection is automatically approved, and the connection is established. Service providers don’t need to manually approve the request. If a customer requests a connection from a subscription in the visibility array and not in the auto-approval array, the request will reach the service provider. The service provider must manually approve the connections.

## Getting connection Information using TCP Proxy v2

In the private link service, the source IP address of the packets coming from private endpoint is network address translated (NAT) on the service provider side using the NAT IP allocated from the provider's virtual network. The applications receive the allocated NAT IP address instead of actual source IP address of the service consumers. If your application needs an actual source IP address from the consumer side, you can enable proxy protocol on your service and retrieve the information from the proxy protocol header. In addition to source IP address, proxy protocol header also carries the LinkID of the private endpoint. Combination of source IP address and LinkID can help service providers uniquely identify their consumers.

This information is encoded using a custom Type-Length-Value (TLV) vector

#### NOTE: The service provider is responsible for making sure that the service behind the standard load balancer is configured to parse the proxy protocol header as per the specification when proxy protocol is enabled on private link service. The request will fail if proxy protocol setting is enabled on private link service but the service provider's service is not configured to parse the header. The request will fail if the service provider's service is expecting a proxy protocol header while the setting is not enabled on the private link service. Once proxy protocol setting is enabled, proxy protocol header will also be included in HTTP/TCP health probes from host to the backend virtual machines. Client information isn't contained in the header.

The matching LINKID that is part of the PROXYv2 (TLV) protocol can be found at the PrivateEndpointConnectionas property linkIdentifier.

## Limitations

The following are the known limitations when using the Private Link service:

Supported only on Standard Load Balancer. Not supported on Basic Load Balancer.
Supported only on Standard Load Balancer where backend pool is configured by NIC. Not supported on Standard Load Balancer where backend pool is configured by IP address.
Supports IPv4 traffic only
Supports TCP and UDP traffic only
Private Link Service has an idle timeout of ~5 minutes (300 seconds). To avoid hitting this limit, applications connecting through Private Link Service must use TCP Keepalives lower than that time.

