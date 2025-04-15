# Network Security Groups (NSGs)

You can use an Azure network security group to filter network traffic between Azure resources in an Azure virtual network. A network security group contains security rules that allow or deny inbound network traffic to, or outbound network traffic from, several types of Azure resources. For each rule, you can specify source and destination, port, and protocol.

This article describes the properties of a network security group rule, the default security rules that are applied, and the rule properties that you can modify to create an augmented security rule.

## Security rules

A network security group contains zero, or as many rules as desired, within Azure subscription limits. Each rule specifies the following properties:

| **Property**           | **Explanation** |
|------------------------|-----------------|
| **Name**               | A unique name within the network security group. The name can be up to 80 characters long. |
| **Priority**           | A number between 100 and 4096. Rules are processed in priority order, with lower numbers processed first. Once traffic matches a rule, processing stops. |
| **Source or destination** | Can be "Any", or a specific IP address, CIDR block (e.g., 10.0.0.0/24), service tag, or application security group. Use private IPs for Azure resources. Augmented rules (multiple IPs/ranges) are only supported in NSGs created via Resource Manager. |
| **Protocol**           | TCP, UDP, ICMP, ESP, AH, or Any. ESP and AH must be configured via ARM templates. |
| **Direction**          | Indicates if the rule applies to **inbound** or **outbound** traffic. |
| **Port range**         | Can be a single port or a range (e.g., 80 or 10000–10005). Only NSGs via Resource Manager support multiple ports or ranges per rule. |
| **Action**             | Either **Allow** or **Deny**. |

Security rules are evaluated and applied based on the five-tuple (source, source port, destination, destination port, and protocol) information. You can't create two security rules with the same priority and direction. A flow record is created for existing connections. Communication is allowed or denied based on the connection state of the flow record. The flow record allows a network security group to be stateful. If you specify an outbound security rule to any address over port 80, for example, it's not necessary to specify an inbound security rule for the response to the outbound traffic. You only need to specify an inbound security rule if communication is initiated externally. The opposite is also true. If inbound traffic is allowed over a port, it's not necessary to specify an outbound security rule to respond to traffic over the port.

Existing connections may not be interrupted when you remove a security rule that enabled the flow. Traffic flows are interrupted when connections are stopped and no traffic is flowing in either direction, for at least a few minutes.

Modifying network security group rules will only affect the new connections that are formed. When a new rule is created or an existing rule is updated in a network security group, it will only apply to new flows and new connections. Existing workflow connections aren't updated with the new rules.

There are limits to the number of security rules you can create in a network security group.

