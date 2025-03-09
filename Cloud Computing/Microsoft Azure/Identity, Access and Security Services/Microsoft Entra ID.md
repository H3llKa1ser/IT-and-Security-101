# Microsoft Entra ID (AKA Azure Active Directory AAD)

Microsoft Entra ID is a directory service that enables you to sign in and access both Microsoft cloud applications and cloud applications that you develop. Microsoft Entra ID can also help you maintain your on-premises Active Directory deployment.

For on-premises environments, Active Directory running on Windows Server provides an identity and access management service that's managed by your organization. Microsoft Entra ID is Microsoft's cloud-based identity and access management service. With Microsoft Entra ID, you control the identity accounts, but Microsoft ensures that the service is available globally. If you've worked with Active Directory, Microsoft Entra ID will be familiar to you.

When you secure identities on-premises with Active Directory, Microsoft doesn't monitor sign-in attempts. When you connect Active Directory with Microsoft Entra ID, Microsoft can help protect you by detecting suspicious sign-in attempts at no extra cost. For example, Microsoft Entra ID can detect sign-in attempts from unexpected locations or unknown devices.

## Who uses Microsoft Entra ID?

Microsoft Entra ID is for:

1) IT administrators. Administrators can use Microsoft Entra ID to control access to applications and resources based on their business requirements.

2) App developers. Developers can use Microsoft Entra ID to provide a standards-based approach for adding functionality to applications that they build, such as adding SSO functionality to an app or enabling an app to work with a user's existing credentials.

3) Users. Users can manage their identities and take maintenance actions like self-service password reset.

4) Online service subscribers. Microsoft 365, Microsoft Office 365, Azure, and Microsoft Dynamics CRM Online subscribers are already using Microsoft Entra ID to authenticate into their account.

## What does Microsoft Entra ID do?

Microsoft Entra ID provides services such as:

1) Authentication: This includes verifying identity to access applications and resources. It also includes providing functionality such as self-service password reset, multifactor authentication, a custom list of banned passwords, and smart lockout services.

2) Single sign-on: Single sign-on (SSO) enables you to remember only one username and one password to access multiple applications. A single identity is tied to a user, which simplifies the security model. As users change roles or leave an organization, access modifications are tied to that identity, which greatly reduces the effort needed to change or disable accounts.

3) Application management: You can manage your cloud and on-premises apps by using Microsoft Entra ID. Features like Application Proxy, SaaS apps, the My Apps portal, and single sign-on provide a better user experience.

4) Device management: Along with accounts for individual people, Microsoft Entra ID supports the registration of devices. Registration enables devices to be managed through tools like Microsoft Intune. It also allows for device-based Conditional Access policies to restrict access attempts to only those coming from known devices, regardless of the requesting user account.

## Can I connect my on-premises AD with Microsoft Entra ID?

If you had an on-premises environment running Active Directory and a cloud deployment using Microsoft Entra ID, you would need to maintain two identity sets. However, you can connect Active Directory with Microsoft Entra ID, enabling a consistent identity experience between cloud and on-premises.

One method of connecting Microsoft Entra ID with your on-premises AD is using Microsoft Entra Connect. Microsoft Entra Connect synchronizes user identities between on-premises Active Directory and Microsoft Entra ID. Microsoft Entra Connect synchronizes changes between both identity systems, so you can use features like SSO, multifactor authentication, and self-service password reset under both systems.

# Microsoft Entra Domain Services

Microsoft Entra Domain Services is a service that provides managed domain services such as domain join, group policy, lightweight directory access protocol (LDAP), and Kerberos/NTLM authentication. Just like Microsoft Entra ID lets you use directory services without having to maintain the infrastructure supporting it, with Microsoft Entra Domain Services, you get the benefit of domain services without the need to deploy, manage, and patch domain controllers (DCs) in the cloud.

A Microsoft Entra Domain Services managed domain lets you run legacy applications in the cloud that can't use modern authentication methods, or where you don't want directory lookups to always go back to an on-premises AD DS environment. You can lift and shift those legacy applications from your on-premises environment into a managed domain, without needing to manage the AD DS environment in the cloud.

Microsoft Entra Domain Services integrates with your existing Microsoft Entra tenant. This integration lets users sign into services and applications connected to the managed domain using their existing credentials. You can also use existing groups and user accounts to secure access to resources. These features provide a smoother lift-and-shift of on-premises resources to Azure.

## How does Microsoft Entra Domain Services work?

When you create a Microsoft Entra Domain Services managed domain, you define a unique namespace. This namespace is the domain name. Two Windows Server domain controllers are then deployed into your selected Azure region. This deployment of DCs is known as a replica set.

You don't need to manage, configure, or update these DCs. The Azure platform handles the DCs as part of the managed domain, including backups and encryption at rest using Azure Disk Encryption.

## Is information synchronized?

A managed domain is configured to perform a one-way synchronization from Microsoft Entra ID to Microsoft Entra Domain Services. You can create resources directly in the managed domain, but they aren't synchronized back to Microsoft Entra ID. In a hybrid environment with an on-premises AD DS environment, Microsoft Entra Connect synchronizes identity information with Microsoft Entra ID, which is then synchronized to the managed domain.

