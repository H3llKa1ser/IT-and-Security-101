# Azure Key Vault

Azure Key Vault is a cloud service for securely storing and accessing secrets. A secret is anything that you want to tightly control access to, such as API keys, passwords, certificates, or cryptographic keys. Key Vault service supports two types of containers: vaults and managed hardware security module (HSM) pools. Vaults support storing software and HSM-backed keys, secrets, and certificates. Managed HSM pools only support HSM-backed keys.

Here are other important terms:

1) Tenant: A tenant is the organization that owns and manages a specific instance of Microsoft cloud services. It's most often used to refer to the set of Azure and Microsoft 365 services for an organization.

2) Vault owner: A vault owner can create a key vault and gain full access and control over it. The vault owner can also set up auditing to log who accesses secrets and keys. Administrators can control the key lifecycle. They can roll to a new version of the key, back it up, and do related tasks.

3) Vault consumer: A vault consumer can perform actions on the assets inside the key vault when the vault owner grants the consumer access. The available actions depend on the permissions granted.

4) Managed HSM Administrators: Users who are assigned the Administrator role have complete control over a Managed HSM pool. They can create more role assignments to delegate controlled access to other users.

5) Managed HSM Crypto Officer/User: Built-in roles that are usually assigned to users or service principals that will perform cryptographic operations using keys in Managed HSM. Crypto User can create new keys, but can't delete keys.

6) Managed HSM Crypto Service Encryption User: Built-in role that is usually assigned to a service accounts managed service identity (for example, Storage account) for encryption of data at rest with customer managed key.

7) Resource: A resource is a manageable item that's available through Azure. Common examples are virtual machine, storage account, web app, database, and virtual network. There are many more.

8) Resource group: A resource group is a container that holds related resources for an Azure solution. The resource group can include all the resources for the solution, or only those resources that you want to manage as a group. You decide how you want to allocate resources to resource groups, based on what makes the most sense for your organization.

9) Security principal: An Azure security principal is a security identity that user-created apps, services, and automation tools use to access specific Azure resources. Think of it as a "user identity" (username and password or certificate) with a specific role, and tightly controlled permissions. A security principal should only need to do specific things, unlike a general user identity. It improves security if you grant it only the minimum permission level that it needs to perform its management tasks. A security principal used with an application or service is called a service principal.

10) Microsoft Entra ID: Microsoft Entra ID is the directory service for a tenant. Each directory has one or more domains. A directory can have many subscriptions associated with it, but only one tenant.

11) Azure tenant ID: A tenant ID is a unique way to identify a Microsoft Entra instance within an Azure subscription.

12) Managed identities: Azure Key Vault provides a way to securely store credentials and other keys and secrets, but your code needs to authenticate to Key Vault to retrieve them. Using a managed identity makes solving this problem simpler by giving Azure services an automatically managed identity in Microsoft Entra ID. You can use this identity to authenticate to Key Vault or any service that supports Microsoft Entra authentication, without having any credentials in your code.

## Authentication

To do any operations with Key Vault, you first need to authenticate to it. There are three ways to authenticate to Key Vault:

1) Managed identities for Azure resources: When you deploy an app on a virtual machine in Azure, you can assign an identity to your virtual machine that has access to Key Vault. You can also assign identities to other Azure resources. The benefit of this approach is that the app or service isn't managing the rotation of the first secret. Azure automatically rotates the identity. We recommend this approach as a best practice.

2) Service principal and certificate: You can use a service principal and an associated certificate that has access to Key Vault. We don't recommend this approach because the application owner or developer must rotate the certificate.

3) Service principal and secret: Although you can use a service principal and a secret to authenticate to Key Vault, we don't recommend it. It's hard to automatically rotate the bootstrap secret that's used to authenticate to Key Vault.

## Encryption of data in transit

Azure Key Vault enforces Transport Layer Security (TLS) protocol to protect data when it’s traveling between Azure Key vault and clients. Clients negotiate a TLS connection with Azure Key Vault. TLS provides strong authentication, message privacy, and integrity (enabling detection of message tampering, interception, and forgery), interoperability, algorithm flexibility, and ease of deployment and use.

Perfect Forward Secrecy (PFS) protects connections between customers’ client systems and Microsoft cloud services by unique keys. Connections also use Rivest-Shamir-Adleman (RSA)-based 2,048-bit encryption key lengths. This combination makes it difficult for someone to intercept and access data that is in transit.

## Key Vault roles

Use the following table to better understand how Key Vault can help to meet the needs of developers and security administrators.

