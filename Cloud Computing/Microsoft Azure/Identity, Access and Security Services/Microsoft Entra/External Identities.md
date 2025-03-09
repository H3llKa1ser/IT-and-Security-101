# Microsoft Entra External Identities

B2B collaboration is a feature within Microsoft Entra External ID that lets you invite guest users to collaborate with your organization. With B2B collaboration, you can securely share your company's applications and services with external users, while maintaining control over your own corporate data. Work safely and securely with external partners, large or small, even if they don't have Microsoft Entra ID or an IT department.

A simple invitation and redemption process lets partners use their own credentials to access your company's resources. You can also enable self-service sign-up user flows to let external users sign up for apps or resources themselves. Once the external user has redeemed their invitation or completed sign-up, they're represented in your directory as a user object. The user type for these B2B collaboration users is typically set to "guest" and their user principal name contains the #EXT# identifier.

Developers can use Microsoft Entra business-to-business APIs to customize the invitation process or write applications like self-service sign-up portals.

## Collaborate with any partner using their identities

With Microsoft Entra B2B, the partner uses their own identity management solution, so there's no external administrative overhead for your organization. Guest users sign in to your apps and services with their own work, school, or social identities.

1) The partner uses their own identities and credentials, whether or not they have a Microsoft Entra account.

2) You don't need to manage external accounts or passwords.

3) You don't need to sync accounts or manage account lifecycles.

Manage collaboration with other organizations and clouds

B2B collaboration is enabled by default, but comprehensive admin settings let you control your inbound and outbound B2B collaboration with external partners and organizations:

1) For B2B collaboration with other Microsoft Entra organizations, use cross-tenant access settings. Manage inbound and outbound B2B collaboration, and scope access to specific users, groups, and applications. Set a default configuration that applies to all external organizations, and then create individual, organization-specific settings as needed. Using cross-tenant access settings, you can also trust multi-factor (MFA) and device claims (compliant claims and Microsoft Entra hybrid joined claims) from other Microsoft Entra organizations.

2) Use external collaboration settings to define who can invite external users, allow or block B2B specific domains, and set restrictions on guest user access to your directory.

3) Use Microsoft cloud settings to establish mutual B2B collaboration between the Microsoft Azure global cloud and Microsoft Azure Government or Microsoft Azure operated by 21Vianet.

## Easily invite guest users from the Azure portal

As an administrator, you can easily add guest users to your organization in the Azure portal.

1) Create a new guest user in Microsoft Entra ID, similar to how you'd add a new user.

2) Assign guest users to apps or groups.

3) Send an invitation email that contains a redemption link, or send a direct link to an app you want to share.

4) Guest users follow a few simple redemption steps to sign in.

## Allow self-service sign-up

With a self-service sign-up user flow, you can create a sign-up experience for external users who want to access your apps. As part of the sign-up flow, you can provide options for different social or enterprise identity providers, and collect information about the user.

You can also use API connectors to integrate your self-service sign-up user flows with external cloud systems. You can connect with custom approval workflows, perform identity verification, and validate user-provided information.

## Use policies to securely share your apps and services

You can use authentication and authorization policies to protect your corporate content. Conditional Access policies, such as multifactor authentication, can be enforced:

1) At the tenant level.

2) At the application level.

3) For specific guest users to protect corporate apps and data.

## Let application and group owners manage their own guest users

You can delegate guest user management to application owners so that they can add guest users directly to any application they want to share, whether it's a Microsoft application or not.

1) Administrators set up self-service app and group management.

2) Non-administrators use their Access Panel to add guest users to applications or groups.

## Customize the onboarding experience for B2B guest users

Bring your external partners on board in ways customized to your organization's needs.

1) Use Microsoft Entra entitlement management to configure policies that manage access for external users.

2) Use the B2B collaboration invitation APIs to customize your onboarding experiences.

## Integrate with Identity providers

Microsoft Entra External ID supports external identity providers like Facebook, Microsoft accounts, Google, or enterprise identity providers. You can set up federation with identity providers. This way your external users can sign in with their existing social or enterprise accounts instead of creating a new account just for your application.

## Integrate with SharePoint and OneDrive

You can enable integration with SharePoint and OneDrive to share files, folders, list items, document libraries, and sites with people outside your organization, while using Azure B2B for authentication and management. The users you share resources with are typically guest users in your directory, and permissions and groups work the same for these guests as they do for internal users. When enabling integration with SharePoint and OneDrive, you also enable the email one-time passcode feature in Microsoft Entra B2B to serve as a fallback authentication method.

# Microsoft Entra External ID

Microsoft Entra External ID combines powerful solutions for working with people outside of your organization. With External ID capabilities, you can allow external identities to securely access your apps and resources. Whether you’re working with external partners, consumers, or business customers, users can bring their own identities. These identities can range from corporate or government-issued accounts to social identity providers like Google or Facebook.

These scenarios fall within the scope of Microsoft Entra External ID:

1) If you’re an organization or a developer creating consumer apps, use External ID to quickly add authentication and customer identity and access management (CIAM) to your application. Register your app, create customized sign-in experiences, and manage your app users in a Microsoft Entra tenant in an external configuration. This tenant is separate from your employees and organizational resources.

2) If you want to enable your employees to collaborate with business partners and guests, use External ID for B2B collaboration. Allow secure access to your enterprise apps through invitation or self-service sign-up. Determine the level of access guests have to the Microsoft Entra tenant that contains your employees and organizational resources, which is a tenant in a workforce configuration.

Microsoft Entra External ID is a flexible solution for both consumer-oriented app developers needing authentication and CIAM, and businesses seeking secure B2B collaboration.