Applications, services, and VMs in Azure that connect to the managed domain can then use common Microsoft Entra Domain Services features such as domain join, group policy, LDAP, and Kerberos/NTLM authentication.

## Microsoft Entra ID licenses

Microsoft Online business services, such as Microsoft 365 or Microsoft Azure, use Microsoft Entra ID for sign-in activities and to help protect your identities. If you subscribe to any Microsoft Online business service, you automatically get access to Microsoft Entra ID Free.

To enhance your Microsoft Entra implementation, you can also add paid features by upgrading to Microsoft Entra ID P1 or Premium P2 licenses. Microsoft Entra paid licenses are built on top of your existing free directory. The licenses provide self-service, enhanced monitoring, security reporting, and secure access for your mobile users.

1) Microsoft Entra ID Free. Provides user and group management, on-premises directory synchronization, basic reports, self-service password change for cloud users, and single sign-on across Azure, Microsoft 365, and many popular SaaS apps.

2) Microsoft Entra ID P1. In addition to the Free features, P1 also lets your hybrid users access both on-premises and cloud resources. It also supports advanced administration, such as dynamic groups, self-service group management, Microsoft Identity Manager, and cloud write-back capabilities, which allow self-service password reset for your on-premises users.

3) Microsoft Entra ID P2. In addition to the Free and P1 features, P2 also offers Microsoft Entra ID Protection to help provide risk-based Conditional Access to your apps and critical company data and Privileged Identity Management to help discover, restrict, and monitor administrators and their access to resources and to provide just-in-time access when needed.

4) "Pay as you go" feature licenses. You can also get licenses for features such as, Microsoft Entra Business-to-Customer (B2C). B2C can help you provide identity and access management solutions for your customer-facing apps. For more information, see Azure Active Directory B2C documentation.

## Features

| Category | Description |
|----------|------------|
| **Application management** | Manage your cloud and on-premises apps using Application Proxy, single sign-on, the My Apps portal, and Software as a Service (SaaS) apps. [More info](https://learn.microsoft.com/en-us/entra/identity/app-proxy/) |
| **Authentication** | Manage Microsoft Entra self-service password reset, multifactor authentication, custom banned password list, and smart lockout. [More info](https://learn.microsoft.com/en-us/entra/identity/authentication/) |
| **Microsoft Entra ID for developers** | Build apps that sign in all Microsoft identities, get tokens to call Microsoft Graph, other Microsoft APIs, or custom APIs. [More info](https://learn.microsoft.com/en-us/entra/identity-platform/) |
| **Business-to-Business (B2B)** | Manage your guest users and external partners, while maintaining control over your own corporate data. [More info](https://learn.microsoft.com/en-us/entra/external-id/b2b/) |
| **Business-to-Customer (B2C)** | Customize and control how users sign up, sign in, and manage their profiles when using your apps. [More info](https://learn.microsoft.com/en-us/azure/active-directory-b2c/) |
| **Conditional Access** | Manage access to your cloud apps. [More info](https://learn.microsoft.com/en-us/entra/identity/conditional-access/) |
| **Device Management** | Manage how your cloud or on-premises devices access your corporate data. [More info](https://learn.microsoft.com/en-us/entra/identity/device-management/) |
| **Domain services** | Join Azure virtual machines to a domain without using domain controllers. [More info](https://learn.microsoft.com/en-us/azure/active-directory-domain-services/) |
| **Enterprise users** | Manage license assignments, access to apps, and set up delegates using groups and administrator roles. [More info](https://learn.microsoft.com/en-us/entra/identity/users/) |
| **Hybrid identity** | Use Microsoft Entra Connect and Connect Health to provide a single user identity for authentication and authorization to all resources, regardless of location (cloud or on-premises). [More info](https://learn.microsoft.com/en-us/entra/identity/hybrid/) |
| **Identity governance** | Manage your organization's identity through employee, business partner, vendor, service, and app access controls. You can also perform access reviews. [More info](https://learn.microsoft.com/en-us/entra/identity/governance/) |
| **Identity protection** | Detect potential vulnerabilities affecting your organization's identities, configure policies to respond to suspicious actions, and then take appropriate action to resolve them. [More info](https://learn.microsoft.com/en-us/entra/identity-protection/) |
| **Managed identities for Azure resources** | Provide your Azure services with an automatically managed identity in Microsoft Entra ID that can authenticate any Microsoft Entra-supported authentication service, including Key Vault. [More info](https://learn.microsoft.com/en-us/azure/active-directory/managed-identities-azure-resources/) |
| **Privileged identity management (PIM)** | Manage, control, and monitor access within your organization. This feature includes access to resources in Microsoft Entra ID and Azure, and other Microsoft Online Services, like Microsoft 365 or Intune. [More info](https://learn.microsoft.com/en-us/entra/identity/privileged-identity-management/) |
| **Monitoring and health** | Gain insights into the security and usage patterns in your environment. [More info](https://learn.microsoft.com/en-us/entra/identity/monitoring/) |
| **Workload identities** | Give an identity to your software workload (such as an application, service, script, or container) to authenticate and access other services and resources. [More info](https://learn.microsoft.com/en-us/entra/identity/workload-identities/) |

