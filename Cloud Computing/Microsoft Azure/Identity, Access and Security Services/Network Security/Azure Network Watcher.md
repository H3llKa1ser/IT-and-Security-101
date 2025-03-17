# Azure Network Watcher

Azure Network Watcher provides a suite of tools to monitor, diagnose, view metrics, and enable or disable logs for Azure IaaS (Infrastructure-as-a-Service) resources. Network Watcher enables you to monitor and repair the network health of IaaS products like virtual machines (VMs), virtual networks (VNets), application gateways, load balancers, etc. Network Watcher isn't designed or intended for PaaS monitoring or Web analytics.

Network Watcher consists of three major sets of tools and capabilities:

1) Monitoring

2) Network diagnostic tools

3) Traffic

#### NOTE: When you create or update a virtual network in your subscription, Network Watcher is automatically enabled in your virtual network's region. There's no impact on your resources or associated charge for automatically enabling Network Watcher.

## Monitoring

Network Watcher offers two monitoring tools that help you view and monitor resources:

1) Topology

2) Connection Monitor

### Topology

Topology provides a visualization of the entire network for understanding network configuration. It provides an interactive interface to view resources and their relationships in Azure spanning across multiple subscriptions, resource groups, and locations.

### Connection Monitor

Connection monitor provides end-to-end connection monitoring for Azure and hybrid endpoints. It helps you understand network performance between various endpoints in your network infrastructure.

## Network diagnostic tools

Network Watcher offers seven network diagnostic tools that help troubleshoot and diagnose network issues:

1) IP flow verify

2) NSG diagnostics

3) Next hop

4) Effective security rules

5) Connection troubleshoot

6) Packet capture

7) VPN troubleshoot

### IP flow verify

IP flow verify allows you to detect traffic filtering issues at a virtual machine level. It checks if a packet is allowed or denied to or from an IP address (IPv4 or IPv6 address). It also tells you which security rule allowed or denied the traffic.

### Network Security Group (NSG) diagnostics

NSG diagnostics allows you to detect traffic filtering issues at a virtual machine, virtual machine scale set, or application gateway level. It checks if a packet is allowed or denied to or from an IP address, IP prefix, or a service tag. It tells you which security rule allowed or denied the traffic. It also allows you to add a new security rule with a higher priority to allow or deny the traffic.

### Next hop

Next hop allows you to detect routing issues. It checks if traffic is routed correctly to the intended destination. It provides you with information about the Next hop type, IP address, and Route table ID for a specific destination IP address.

### Effective security rules

Effective security rules allow you to view the effective security rules applied to a network interface. It shows you all security rules applied to the network interface, the subnet the network interface is in, and the aggregate of both.

### Connection troubleshoot

Connection troubleshoot enables you to test a connection between a virtual machine, a virtual machine scale set, an application gateway, or a Bastion host and a virtual machine, an FQDN, a URI, or an IPv4 address. The test returns similar information returned when using the connection monitor capability, but tests the connection at a point in time instead of monitoring it over time, as connection monitor does.

### Packet capture

Packet capture allows you to remotely create packet capture sessions to track traffic to and from a virtual machine (VM) or a virtual machine scale set.

### VPN troubleshoot

VPN troubleshoot enables you to troubleshoot virtual network gateways and their connections

## Traffic

Network Watcher offers two traffic tools that help you log and visualize network traffic:

1) Flow Logs

2) Traffic Analytics

### Flow logs

Flow logs allows you to log information about your Azure IP traffic and stores the data in Azure storage.

Network security groups flow logging is a feature of Azure Network Watcher that allows you to log information about IP traffic flowing through a network security group. Flow data is sent to Azure Storage from where you can access it and export it to any visualization tool, security information and event management (SIEM) solution, or intrusion detection system (IDS) of your choice.

### Traffic Analytics

Traffic analytics provides rich visualizations of flow logs data.


![image](https://github.com/user-attachments/assets/f3532dbb-a06c-4166-bfe2-f45eac434012)

## Usage + quotas

The Usage + quotas capability of Network Watcher provides a summary of your deployed network resources within a subscription and region, including current usage and corresponding limits for each resource. For more information, see Networking limits to learn about the limits for each Azure network resource per region per subscription. This information is helpful when planning future resource deployments as you can't create more resources if you reach their limits within the subscription or region.