| Role | Problem Statement | Solved by Azure Key Vault |
|------|------------------|--------------------------|
| **Developer for an Azure application** | "I want to write an application for Azure that uses keys for signing and encryption. But I want these keys to be external from my application so that the solution is suitable for an application that's geographically distributed. I want these keys and secrets to be protected, without having to write the code myself. I also want these keys and secrets to be easy for me to use from my applications, with optimal performance." | ✔ Keys are stored in a vault and invoked by URI when needed. <br> ✔ Keys are safeguarded by Azure, using industry-standard algorithms, key lengths, and hardware security modules. <br> ✔ Keys are processed in HSMs that reside in the same Azure datacenters as the applications, providing better reliability and reduced latency than on-premises keys. |
| **Developer for software as a service (SaaS)** | "I don't want the responsibility or potential liability for my customers' tenant keys and secrets. I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features." | ✔ Customers can import their own keys into Azure and manage them. <br> ✔ When a SaaS application needs to perform cryptographic operations using customers' keys, Key Vault handles these operations on behalf of the application, ensuring the application never accesses the keys directly. |
| **Chief Security Officer (CSO)** | "I want to know that our applications comply with Federal Information Processing Standards (FIPS) 140-2 Level 2 or FIPS 140-2 Level 3 HSMs for secure key management. I want to make sure that my organization is in control of the key lifecycle and can monitor key usage. And although we use multiple Azure services and resources, I want to manage the keys from a single location in Azure." | ✔ Choose vaults for FIPS 140-2 Level 2 validated HSMs. <br> ✔ Choose managed HSM pools for FIPS 140-2 Level 3 validated HSMs. <br> ✔ Key Vault is designed so that Microsoft does not see or extract your keys. <br> ✔ Key usage is logged in near real-time. <br> ✔ The vault provides a single interface, regardless of how many vaults you have in Azure, which regions they support, and which applications use them. |

Anybody with an Azure subscription can create and use key vaults. Although Key Vault benefits developers and security administrators, it can be implemented and managed by an organization's administrator who manages other Azure services. For example, this administrator can sign in with an Azure subscription, create a vault for the organization in which to store keys, and then be responsible for operational tasks like these:

1) Create or import a key or secret.

2) Revoke or delete a key or secret.

3) Authorize users or applications to access the key vault, so they can then manage or use its keys and secrets.

4) Configure key usage (for example, sign or encrypt).

5) Monitor key usage.

![image](https://github.com/user-attachments/assets/023f11a0-0422-444b-87b6-83f77908bfa4)

## Azure Key Vault Security

Azure Key Vault protects cryptographic keys, certificates (and the private keys associated with the certificates), and secrets (such as connection strings and passwords) in the cloud. When storing sensitive and business critical data, however, you must take steps to maximize the security of your vaults and the data stored in them.

### Network security

You can reduce the exposure of your vaults by specifying which IP addresses have access to them. The virtual network service endpoints for Azure Key Vault allow you to restrict access to a specified virtual network. The endpoints also allow you to restrict access to a list of IPv4 (internet protocol version 4) address ranges. Any user connecting to your key vault from outside those sources is denied access.

After firewall rules are in effect, users can only read data from Key Vault when their requests originate from allowed virtual networks or IPv4 address ranges. This also applies to accessing Key Vault from the Azure portal. Although users can browse to a key vault from the Azure portal, they might not be able to list keys, secrets, or certificates if their client machine is not in the allowed list.

Azure Private Link Service enables you to access Azure Key Vault and Azure hosted customer/partner services over a Private Endpoint in your virtual network. An Azure Private Endpoint is a network interface that connects you privately and securely to a service powered by Azure Private Link. The private endpoint uses a private IP address from your VNet, effectively bringing the service into your VNet. All traffic to the service can be routed through the private endpoint, so no gateways, Network address translation (NAT) devices, ExpressRoute or VPN connections, or public IP addresses are needed. Traffic between your virtual network and the service traverses over the Microsoft backbone network, eliminating exposure from the public Internet. You can connect to an instance of an Azure resource, giving you the highest level of granularity in access control.

### Transport Layer Security (TLS) and Hypertext Transfer Protocol Secure (HTTPS)

The Key Vault front end (data plane) is a multitenant server. This means that key vaults from different customers can share the same public IP address. In order to achieve isolation, each HTTP request is authenticated and authorized independently of other requests.

The HTTPS protocol allows the client to participate in TLS negotiation. Clients can enforce the version of TLS, and whenever a client does so, the entire connection will use the corresponding level protection. Key Vault supports TLS 1.2 and 1.3 protocol versions.

### Key Vault authentication options

When you create a key vault in an Azure subscription, it's automatically associated with the Microsoft Entra tenant of the subscription. All callers in both planes must register in this tenant and authenticate to access the key vault. In both cases, applications can access Key Vault in three ways:

1) Application-only: The application represents a service principal or managed identity. This identity is the most common scenario for applications that periodically need to access certificates, keys, or secrets from the key vault. For this scenario to work, the objectId of the application must be specified in the access policy and the applicationId must not be specified or must be null.

2) User-only: The user accesses the key vault from any application registered in the tenant. Examples of this type of access include Azure PowerShell and the Azure portal. For this scenario to work, the objectId of the user must be specified in the access policy and the applicationId must not be specified or must be null.

3) Application-plus-user (sometimes referred as compound identity): The user is required to access the key vault from a specific application and the application must use the on-behalf-of authentication (OBO) flow to impersonate the user. For this scenario to work, both applicationId and objectId must be specified in the access policy. The applicationId identifies the required application and the objectId identifies the user. Currently, this option isn't available for data plane Azure RBAC.

