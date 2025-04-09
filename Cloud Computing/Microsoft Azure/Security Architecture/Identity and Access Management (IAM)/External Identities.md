# Design a solution for external identities

Microsoft Entra External ID combines powerful solutions for working with people outside of your organization. With External ID capabilities, you can allow external identities to securely access your apps and resources. Whether you’re working with external partners, consumers, or business customers, users can bring their own identities. These identities can range from corporate or government-issued accounts to social identity providers like Google or Facebook.

![image](https://github.com/user-attachments/assets/e3c340df-226d-4a5e-ae8c-d84b38ce5e95)

These scenarios fall within the scope of Microsoft Entra External ID:

1) If you’re an organization or a developer creating consumer apps, use External ID to quickly add authentication and customer identity and access management (CIAM) to your application. Register your app, create customized sign-in experiences, and manage your app users in a Microsoft Entra tenant in an external configuration. This tenant is separate from your employees and organizational resources.

2) If you want to enable your employees to collaborate with business partners and guests, use External ID for B2B collaboration. Allow secure access to your enterprise apps through invitation or self-service sign-up. Determine the level of access guests have to the Microsoft Entra tenant that contains your employees and organizational resources, which is a tenant in a workforce configuration.

Microsoft Entra External ID is a flexible solution for both consumer-oriented app developers needing authentication and CIAM, and businesses seeking secure B2B collaboration.

The sections that follow describe the two scenarios, but first it's important understand the terminology used in each of the two scenarios.

A tenant is a dedicated and trusted instance of Microsoft Entra ID that contains an organization's resources, including registered apps and a directory of users. There are two ways to configure a tenant, depending on how the organization intends to use the tenant and the resources they want to manage:

1) A workforce tenant configuration is a standard Microsoft Entra tenant that contains your employees, internal business apps, and other organizational resources. In a workforce tenant, your internal users can collaborate with external business partners and guests using B2B collaboration.

2) An external tenant configuration is used exclusively for apps you want to publish to consumers or business customers. This distinct tenant follows the standard Microsoft Entra tenant model, but is configured for consumer scenarios. It contains your app registrations and a directory of consumer or customer accounts.

## Secure your apps for consumers and business customers

Microsoft Entra External ID includes Microsoft's customer identity and access management (CIAM) solution. For organizations and businesses that want to make their apps available to consumers and business customers, External ID makes it easy to add CIAM features like self-service registration, personalized sign-in experiences, and customer account management. Because these CIAM capabilities are built into Microsoft Entra ID, you also benefit from platform features like enhanced security, compliance, and scalability.

![image](https://github.com/user-attachments/assets/1e7a3804-7fb4-4601-8c3a-bf2e2ff0f4c5)

Organizations and developers use External ID in an external tenant as their CIAM solution when publishing their apps to consumers and business customers. You can create a separate Microsoft Entra tenant in an external configuration, which allows you to manage your apps and user accounts separately from your workforce. Within this tenant, you can easily configure custom-branded sign-up experiences and user management features:

1) Set up self-service registration flows that define the series of sign-up steps customers follow and the sign-in methods they can use, such as email and password, one-time passcodes, or social accounts from Google or Facebook.

2) Create a custom look and feel for users signing in to your apps by configuring Company branding settings for your tenant. With these settings, you can add your own background images, colors, company logos, and text to customize the sign-in experiences across your apps.

3) Collect information from customers during sign-up by selecting from a series of built-in user attributes or adding your own custom attributes.

4) Analyze user activity and engagement data to uncover valuable insights that can aid strategic decisions and drive business growth.

With External ID, customers can sign in with an identity they already have. You can customize and control how customers sign up and sign in when using your applications. Because these CIAM capabilities are built into External ID, you also benefit from Microsoft Entra platform features like enhanced security, compliance, and scalability.

## Collaborate with business guests

External ID B2B collaboration allows your workforce to collaborate with external business partners. You can invite anyone to sign in to your Microsoft Entra organization using their own credentials so they can access the apps and resources you want to share with them. Use B2B collaboration when you need to let business guests access your Office 365 apps, software-as-a-service (SaaS) apps, and line-of-business applications. There are no credentials associated with business guests. Instead, they authenticate with their home organization or identity provider, and then your organization checks the user’s eligibility for guest collaboration.

![image](https://github.com/user-attachments/assets/bc5982e0-fd6f-4997-be16-e2b93f9b213f)

There are various ways to add business guests to your organization for collaboration:

1) Invite users to collaborate using their Microsoft Entra accounts, Microsoft accounts, or social identities that you enable, such as Google. An admin can use the Microsoft Entra admin center or PowerShell to invite users to collaborate. The user signs into the shared resources using a simple redemption process with their work, school, or other email account.

2) Use self-service sign-up user flows to let guests sign up for applications themselves. The experience can be customized to allow sign-up with a work, school, or social identity (like Google or Facebook). You can also collect information about the user during the sign-up process.

3) Use Microsoft Entra entitlement management, an identity governance feature that lets you manage identity and access for external users at scale by automating access request workflows, access assignments, reviews, and expiration.

A user object is created for the business guest in the same directory as your employees. This user object can be managed like other user objects in your directory, added to groups, and so on. You can assign permissions to the user object (for authorization) while letting them use their existing credentials (for authentication).

