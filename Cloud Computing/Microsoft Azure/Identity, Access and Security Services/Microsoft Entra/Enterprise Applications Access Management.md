# Manage access to enterprise applications in Microsoft Entra ID, including OAuth permission grants

Ongoing access management, usage evaluation, and reporting continue to be a challenge after an app is integrated into your organization's identity system. In many cases, IT Administrators or help desk have to take an ongoing active role in managing access to your apps. Sometimes, assignment is performed by a general or divisional IT team. Often, the assignment decision is intended to be delegated to the business decision maker, requiring their approval before IT makes the assignment.

Other organizations invest in integration with an existing automated identity and access management system, like Role-Based Access Control (RBAC) or Attribute-Based Access Control (ABAC). Both the integration and rule development tend to be specialized and expensive. Monitoring or reporting on either management approach is its own separate, costly, and complex investment.

## How does Microsoft Entra ID help?

Microsoft Entra ID supports extensive access management for configured applications, enabling organizations to easily achieve the right access policies ranging from automatic, attribute-based assignment (ABAC or RBAC scenarios) through delegation and including administrator management. With Microsoft Entra ID, you can easily achieve complex policies, combining multiple management models for a single application and can even reuse management rules across applications with the same audiences.

With Microsoft Entra ID, usage and assignment reporting is fully integrated, enabling administrators to easily report on assignment state, assignment errors, and even usage.

## Assigning users and groups to an app

Microsoft Entra application assignment focuses on two primary assignment modes:

1) Individual assignment: An IT admin with directory Global Administrator permissions can select individual user accounts and grant them access to the application.

2) Group-based assignment: (requires Microsoft Entra ID P1 or P2) An IT admin with directory Global Administrator permissions can assign a group to the application. Specific users' access is determined by whether they are members of the group at the time they try to access the application. In other words, an administrator can effectively create an assignment rule stating "any current member of the assigned group has access to the application". Using this assignment option, administrators can benefit from any of Microsoft Entra group management options, including attribute-based dynamic groups, external system groups (for example, on-premises Active Directory or Workday), or Administrator-managed or self-service-managed groups. A single group can be easily assigned to multiple apps, making sure that applications with assignment affinity can share assignment rules, reducing the overall management complexity.

## Requiring user assignment for an app

With certain types of applications, you have the option of requiring users to be assigned to the application. By doing so, you prevent everyone from signing in except those users you explicitly assign to the application. The following types of applications support this option:

1) Applications configured for federated single sign-on (SSO) with SAML-based authentication

2) Application Proxy applications that use Microsoft Entra Pre-Authentication

3) Applications, which are built on the Microsoft Entra application platform that use OAuth 2.0 / OpenID Connect Authentication after a user or admin has consented to that application. Certain enterprise applications offer more control over who is allowed to sign in.

When user assignment is required, only those users you assign to the application (either through direct user assignment or based on group membership) are able to sign in. They can access the app on the My Apps portal or by using a direct link.

When user assignment is not required, unassigned users don't see the app on their My Apps, but they can still sign in to the application itself (also known as SP-initiated sign-on) or they can use the User Access URL in the application’s Properties page (also known as IDP-initiated sign on).

This setting doesn't affect whether or not an application appears on My Apps. Applications appear on users' My Apps access panels once you've assigned a user or group to the application.

#### NOTE: When an application requires assignment, user consent for that application isn't allowed. This is true even if users consent for that app would have otherwise been allowed. Be sure to grant tenant-wide admin consent to apps that require assignment.

For some applications, the option to require user assignment isn't available in the application's properties. In these cases, you can use PowerShell to set the appRoleAssignmentRequired property on the service principal.

## Determining the user experience for accessing apps

Microsoft Entra ID provides several customizable ways to deploy applications to end users in your organization:

1) Microsoft Entra My Apps

2) Microsoft 365 application launcher

3) Direct sign-on to federated apps (service-pr)

4) Deep links to federated, password-based, or existing apps

## Access to Microsoft applications

Microsoft Applications (like Exchange, SharePoint, Yammer, etc.) are assigned and managed a bit differently than third party SaaS applications or other applications you integrate with Microsoft Entra ID for single sign-on.

There are three main ways that a user can get access to a Microsoft-published application.

1) For applications in the Microsoft 365 or other paid suites, users are granted access through license assignment either directly to their user account, or through a group using our group-based license assignment capability.

2) For applications that Microsoft or a third party publishes freely for anyone to use, users may be granted access through user consent. The users sign in to the application with their Microsoft Entra work or school account and allow it to have access to some limited set of data on their account.

3) For applications that Microsoft or a third party publishes freely for anyone to use, users may also be granted access through administrator consent. This means that an administrator has determined the application may be used by everyone in the organization, so they sign in to the application with a Global Administrator account and grant access to everyone in the organization.

Some applications combine these methods. For example, certain Microsoft applications are part of a Microsoft 365 subscription, but still require consent.

Users can access Microsoft 365 applications through their Office 365 portals. You can also show or hide Microsoft 365 applications in the My Apps with the Office 365 visibility toggle in your directory's User settings.

As with enterprise apps, you can assign users to certain Microsoft applications via the Microsoft Entra admin center or, using PowerShell.

