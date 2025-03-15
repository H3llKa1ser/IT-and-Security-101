# Recommend when to use and configure a Microsoft Entra Application Proxy, including authentication

Microsoft Entra application proxy is a secure and cost-effective remote access solution for on-premises applications. It provides an immediate transition path for “Cloud First” organizations to manage access to legacy on-premises applications that aren’t yet capable of using modern protocols.

Application Proxy is recommended for giving remote users access to internal resources. Application Proxy replaces the need for a VPN or reverse proxy for these remote access use cases. It isn't intended for users who are on the corporate network. These users who use Application Proxy for intranet access may experience undesirable performance issues.

## Prerequisites

You need to meet the following prerequisites before beginning your implementation. You can see more information on setting up your environment, including these prerequisites, in this tutorial.

1) Connectors: Connectors are lightweight agents that you can deploy onto:

Physical hardware on-premises

A VM hosted within any hypervisor solution

A VM hosted in Azure to enable outbound connection to the Application Proxy service.

2) Microsoft Entra application proxy Connectors.

Connector machines must be enabled for TLS 1.2 before installing the connectors.

If possible, deploy connectors in the same network and segment as the back-end web application servers. It's best to deploy connectors after you complete a discovery of applications.

We recommend that each connector group has at least two connectors to provide high availability and scale. Having three connectors is optimal in case you may need to service a machine at any point. Review the connector capacity table to help with deciding what type of machine to install connectors on. The larger the machine the more buffer and performant the connector will be.

3) Network access settings: Microsoft Entra application proxy connectors connect to Azure via HTTPS (TCP Port 443) and HTTP (TCP Port 80).

Terminating connector TLS traffic isn't supported and will prevent connectors from establishing a secure channel with their respective Azure App Proxy endpoints.

Avoid all forms of inline inspection on outbound TLS communications between connectors and Azure. Internal inspection between a connector and backend applications is possible, but could degrade the user experience, and as such, isn't recommended.

Load balancing of the connectors themselves is also not supported, or even necessary.

## Important considerations before configuring Microsoft Entra application proxy

The following core requirements must be met in order to configure and implement Microsoft Entra application proxy.

1) Azure onboarding: Before deploying application proxy, user identities must be synchronized from an on-premises directory or created directly within your Microsoft Entra tenants. Identity synchronization allows Microsoft Entra ID to pre-authenticate users before granting them access to App Proxy published applications and to have the necessary user identifier information to perform single sign-on (SSO).

2) Conditional Access requirements: We don't recommend using Application Proxy for intranet access because this adds latency that will impact users. We recommend using Application Proxy with pre-authentication and Conditional Access policies for remote access from the internet. An approach to provide Conditional Access for intranet use is to modernize applications so they can directly authenticate with Microsoft Entra ID. Refer to Resources for migrating applications to Microsoft Entra ID for more information.

3) Service limits: To protect against overconsumption of resources by individual tenants, there are throttling limits set per application and tenant. To see these limits refer to Microsoft Entra service limits and restrictions. These throttling limits are based on a benchmark far above typical usage volume and provide ample buffer for a majority of deployments.

4) Public certificate: If you're using custom domain names, you must procure a TLS/SSL certificate. Depending on your organizational requirements, getting a certificate can take some time and we recommend beginning the process as early as possible. Azure Application Proxy supports standard, wildcard, or SAN-based certificates. For more details, see Configure custom domains with Microsoft Entra application proxy.

5) Domain requirements: Single sign-on to your published applications using Kerberos Constrained Delegation (KCD) requires that the server running the Connector and the server running the app are domain joined and part of the same domain or trusting domains. For detailed information on the topic, see KCD for single sign-on with Application Proxy. The connector service runs in the context of the local system and shouldn't be configured to use a custom identity.

6) DNS records for URLs

Before using custom domains in Application Proxy you must create a CNAME record in public DNS, allowing clients to resolve the custom defined external URL to the pre-defined Application Proxy address. Failing to create a CNAME record for an application that uses a custom domain prevents remote users from connecting to the application. Steps required to add CNAME records can vary from DNS provider to provider, so learn how to manage DNS records and record sets by using the Microsoft Entra admin center.

Similarly, connector hosts must be able to resolve the internal URL of applications being published.

7) Administrative rights and roles

Connector installation requires local admin rights to the Windows server that it's being installed on. It also requires a minimum of an Application Administrator role to authenticate and register the connector instance to your Microsoft Entra tenant.
Application publishing and administration require the Application Administrator role. Application Administrators can manage all applications in the directory including registrations, SSO settings, user and group assignments and licensing, Application Proxy settings, and consent. It doesn't grant the ability to manage Conditional Access. The Cloud Application Administrator role has all the abilities of the Application Administrator, except that it doesn't allow management of Application Proxy settings.

8) Licensing: Application Proxy is available through a Microsoft Entra ID P1 or P2 subscription.

## Application Discovery

Compile an inventory of all in-scope applications that are being published via application proxy by collecting the following information:

