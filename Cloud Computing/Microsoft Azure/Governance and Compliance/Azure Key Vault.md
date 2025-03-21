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

