# Azure Firewall

Azure Firewall is a cloud-native and intelligent network firewall security service that provides the best of breed threat protection for your cloud workloads running in Azure. It's a fully stateful firewall as a service with built-in high availability and unrestricted cloud scalability. It provides both east-west and north-south traffic inspection.

Azure Firewall is offered in three SKUs: Standard, Premium, and Basic.

## Azure Firewall Standard

Azure Firewall Standard provides layer 3 to layer 7 (L3-L7) filtering and threat intelligence feeds directly from Microsoft Cyber Security. Threat intelligence-based filtering can alert and deny traffic from/to known malicious IP addresses and domains that are updated in real time to protect against new and emerging attacks.

![image](https://github.com/user-attachments/assets/c9d723a3-0fa3-4b45-a7ae-2aaee044cf6e)

## Azure Firewall Premium

Azure Firewall Premium provides advanced capabilities include signature based intrusion detection and prevention system (IDPS) to allow rapid detection of attacks by looking for specific patterns. These patterns can include byte sequences in network traffic or known malicious instruction sequences used by malware. There are more than 67,000 signatures in over 50 categories that are updated in real time to protect against new and emerging exploits. The exploit categories include malware, phishing, coin mining, and Trojan attacks.

![image](https://github.com/user-attachments/assets/9a063d84-d296-40e5-9e6f-769c0c291628)

## Azure Firewall Basic

Azure Firewall Basic is intended for small and medium size (SMB) customers to secure their Azure cloud environments. It provides the essential protection SMB customers need at an affordable price point.

Azure Firewall Basic is like Firewall Standard, but has the following main limitations:

1) Supports Threat Intel alert mode only

2) Fixed scale unit to run the service on two virtual machine backend instances

3) Recommended for environments with an estimated throughput of 250 Mbps

![image](https://github.com/user-attachments/assets/375a61f1-4cb8-4462-8460-22c13617e27a)

## Azure Firewall Manager

Azure Firewall Manager is a security management service that provides central security policy and route management for cloud-based security perimeters.

Firewall Manager can provide security management for two network architecture types:

1) Secured virtual hub
An Azure Virtual WAN Hub is a Microsoft-managed resource that lets you easily create hub and spoke architectures. When security and routing policies are associated with such a hub, it is referred to as a secured virtual hub.

2) Hub virtual network
This is a standard Azure virtual network that you create and manage yourself. When security policies are associated with such a hub, it is referred to as a hub virtual network. At this time, only Azure Firewall Policy is supported. You can peer spoke virtual networks that contain your workload servers and services. You can also manage firewalls in standalone virtual networks that aren't peered to any spoke.

![image](https://github.com/user-attachments/assets/5ee6c954-8ccb-44c0-a855-df3512594891)

## Features

Azure Firewall Manager offers the following features:

### Central Azure Firewall deployment and configuration

You can centrally deploy and configure multiple Azure Firewall instances that span different Azure regions and subscriptions.

### Hierarchical policies (global and local)

You can use Azure Firewall Manager to centrally manage Azure Firewall policies across multiple secured virtual hubs. Your central IT teams can author global firewall policies to enforce organization wide firewall policy across teams. Locally authored firewall policies allow a DevOps self-service model for better agility.

### Integrated with third-party security-as-a-service for advanced security

In addition to Azure Firewall, you can integrate third-party security as a service (SECaaS) providers to provide additional network protection for your VNet and branch Internet connections.

This feature is available only with secured virtual hub deployments.

1) VNet to Internet (V2I) traffic filtering

Filter outbound virtual network traffic with your preferred third-party security provider.
Leverage advanced user-aware Internet protection for your cloud workloads running on Azure.

2) Branch to Internet (B2I) traffic filtering Leverage your Azure connectivity and global distribution to easily add third-party filtering for branch to Internet scenarios.

### Centralized route management

Easily route traffic to your secured hub for filtering and logging without the need to manually setup User Defined Routes (UDR) on spoke virtual networks.

This feature is available only with secured virtual hub deployments.

You can use third-party providers for Branch to Internet (B2I) traffic filtering, side by side with Azure Firewall for Branch to VNet (B2V), VNet to VNet (V2V) and VNet to Internet (V2I).

## DDoS protection plan

You can associate your virtual networks with a DDoS protection plan within Azure Firewall Manager. For more information, see Configure an Azure DDoS Protection Plan using Azure Firewall Manager.

## Manage Web Application Firewall policies

You can centrally create and associate Web Application Firewall (WAF) policies for your application delivery platforms, including Azure Front Door and Azure Application Gateway. For more information, see Manage Web Application Firewall policies.

## Region availability

Azure Firewall Policies can be used across regions. For example, you can create a policy in West US, and use it in East US.