You can use cross-tenant access settings to manage collaboration with other Microsoft Entra organizations and across Microsoft Azure clouds. For collaboration with non-Azure AD external users and organizations, use external collaboration settings.

## Comparing External ID feature sets

The following table compares the scenarios you can enable with External ID.

| **Feature**                 | **External ID in Workforce Tenants**                                                                                                                                                    | **External ID in External Tenants**                                                                                                                                                        |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Primary scenario**       | Allow your workforce to collaborate with business guests. Guests can use their own identities to sign in to Microsoft Entra resources and access Microsoft or custom applications. <br> **Example**: Invite a guest to sign in to Microsoft apps or join Teams. | Publish apps to external consumers and business customers with External ID. Provides identity access for modern SaaS or custom-developed apps (not Microsoft first-party apps). <br> **Example**: Sign-in for a consumer mobile app. |
| **Intended for**           | Collaborating with external business partners like suppliers, vendors, or partners (with or without Entra ID or managed IT).                                                              | Consumers and business customers of your app. Users are managed in an external tenant configured specifically for external identity use.                                                    |
| **User management**        | B2B collaboration users are in the same tenant as employees (as guest users). They can be managed like employees and added to groups. Cross-tenant settings define access.              | App users are managed in a separate external tenant, distinct from employee directories. They have different permissions and management scopes.                                             |
| **Single sign-on (SSO)**   | SSO supported to all Entra-connected apps (e.g., Microsoft 365, on-prem apps, SaaS like Salesforce or Workday).                                                                           | SSO supported only to apps registered in the external tenant. Not supported for Microsoft 365 or other Microsoft SaaS apps.                                                                |
| **Company branding**       | Microsoft-themed by default. Admins can customize the guest sign-in experience.                                                                                                           | Neutral by default (no Microsoft branding). Admins can apply organization or per-app branding.                                                                                             |
| **Microsoft cloud settings** | Supported.                                                                                                                                                                                 | Not applicable.                                                                                                                                                                             |
| **Entitlement management** | Supported.                                                                                                                                                                                 | Not applicable.                                                                                                                                                                             |

## Related technologies

There are several Microsoft Entra technologies that are related to collaboration with external users and organizations. As you design your External ID collaboration model, consider these other features.

### B2B direct connect

B2B direct connect lets you create two-way trust relationships with other Microsoft Entra organizations to enable the Teams Connect shared channels feature. This feature allows users to seamlessly sign in to Teams shared channels for chat, calls, file-sharing, and app-sharing. When two organizations mutually enable B2B direct connect, users authenticate in their home organization and receive a token from the resource organization for access. Unlike B2B collaboration, B2B direct connect users aren't added as guests to your workforce directory. To learn more about B2B direct connect see [B2B direct connect overview](B2B direct connect overview)

### Azure Active Directory B2C

Azure Active Directory B2C (Azure AD B2C) is Microsoft's legacy solution for customer identity and access management. Azure AD B2C includes a separate consumer-based directory that you manage in the Azure portal through the Azure AD B2C service. Each Azure AD B2C tenant is separate and distinct from other Microsoft Entra ID and Azure AD B2C tenants. The Azure AD B2C portal experience is similar to Microsoft Entra ID, but there are key differences, such as the ability to customize your user journeys using the Identity Experience Framework.

### Conditional Access and MFA in external tenants

In external tenants, organizations can enforce MFA for customers by creating a Microsoft Entra Conditional Access policy and adding MFA to sign-up and sign-in user flows. External tenants support two methods for authentication as a second factor:

1) Email one-time passcode: After the user signs in with their email and password, they're prompted for a passcode that is sent to their email.

2) SMS-based authentication: SMS is available as a second factor authentication method for MFA for users in external tenants. Users who sign in with email and password, email and one-time passcode, or social identities like Google or Facebook, are prompted for second verification using SMS.

### Conditional Access for B2B collaboration and B2B direct connect

In a workforce tenant, organizations can enforce Conditional Access policies for external B2B collaboration and B2B direct connect users in the same way that they're enabled for full-time employees and members of the organization. For Microsoft Entra cross-tenant scenarios, if your Conditional Access policies require MFA or device compliance, you can now trust MFA and device compliance claims from an external user's home organization. When trust settings are enabled, during authentication, Microsoft Entra ID checks a user's credentials for an MFA claim or a device ID to determine if the policies were already met. If so, the external user is granted seamless sign-on to your shared resource. Otherwise, an MFA or device challenge is initiated in the user's home tenant. 

### Multitenant applications

If you offer a Software as a Service (SaaS) application to many organizations, you can configure your application to accept sign-ins from any Microsoft Entra tenant. This configuration is called making your application multitenant. Users in any Microsoft Entra tenant will be able to sign in to your application after consenting to use their account with your application.

### Multitenant organizations

A multitenant organization is an organization that has more than one instance of Microsoft Entra ID. There are various reasons for multi-tenancy. For example, your organization might span multiple clouds or geographical boundaries.

The multitenant organization capability enables seamless collaboration across Microsoft 365. It improves employee collaboration experiences across your organization of multiple tenants in applications such as Microsoft Teams and Microsoft Viva Engage.

The cross-tenant synchronization capability is a one-way synchronization service that ensures users can access resources, without receiving an invitation email and having to accept a consent prompt in each tenant.