## Secure your apps for consumers and business customers

Organizations and developers can use External ID in an external tenant as their CIAM solution when publishing their apps to consumers and business customers. You can create a separate Microsoft Entra tenant in an external configuration, which allows you to manage your apps and user accounts separately from your workforce. Within this tenant, you can easily configure custom-branded sign-up experiences and user management features:

1) Set up self-service registration flows that define the series of sign-up steps customers follow and the sign-in methods they can use, such as email and password, one-time passcodes, or social accounts from Google or Facebook.

2) Create a custom look and feel for users signing in to your apps by configuring Company branding settings for your tenant. With these settings, you can add your own background images, colors, company logos, and text to customize the sign-in experiences across your apps.

3) Collect information from customers during sign-up by selecting from a series of built-in user attributes or adding your own custom attributes.

4) Analyze user activity and engagement data to uncover valuable insights that can aid strategic decisions and drive business growth.

With External ID, customers can sign in with an identity they already have. You can customize and control how customers sign up and sign in when using your applications. Because these CIAM capabilities are built into External ID, you also benefit from Microsoft Entra platform features like enhanced security, compliance, and scalability.

## Collaborate with business guests

External ID B2B collaboration allows your workforce to collaborate with external business partners. You can invite anyone to sign in to your Microsoft Entra organization using their own credentials so they can access the apps and resources you want to share with them. Use B2B collaboration when you need to let business guests access your Office 365 apps, software-as-a-service (SaaS) apps, and line-of-business applications. There are no credentials associated with business guests. Instead, they authenticate with their home organization or identity provider, and then your organization checks the user’s eligibility for guest collaboration.

There are various ways to add business guests to your organization for collaboration:

1) Invite users to collaborate using their Microsoft Entra accounts, Microsoft accounts, or social identities that you enable, such as Google. An admin can use the Microsoft Entra admin center or PowerShell to invite users to collaborate. The user signs into the shared resources using a simple redemption process with their work, school, or other email account.

2) Use self-service sign-up user flows to let guests sign up for applications themselves. The experience can be customized to allow sign-up with a work, school, or social identity (like Google or Facebook). You can also collect information about the user during the sign-up process.

3) Use Microsoft Entra entitlement management, an identity governance feature that lets you manage identity and access for external users at scale by automating access request workflows, access assignments, reviews, and expiration.

A user object is created for the business guest in the same directory as your employees. This user object can be managed like other user objects in your directory, added to groups, and so on. You can assign permissions to the user object (for authorization) while letting them use their existing credentials (for authentication).

You can use cross-tenant access settings to manage collaboration with other Microsoft Entra organizations and across Microsoft Azure clouds. For collaboration with non-Azure AD external users and organizations, use external collaboration settings.

## What are "workforce" and "external" tenants?

A tenant is a dedicated and trusted instance of Microsoft Entra ID that contains an organization's resources, including registered apps and a directory of users. There are two ways to configure a tenant, depending on how the organization intends to use the tenant and the resources they want to manage:

1) A workforce tenant configuration is a standard Microsoft Entra tenant that contains your employees, internal business apps, and other organizational resources. In a workforce tenant, your internal users can collaborate with external business partners and guests using B2B collaboration.

2) An external tenant configuration is used exclusively for apps you want to publish to consumers or business customers. This distinct tenant follows the standard Microsoft Entra tenant model, but is configured for consumer scenarios. It contains your app registrations and a directory of consumer or customer accounts.

## Comparing External ID feature sets

The following table compares the scenarios you can enable with External ID.

| **Identity** | **External ID in workforce tenants** | **External ID in external tenants** |
|-------------|--------------------------------|--------------------------------|
| **Primary scenario** | Allow your workforce to collaborate with business guests. Let guests use their preferred identities to sign in to resources in your Microsoft Entra organization. Provides access to Microsoft applications or your own applications (SaaS apps, custom-developed apps, etc.). <br> **Example:** Invite a guest to sign in to your Microsoft apps or become a guest member in Teams. | Publish apps to external consumers and business customers using External ID for identity experiences. Provides identity and access management for modern SaaS or custom-developed applications (not first-party Microsoft apps). <br> **Example:** Create a customized sign-in experience for users of your consumer mobile app and monitor app usage. |
| **Intended for** | Collaborating with business partners from external organizations like suppliers, partners, vendors. These users might or might not have Microsoft Entra ID or managed IT. | Consumers and business customers of your app. These users are managed in a Microsoft Entra tenant that is configured for external apps and users. |
| **User management** | B2B collaboration users are managed in the same workforce tenant as employees but are typically annotated as guest users. Guest users can be managed the same way as employees, added to the same groups, and so on. Cross-tenant access settings can be used to determine which users have access to B2B collaboration. | App users are managed in an external tenant that you create for consumers of your application. Users in an external tenant have different default permissions than users in a workforce tenant. They're managed in the external tenant, separate from the organization's employee directory. |
| **Single sign-on (SSO)** | SSO to all Microsoft Entra connected apps is supported. For example, you can provide access to Microsoft 365 or on-premises apps, and to other SaaS apps such as Salesforce or Workday. | SSO to apps registered in the external tenant is supported. SSO to Microsoft 365 or to other Microsoft SaaS apps isn't supported. |
| **Company branding** | The default state for the authentication experience is a Microsoft look and feel. Administrators can customize the guest sign-in experience with their company branding. | The default branding for the external tenant is neutral and doesn't include any existing Microsoft branding. Administrators can customize the branding for the organization or per application. [Learn more](https://learn.microsoft.com/). |
| **Microsoft cloud settings** | Supported. | Not applicable. |
| **Entitlement management** | Supported. | Not applicable. |