In all types of access, the application authenticates with Microsoft Entra ID. The application uses any supported authentication method based on the application type. The application acquires a token for a resource in the plane to grant access. The resource is an endpoint in the management or data plane, based on the Azure environment. The application uses the token and sends a REST API request to Key Vault.

The model of a single mechanism for authentication to both planes has several benefits:

1) Organizations can control access centrally to all key vaults in their organization.

2) If a user leaves, they instantly lose access to all key vaults in the organization.

3) Organizations can customize authentication by using the options in Microsoft Entra ID, such as to enable multifactor authentication for added security.

## Access Model Overview

Access to a key vault is controlled through two interfaces: the management plane and the data plane. The management plane is where you manage Key Vault itself. Operations in this plane include creating and deleting key vaults, retrieving Key Vault properties, and updating access policies. The data plane is where you work with the data stored in a key vault. You can add, delete, and modify keys, secrets, and certificates.

Both planes use Microsoft Entra ID for authentication. For authorization, the management plane uses Azure role-based access control (Azure RBAC) and the data plane uses a Key Vault access policy and Azure RBAC for Key Vault data plane operations.

To access a key vault in either plane, all callers (users or applications) must have proper authentication and authorization. Authentication establishes the identity of the caller. Authorization determines which operations the caller can execute. Authentication with Key Vault works in conjunction with Microsoft Entra ID, which is responsible for authenticating the identity of any given security principal.

A security principal is an object that represents a user, group, service, or application that's requesting access to Azure resources. Azure assigns a unique object ID to every security principal.

1) A user security principal identifies an individual who has a profile in Microsoft Entra ID.

2) A group security principal identifies a set of users created in Microsoft Entra ID. Any roles or permissions assigned to the group are granted to all of the users within the group.

3) A service principal is a type of security principal that identifies an application or service, which is to say, a piece of code rather than a user or group. A service principal's object ID is known as its client ID and acts like its username. The service principal's client secret or certificate acts like its password.Many Azure Services supports assigning Managed Identity with automated management of client ID and certificate. Managed identity is the most secure and recommended option for authenticating within Azure.

### Conditional Access

Key Vault provides support for Microsoft Entra Conditional Access policies. By using Conditional Access policies, you can apply the right access controls to Key Vault when needed to keep your organization secure and stay out of your user's way when not needed.

### Privileged access

Authorization determines which operations the caller can perform. Authorization in Key Vault uses Azure role-based access control (Azure RBAC) on management plane and either Azure RBAC or Azure Key Vault access policies on data plane.

Access to vaults takes place through two interfaces or planes. These planes are the management plane and the data plane.

The management plane is where you manage Key Vault itself and it is the interface used to create and delete vaults. You can also read key vault properties and manage access policies.

The data plane allows you to work with the data stored in a key vault. You can add, delete, and modify keys, secrets, and certificates.

Applications access the planes through endpoints. The access controls for the two planes work independently. To grant an application access to use keys in a key vault, you grant data plane access by using Azure RBAC or a Key Vault access policy. To grant a user read access to Key Vault properties and tags, but not access to data (keys, secrets, or certificates), you grant management plane access with Azure RBAC.

### Managing administrative access to Key Vault

When you create a key vault in a resource group, you manage access by using Microsoft Entra ID. You grant users or groups the ability to manage the key vaults in a resource group. You can grant access at a specific scope level by assigning the appropriate Azure roles. To grant access to a user to manage key vaults, you assign a predefined key vault Contributor role to the user at a specific scope. The following scopes levels can be assigned to an Azure role:

1) Subscription: An Azure role assigned at the subscription level applies to all resource groups and resources within that subscription.

2) Resource group: An Azure role assigned at the resource group level applies to all resources in that resource group.

3) Specific resource: An Azure role assigned for a specific resource applies to that resource. In this case, the resource is a specific key vault.

When using the Access Policy permission model, if a user has Contributor permissions to a key vault management plane, the user can grant themselves access to the data plane by setting a Key Vault access policy. You should tightly control who has Contributor role access to your key vaults with the Access Policy permission model to ensure that only authorized persons can access and manage your key vaults, keys, secrets, and certificates. It is recommended to use the new Role Based Access Control (RBAC) permission model to avoid this issue. With the RBAC permission model, permission management is limited to 'Owner' and 'User Access Administrator' roles, which allows separation of duties between roles for security operations and general administrative operations.

### Controlling access to Key Vault data

You can control access to Key Vault keys, certificates and secrets using Azure RBAC or Key Vault access policies.

## Logging and monitoring

Key Vault logging saves information about the activities performed on your vault.

You can integrate Key Vault with Event Grid to be notified when the status of a key, certificate, or secret stored in key vault has changed.

It is also important to monitor the health of your key vault, to make sure your service operates as intended.

## Backup and recovery

Azure Key Vault soft-delete and purge protection allows you to recover deleted vaults and vault objects.

You should also take regular back ups of your vault on update/delete/create of objects within a Vault.

