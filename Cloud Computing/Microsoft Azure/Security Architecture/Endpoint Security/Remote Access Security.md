# Design a solution for secure remote access

This article describes the recommended guidance for providing remote access to virtual machines (VMs) deployed within an Azure landing zones architecture.

Azure offers different technologies for providing remote access to VMs:

1) Azure Bastion, a platform as a service (PaaS) solution, for accessing VMs through a browser or currently in preview through the native SSH/RDP client on Windows workstations

2) Just in time (JIT) access provided through Microsoft Defender for Cloud

3) Hybrid connectivity options, such as Azure ExpressRoute and VPNs

4) Public IP attached directly to the VM or through a NAT rule via an Azure public load balancer

The choice of which remote access solution is most appropriate depends on factors like scale, topology, and security requirements.

## Design considerations

When available, you can use existing hybrid connectivity to Azure virtual networks via ExpressRoute or S2S/P2S VPN connections to provide remote access from on-premises to Windows and Linux Azure VMs.

NSGs can be used to secure SSH/RDP connections to Azure VMs.

JIT allows remote SSH/RDP access over the internet without having to deploy any other infrastructure.

There are some availability limitations with JIT access.

JIT access can't be used for VMs protected by Azure firewalls controlled by Azure Firewall Manager.

Azure Bastion provides an extra layer of control. It enables secure and seamless RDP/SSH connectivity to your VMs directly from the Azure portal or native client in preview over a secure TLS channel. Azure Bastion also negates the need for hybrid connectivity.

Consider the appropriate Azure Bastion SKU to use based on your requirements as described in About Azure Bastion configuration settings.

Review the Azure Bastion FAQ for answers to common questions you might have about the service.

Azure Bastion can be used in Azure Virtual WAN topology however there are some limitations:

Azure Bastion cannot be deployed inside of a Virtual WAN virtual hub.

Azure Bastion must use the Standard SKU and also the IP based connection feature must be enabled on the Azure Bastion resource, see the Azure Bastion IP based connection documentation

Azure Bastion can be deployed in any spoke virtual network connected in a Virtual WAN, for accessing Virtual Machines, in its own or, other virtual networks that are connected to the same Virtual WAN, via its associated hubs, through Virtual WAN virtual network connections; providing routing is configured correctly.

## Design recommendations

Use existing ExpressRoute or VPN connectivity to provide remote access to Azure VMs that are accessible from on-premises via ExpressRoute or VPN connections.

In a Virtual WAN-based network topology where remote access to Virtual Machines over the internet is required:

Azure Bastion can be deployed in each spoke virtual network of the respective VMs.

Or you may choose to deploy a centralized Azure Bastion instance in a single spoke in your Virtual WAN topology, as shown in Figure 1. This configuration reduces the number of Azure Bastion instances to manage in your environment. This scenario requires users who sign in to Windows and Linux VMs via Azure Bastion to have a reader role on the Azure Bastion resource and the chosen spoke virtual network. Some implementations might have security or compliance considerations that restrict or prevent this.

In hub-and-spoke network topology, where remote access to Azure Virtual Machines over the internet is required:

A single Azure Bastion host can be deployed in the hub virtual network, which can provide connectivity to Azure VMs on spoke virtual networks via virtual network peering. This configuration reduces the number of Azure Bastion instances to manage in your environment. This scenario requires users who sign in to Windows and Linux VMs via Azure Bastion to have a reader role on the Azure Bastion resource and the hub virtual network. Some implementations might have security or compliance considerations. See Figure 2.

Your environment might not permit granting users the reader role-based access control (RBAC) role on the Azure Bastion resource and the hub virtual network. Use Azure Bastion Basic or Standard to provide connectivity to VMs within a spoke virtual network. Deploy a dedicated Azure Bastion instance into each spoke virtual network that requires remote access. See Figure 3.

Configure NSG rules to protect Azure Bastion and the VMs to which it provides connectivity. Follow the guidance in Working with VMs and NSGs in Azure Bastion.

Configure Azure Bastion diagnostic logs to be sent to the central Log Analytics workspace. Follow the guidance in Enable and work with Azure Bastion resource logs.

Ensure the required RBAC role assignments are made for the users or groups that connect to the VMs via Azure Bastion are in place.

If you connect to Linux VMs via SSH, use the feature of connecting by using a private key stored in Azure Key Vault.

Deploy Azure Bastion and ExpressRoute or VPN access to address specific needs like emergency break-glass access.

Remote access to Windows and Linux VMs via public IPs directly attached to the VMs is discouraged. Remote access should never be deployed without strict NSG rules and firewalling.

### Figure 1: Azure Virtual WAN topology.

![image](https://github.com/user-attachments/assets/d7ede9e6-b535-493b-a02f-f5fad4d1ba41)

### Figure 2: Azure hub-and-spoke topology.

![image](https://github.com/user-attachments/assets/2f90d9d4-7603-48df-a0e5-2bff6631930d)

### Figure 3: Azure standalone virtual network topology.

![image](https://github.com/user-attachments/assets/55186d4c-4788-4754-a522-f2a26f25a9bc)
