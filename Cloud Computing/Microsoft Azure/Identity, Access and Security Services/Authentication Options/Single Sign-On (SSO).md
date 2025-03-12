# Single Sign-On (SSO)

Single sign-on is an authentication method that allows users to sign in using one set of credentials to multiple independent software systems. Using SSO means a user doesn't have to sign in to every application they use. With SSO, users can access all needed applications without being required to authenticate using different credentials.

Many applications already exist in Microsoft Entra ID that you can use with SSO. You have several options for SSO depending on the needs of the application and how it's implemented. Take time to plan your SSO deployment before you create applications in Microsoft Entra ID. The management of applications can be made easier by using the My Apps portal.

## SSO Options

Choosing an SSO method depends on how the application is configured for authentication. Cloud applications can use federation-based options, such as OpenID Connect, Open Authorization (OAuth), and Security Assertion Markup Language (SAML). The application can also use password-based SSO, linked-based SSO, or SSO can be disabled.

1) Federation

When you set up SSO to work between multiple identity providers, it's called federation. An SSO implementation based on federation protocols improves security, reliability, end-user experiences, and implementation.

With federated single sign-on, Microsoft Entra authenticates the user to the application by using their Microsoft Entra account. This method is supported for SAML 2.0, Web Services Federation (WS-Federation), or OpenID Connect applications. Federated SSO is the richest mode of SSO. Use federated SSO with Microsoft Entra ID when an application supports it, instead of password-based SSO and Active Directory Federation Services (AD FS).

There are some scenarios where the SSO option isn't present for an enterprise application. If the application was registered using App registrations in the portal, then the single sign-on capability is configured to use OpenID Connect and OAuth by default. In this case, the single sign-on option doesn't appear in the navigation under enterprise applications.

Single sign-on isn't available when an application is hosted in another tenant. Single sign-on is also not available if your account doesn't have the required permissions (Global Administrator, Cloud Application Administrator, Application Administrator, or owner of the service principal). Permissions can also cause a scenario where you can open single sign-on but might not be able to save.

2) Password

On-premises applications can use a password-based method for SSO. This choice works when applications are configured for Application Proxy.

With password-based SSO, users sign in to the application with a username and password the first time they access it. After the first sign-on, Microsoft Entra ID provides the username and password to the application. Password-based SSO enables secure application password storage and replay using a web browser extension or mobile app. This option uses the existing sign-in process provided by the application, enables an administrator to manage the passwords, and doesn't require the user to know the password.

3) Linked

Linked sign-on can provide a consistent user experience while you migrate applications over a period of time. If you're migrating applications to Microsoft Entra ID, you can use linked-based SSO to quickly publish links to all the applications you intend to migrate. Users can find all the links in the My Apps or Microsoft 365 portals.

After a user has authenticated with a linked application, an account needs to be created before the user is provided single sign-on access. Provisioning this account can either occur automatically, or it can occur manually by an administrator. You can't apply Conditional Access policies or multifactor authentication to a linked application because a linked application doesn't provide single sign-on capabilities through Microsoft Entra ID. When you configure a linked application, you're simply adding a link that appears for launching the application.

4) Disabled

When SSO is disabled, it isn't available for the application. When single sign-on is disabled, users might need to authenticate twice. First, users authenticate to Microsoft Entra ID, and then they sign in to the application.

Disable SSO when:

1) You're not ready to integrate this application with Microsoft Entra single sign-on

2) You're testing other aspects of the application

3) An on-premises application doesn't require users to authenticate, but you want them to. With SSO disabled, the user needs to authenticate.

4) If you configured the application for SP-initiated SAML-based SSO and you change the SSO mode to disabled, it doesn't stop users from signing in to the application outside the My Apps portal. To stop users from signing in from outside My Apps portal, you need to disable the ability for users to sign in.

## Plan SSO deployment

Web applications are hosted by various companies and made available as a service. Some popular examples of web applications include Microsoft 365, GitHub, and Salesforce. There are thousands of others. People access web applications using a web browser on their computer. Single sign-on makes it possible for people to navigate between the various web applications without having to sign in multiple times. For more information, see Plan a single sign-on deployment.

How you implement SSO depends on where the application is hosted. Hosting matters because of the way network traffic is routed to access the application. Users don't need to use the Internet to access on-premises applications (hosted on a local network). If the application is hosted in the cloud, users need the Internet to use it. Cloud hosted applications are also called Software as a Service (SaaS) applications.

For cloud applications, federation protocols are used. You can also use single sign-on for on-premises applications. You can use Application Proxy to configure access for your on-premises application.

## My Apps

If you're a user of an application, you likely don't care much about SSO details. You just want to use the applications that make you productive without having to type your password so much. You can find and manage your applications at the My Apps portal.

## SSO Implementation

When you plan your SSO deployment with your applications in Microsoft Entra ID, you need to consider the following questions:

1) What are the administrative roles required for managing the application?

2) Does the Security Assertion Markup Language (SAML) application certificate need to be renewed?

3) Who needs to be notified of changes related to the implementation of SSO?

4) What licenses are needed to ensure effective management of the application?

5) Are shared and guest user accounts used to access the application?

6) Do I understand the options for SSO deployment?

### Administrative roles