| **Information Type**      | **Information to Collect** |
|---------------------------|----------------------------|
| **Service Type**          | For example: SharePoint, SAP, CRM, Custom Web Application, API |
| **Application Platform**  | For example: Windows IIS, Apache on Linux, Tomcat, NGINX |
| **Domain Membership**     | Web server’s fully qualified domain name (FQDN) |
| **Application Location**  | Where the web server or farm is located in your infrastructure |
| **Internal Access**       | The exact URL used when accessing the application internally. <br> If a farm, what type of load balancing is in use? <br> Whether the application draws content from sources other than itself. <br> Determine if the application operates over WebSockets. |
| **External Access**       | The vendor solution that the application may already be exposed through, externally. <br> The URL you want to use for external access. If SharePoint, ensure Alternate Access. |
| **Public Certificate**    | If using a custom domain, procure a certificate with a corresponding subject name. If a certificate exists, note the serial number and location from where it can be obtained. |
| **Authentication Type**   | The type of authentication supported by the application such as Basic, Windows Integration Authentication, forms-based, header-based, and claims. <br> If the application is configured to run under a specific domain account, note the Fully Qualified Domain Name (FQDN) of the service account. <br> If SAML-based, the identifier and reply URLs. <br> If header-based, the vendor solution and specific requirement for handling authentication type. |
| **Connector Group Name**  | The logical name for the group of connectors that will be designated to provide the conduit and SSO to this backend application. |
| **Users/Groups Access**   | The users or user groups that will be granted external access to the application. |
| **Additional Requirements** | Note any additional remote access or security requirements that should be factored into publishing the application. |

## Define organizational requirements

The following are areas for which you should define your organization’s business requirements. Each area contains examples of requirements

1) Access

Remote users with domain-joined or Microsoft Entra joined devices can access published applications securely with seamless single sign-on (SSO).

Remote users with approved personal devices can securely access published applications provided they're enrolled in MFA and have registered the Microsoft Authenticator app on their mobile phone as an authentication method.

2) Governance

Administrators can define and monitor the lifecycle of user assignments to applications published through application proxy.

3) Security

Only users assigned to applications via group membership or individually can access those applications.

4) Performance

There's no degradation of application performance compared to accessing application from the internal network.

5) User Experience

Users are aware of how to access their applications by using familiar company URLs on any device platform.

6) Auditing

Administrators are able to audit user access activity.

## Best practices for a pilot

Determine the amount of time and effort needed to fully commission a single application for remote access with Single sign-on (SSO). Do so by running a pilot that considers its initial discovery, publishing, and general testing. Using a simple IIS-based web application that is already preconfigured for integrated Windows authentication (IWA) would help establish a baseline, as this setup requires minimal effort to successfully pilot remote access and SSO.

The following design elements should increase the success of your pilot implementation directly in a production tenant.

1) Connector management

Connectors play a key role in providing the on-premises conduit to your applications. Using the Default connector group is adequate for initial pilot testing of published applications before commissioning them into production. Successfully tested applications can then be moved to production connector groups.

2) Application management

Your workforce is most likely to remember an external URL is familiar and relevant. Avoid publishing your application using our pre-defined msappproxy.net or onmicrosoft.com suffixes. Instead, provide a familiar top-level verified domain, prefixed with a logical hostname such as intranet.<customers_domain>.com.

Restrict visibility of the pilot application’s icon to a pilot group by hiding its launch icon from the Azure MyApps portal. When ready for production you can scope the app to its respective targeted audience, either in the same pre-production tenant, or by also publishing the application in your production tenant.

3) Single Sign-On settings

Some SSO settings have specific dependencies that can take time to set up, so avoid change control delays by ensuring dependencies are addressed ahead of time. This includes domain joining connector hosts to perform SSO using Kerberos Constrained Delegation (KCD) and taking care of other time-consuming activities.

4) TLS between connector host and target application

Security is paramount, so TLS between the connector host and target applications should always be used. Particularly if the web application is configured for forms-based authentication (FBA), as user credentials are then effectively transmitted in clear text.

5) Implement incrementally and test each step

Conduct basic functional testing after publishing an application to ensure that all user and business requirements are met by following the directions below:

Test and validate general access to the web application with pre-authentication disabled.

If successful enable pre-authentication and assign users and groups. Test and validate access.

Then add the SSO method for your application and test again to validate access.

Apply Conditional Access and MFA policies as required. Test and validate access.

6) Troubleshooting tools

When troubleshooting, always start by validating access to the published application from the browser on the connector host, and confirm that the application functions as expected. The simpler your setup, the easier to determine root cause, so consider trying to reproduce issues with a minimal configuration such as using only a single connector and no SSO. In some cases, web debugging tools such as Telerik’s Fiddler can prove indispensable to troubleshoot access or content issues in applications accessed through a proxy. Fiddler can also act as a proxy to help trace and debug traffic for mobile platforms such as iOS and Android, and virtually anything that can be configured to route via a proxy.

## Deploy application proxy

