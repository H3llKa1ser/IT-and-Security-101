# Azure Application Gateway

Azure Application Gateway is a web traffic (OSI layer 7) load balancer that enables you to manage traffic to your web applications. Traditional load balancers operate at the transport layer (OSI layer 4 - TCP and UDP) and route traffic based on source IP address and port, to a destination IP address and port.

Application Gateway can make routing decisions based on additional attributes of an HTTP request, for example URI path or host headers. For example, you can route traffic based on the incoming URL. So if /images is in the incoming URL, you can route traffic to a specific set of servers (known as a pool) configured for images. If /video is in the URL, that traffic is routed to another pool that's optimized for videos.

![image](https://github.com/user-attachments/assets/74efa097-f3aa-42d9-a102-b9498058f390)

This type of routing is known as application layer (OSI layer 7) load balancing. Azure Application Gateway can do URL-based routing and more.

## Application gateway components

An application gateway serves as the single point of contact for clients. It distributes incoming application traffic across multiple backend pools, which include Azure VMs, virtual machine scale sets, Azure App Service, and on-premises/external servers.

![image](https://github.com/user-attachments/assets/f93931e5-beae-4ad4-98b4-320b4ce2c474)

## Infrastructure

The Application Gateway infrastructure includes the virtual network, subnets, network security groups, and user defined routes.

## Frontend IP address

You can configure the application gateway to have a public IP address, a private IP address, or both. A public IP is required when you host a back end that clients must access over the Internet via an Internet-facing virtual IP (VIP).

A public IP address isn't required for an internal endpoint that's not exposed to the internet. A private frontend configuration is useful for internal line-of-business applications that aren't exposed to the internet. It's also useful for services and tiers in a multitier application within a security boundary that aren't exposed to the internet but that require round-robin load distribution, session stickiness, or TLS termination.

Only one public IP address and one private IP address are supported. You choose the frontend IP when you create the application gateway.

#### NOTE: The Application Gateway front end supports dual-stack IP addresses (public preview). You can create up to four frontend IPs. Two are IPv4 addresses (public and private) and two are IPv6 addresses (public and private).

For a public IP address, you can create a new public IP address or use an existing public IP in the same location as the application gateway. For more information, see Static versus dynamic public IP address.

For a private IP address, you can specify a private IP address from the subnet where the application gateway is created. For Application Gateway v2 SKU deployments, a static IP address must be defined when you add a private IP address to the gateway. For Application Gateway v1 SKU deployments, if you don't specify an IP address, an available IP address is automatically selected from the subnet. The IP address type that you select (static or dynamic) can't be changed later.

A frontend IP address is associated to a listener, which checks for incoming requests on the frontend IP.

You can create private and public listeners with the same port number. However, be aware of any network security group (NSG) associated with the Application Gateway subnet. Depending on your NSG's configuration, you might need an allow-inbound rule with Destination IP addresses as your application gateway's public and private frontend IPs. When you use the same port, your application gateway changes the Destination of the inbound flow to the frontend IPs of your gateway.

Inbound rule:

1) Source: According to your requirement

2) Destination: Public and private frontend IPs of your application gateway.

3) Destination port: According to configured listeners

4) Protocol: TCP

Outbound rule: No specific requirement

## Listeners

A listener is a logical entity that checks for incoming connection requests by using the port, protocol, host, and IP address. When you configure the listener, you must enter values for these that match the corresponding values in the incoming request on the gateway.

When you create an application gateway by using the Azure portal, you also create a default listener by choosing the protocol and port for the listener. You can choose whether to enable HTTP2 support on the listener. After you create the application gateway, you can edit the settings of that default listener (appGatewayHttpListener) or create new listeners.

### Listener Type

A listener is a logical entity that checks for incoming connection requests. A listener accepts a request if the protocol, port, hostname, and IP address associated with the request match the same elements associated with the listener configuration.

Before you use an application gateway, you must add at least one listener. There can be multiple listeners attached to an application gateway, and they can be used for the same protocol.

After a listener detects incoming requests from clients, the application gateway routes these requests to members in the backend pool configured in the rule.

Listeners support the following ports and protocols.

## Ports

A port is where a listener listens for the client request. You can configure ports for v1 and v2 SKUs as per below.

| SKU | Supported Port Range | Exception(s) |
|----|----------------------|-------------|
| V2 | 1 to 64999          | 22          |
| V1 | 1 to 65502          | 3389        |

## Protocols

Application Gateway supports four protocols: HTTP, HTTPS, HTTP/2, and WebSocket:

#### NOTE: HTTP/2 protocol support is available to clients connecting to application gateway listeners only. The communication to backend server pools is always over HTTP/1.1. By default, HTTP/2 support is disabled. You can choose to enable it.

Specify between the HTTP and HTTPS protocols in the listener configuration.

Support for WebSockets and HTTP/2 protocols is provided natively, and WebSocket support is enabled by default. There's no user-configurable setting to selectively enable or disable WebSocket support. Use WebSockets with both HTTP and HTTPS listeners.

Use an HTTPS listener for TLS termination. An HTTPS listener offloads the encryption and decryption work to your application gateway, so your web servers aren't burdened by the overhead.
