# Microsoft Entra Cloud Sync

Microsoft Entra Cloud Sync is a new offering from Microsoft designed to meet and accomplish your hybrid identity goals for synchronization of users, groups, and contacts to Microsoft Entra ID. It accomplishes this by using the Microsoft Entra cloud provisioning agent instead of the Microsoft Entra Connect application. However, it can be used alongside Microsoft Entra Connect Sync and it provides the following benefits:

1) Support for synchronizing to a Microsoft Entra tenant from a multi-forest disconnected Active Directory forest environment: The common scenarios include merger & acquisition (where the acquired company's AD forests are isolated from the parent company's AD forests), and companies that have historically had multiple AD forests.

2) Simplified installation with light-weight provisioning agents: The agents act as a bridge from AD to Microsoft Entra ID, with all the sync configuration managed in the cloud.

3) Multiple provisioning agents can be used to simplify high availability deployments, particularly critical for organizations relying upon password hash synchronization from AD to Microsoft Entra ID.

4) Support for large groups with up to 50,000 members. It's recommended to use only the organizational unit (OU) scoping filter when synchronizing large groups.

## How is Microsoft Entra Cloud Sync different from Microsoft Entra Connect Sync?

With Microsoft Entra Cloud Sync, provisioning from AD to Microsoft Entra ID is orchestrated in Microsoft Online Services. An organization only needs to deploy, in their on-premises or IaaS-hosted environment, a light-weight agent that acts as a bridge between Microsoft Entra ID and AD. The provisioning configuration is stored in Microsoft Entra ID and managed as part of the service.

## Comparison between Microsoft Entra Connect and Cloud Sync

The following table provides a comparison between Microsoft Entra Connect and Microsoft Entra Cloud Sync:

| Feature | Connect sync | Cloud sync |
|---|---|---|
| Connect to single on-premises AD forest | ● | ● |
| Connect to multiple on-premises AD forests | ● | ● |
| Connect to multiple disconnected on-premises AD forests |  | ● |
| Lightweight agent installation model |  | ● |
| Multiple active agents for high availability |  | ● |
| Connect to LDAP directories | ● |  |
| Support for user objects | ● | ● |
| Support for group objects | ● | ● |
| Support for contact objects | ● | ● |
| Support for device objects | ● |  |
| Allow basic customization for attribute flows | ● | ● |
| Synchronize Exchange online attributes | ● | ● |
| Synchronize extension attributes 1-15 | ● | ● |
| Synchronize customer defined AD attributes (directory extensions) | ● | ● |
| Support for Password Hash Sync | ● | ● |
| Support for Pass-Through Authentication | ● |  |
| Support for federation | ● | ● |
| Seamless Single Sign-on | ● | ● |
| Supports installation on a Domain Controller | ● | ● |
| Support for Windows Server 2016 | ● | ● |
| Filter on Domains/OUs/groups | ● | ● |
| Filter on objects' attribute values | ● |  |
| Allow minimal set of attributes to be synchronized (MinSync) | ● | ● |
| Allow removing attributes from flowing from AD to Microsoft Entra ID | ● | ● |
| Allow advanced customization for attribute flows | ● |  |
| Support for password writeback | ● | ● |
| Support for device writeback | ● | Customers should use Cloud Kerberos trust for this moving forward |
| Support for group writeback | ● | ● |
| Support for merging user attributes from multiple domains | ● |  |
| Microsoft Entra Domain Services support | ● |  |
| Exchange hybrid writeback | ● | ● |
| Unlimited number of objects per AD domain | ● |  |
| Support for up to 150,000 objects per AD domain | ● | ● |
| Groups with up to 50,000 members | ● | ● |
| Large groups with up to 250,000 members | ● |  |
| Cross domain references | ● | ● |
| On-demand provisioning |  | ● |
| Support for US Government | ● | ● |

