# Azure Virtual Network encryption

Azure Virtual Network encryption is a feature of Azure Virtual Networks. Virtual network encryption allows you to seamlessly encrypt and decrypt traffic between Azure Virtual Machines by creating a Datagram Transport Layer Security (DTLS) tunnel.

Virtual network encryption enables you to encrypt traffic between Virtual Machines and Virtual Machines Scale Sets within the same virtual network. Virtual network encryption encrypts traffic between regionally and globally peered virtual networks.

Virtual network encryption enhances existing encryption in transit capabilities in Azure.

## Requirements

1) Accelerated Networking must be enabled on the network interface of the virtual machine. For more information about Accelerated Networking, see What is Accelerated Networking?

2) Encryption is only applied to traffic between virtual machines in a virtual network. Traffic is encrypted from a private IP address to a private IP address.

3) Traffic to unsupported Virtual Machines is unencrypted. Use Virtual Network Flow Logs to confirm flow encryption between virtual machines. For more information, see Virtual network flow logs.

4) The start/stop of existing virtual machines is required after enabling encryption in a virtual network.

## Availability

Azure Virtual Network encryption is generally available in all Azure public regions and is currently in public preview in Azure Government and Microsoft Azure operated by 21Vianet.

## Limitations

Azure Virtual Network encryption has the following limitations:

1) In scenarios where a PaaS is involved, the virtual machine where the PaaS is hosted dictates if virtual network encryption is supported. The virtual machine must meet the listed requirements.

2) For Internal load balancer, all virtual machines behind the load balancer must be a supported virtual machine SKU.

3) AllowUnencrypted is the only supported enforcement at general availability. DropUnencrypted enforcement will be supported in the future.

4) Virtual networks with encryption enabled don't support Azure DNS Private Resolver.

5) Virtual networks configured with the Azure Private Link service don't support Virtual Network encryption, so Virtual Network encryption shouldn't be enabled on these virtual networks.

6) Virtual Network encryption shouldn't be enabled in virtual networks that have Azure confidential computing VM SKUs. If you want to use Azure confidential computing VMs in virtual networks where Virtual Network encryption is enabled, then:

Enable Accelerated Networking on the VM's NIC if it's supported.
If Accelerated Networking isn't supported, change the VM SKU to one that supports Accelerated Networking or Virtual Network encryption.

#### NOTE: Don't enable Virtual Network encryption if the VM SKU doesn't support Accelerated Networking or Virtual Network encryption.

## Supported Scenarios

Virtual network encryption is supported in the following scenarios:

| Scenario                            | Support |
|--------------------------------------|---------|
| **Virtual machines in the same virtual network** (including virtual machine scale sets and their internal load balancer) | Supported on traffic between virtual machines from these SKUs. |
| **Virtual network peering**          | Supported on traffic between virtual machines across regional peering. |
| **Global virtual network peering**    | Supported on traffic between virtual machines across global peering. |
| **Azure Kubernetes Service (AKS)**    | - Supported on AKS using Azure Container Network Interface (regular or overlay mode), Kubenet, or BYOCNI: node and pod traffic is encrypted.<br> - Partially supported on AKS using Azure CNI Dynamic Pod IP Assignment (podSubnetId specified): node traffic is encrypted, but pod traffic isn't encrypted.<br> - Traffic to the AKS managed control plane egresses from the virtual network and thus isn't in scope for virtual network encryption. However, this traffic is always encrypted via Transport Layer Security (TLS). |