Always use the role with the fewest permissions available to accomplish the required task within Microsoft Entra ID. Review the different roles that are available and choose the right one to solve your needs for each persona for the application. Some roles may need to be applied temporarily and removed after the deployment has been completed.

| Persona                  | Roles                                                         | Microsoft Entra role (if necessary)      |
|--------------------------|--------------------------------------------------------------|------------------------------------------|
| Help desk admin         | Tier 1 support, view the sign-in logs to resolve issues.     | None                                     |
| Identity admin          | Configure and debug when issues involve Microsoft Entra ID.  | Cloud Application Administrator         |
| Application admin       | User attestation in application, configuration on users with permissions. | None |
| Infrastructure admins   | Certificate rollover owner.                                  | Cloud Application Administrator         |
| Business owner/stakeholder | User attestation in application, configuration on users with permissions. | None |

### Certificate

When you enable federation on SAML application, Microsoft Entra ID creates a certificate that is by default valid for three years. You can customize the expiration date for that certificate if needed. Ensure that you have processes in place to renew certificates prior to their expiration.

You change that certificate duration in the Microsoft Entra admin center. Make sure to document the expiration and know how you'll manage your certificate renewal. It’s important to identify the right roles and email distribution lists involved with managing the lifecycle of the signing certificate. The following roles are recommended:

1) Owner for updating user properties in the application.

2) Owner On-Call for application troubleshooting support.

3) Closely monitored email distribution list for certificate-related change notifications.

Set up a process for how you'll handle a certificate change between Microsoft Entra ID and your application. By having this process in place, you can help prevent or minimize an outage due to a certificate expiring or a forced certificate rollover.

### Communications

Communication is critical to the success of any new service. Proactively communicate to your users about how their experience will change. Communicate when it will change, and how to gain support if they experience issues. Review the options for how users will access their SSO-enabled applications, and craft your communications to match your selection.

Implement your communication plan. Make sure you were letting your users know that a change is coming, when it has arrived, and what to do now. Also, make sure that you provide information about how to seek assistance.

### Licensing

Ensure the application is covered by the following licensing requirements:

1) Microsoft Entra licensing - SSO for pre-integrated enterprise applications is free. However, the number of objects in your directory and the features you wish to deploy may require more licenses.

2) Application licensing - You'll need the appropriate licenses for your applications to meet your business needs. Work with the application owner to determine whether the users assigned to the application have the appropriate licenses for their roles within the application. If Microsoft Entra ID manages the automatic provisioning based on roles, the roles assigned in Microsoft Entra ID must align with the number of licenses owned within the application. Improper number of licenses owned in the application may lead to errors during the provisioning or updating of a user account.

 ### Shared Accounts

 From the sign-in perspective, applications with shared accounts aren't different from enterprise applications that use password SSO for individual users. However, there are more steps required when planning and configuring an application meant to use shared accounts.

1) Work with users to document the following information:

The set of users in the organization who will use the application.
The existing set of credentials in the application associated with the set of users.

2) For each combination of user set and credentials, create a security group in the cloud or on-premises based on your requirements.

3) Reset the shared credentials. After the application is deployed in Microsoft Entra ID, individuals don't need the password of the shared account. Microsoft Entra ID stores the password and you should consider setting it to be long and complex.

4) Configure automatic rollover of the password if the application supports it. That way, not even the administrator who did the initial setup knows the password of the shared account.

## SSO Options

There are several ways you can configure an application for SSO. Choosing an SSO method depends on how the application is configured for authentication.

1) Cloud applications can use OpenID Connect, OAuth, SAML, password-based, or linked for SSO. Single sign-on can also be disabled.

2) On-premises applications can use password-based, Integrated Windows Authentication, header-based, or linked for SSO. The on-premises choices work when applications are configured for Application Proxy.

This flowchart can help you decide which SSO method is best for your situation.

![image](https://github.com/user-attachments/assets/0d0a5824-aacc-4493-bd27-f8349b7ab334)

## SSO Protocols

1) OpenID Connect and OAuth - Choose OpenID Connect and OAuth 2.0 if the application you're connecting to supports it.

2) SAML - Choose SAML whenever possible for existing applications that don't use OpenID Connect or OAuth.

3) Password-based - Choose password-based when the application has an HTML sign-in page. Password-based SSO is also known as password vaulting. Password-based SSO enables you to manage user access and passwords to web applications that don't support identity federation. It's also useful where several users need to share a single account, such as to your organization's social media app accounts. Password-based SSO supports applications that require multiple sign-in fields for applications that require more than just username and password fields to sign in. You can customize the labels of the username and password fields your users see on My Apps when they enter their credentials.

4) Linked - Choose linked when the application is configured for SSO in another identity provider service. The linked option lets you configure the target location when a user selects the application in your organization's end user portals. You can add a link to a custom web application that currently uses federation, such as Microsoft Entra Domain Federation Services. You can also add links to specific web pages that you want to appear on your user's access panels and to an app that doesn't require authentication. The Linked option doesn't provide sign-on functionality through Microsoft Entra credentials.

5) Disabled - Choose disabled SSO when the application isn't ready to be configured for SSO.

6) Integrated Windows Authentication (IWA) - Choose IWA single sign-on for applications that use IWA, or for claims-aware applications.

7) Header-based - Choose header-based single sign-on when the application uses headers for authentication.

