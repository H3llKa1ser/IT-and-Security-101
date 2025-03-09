# Microsoft Cloud Security Benchmark (MCSB)

## Identity Management and Privileged Access

Identity Management covers controls to establish a secure identity and access controls using identity and access management systems, including the use of single sign-on, strong authentications, managed identities (and service principals) for applications, conditional access, and account anomalies monitoring.

### IM-1: Use centralized identity and authentication system

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| 6.7, 12.5          | AC-2, AC-3, IA-2, IA-8 | 7.2, 8.3           |

Security principle: Use a centralized identity and authentication system to govern your organization's identities and authentications for cloud and non-cloud resources.

Azure guidance: Microsoft Entra ID (Microsoft Entra ID) is Azure's identity and authentication management service. You should standardize on Microsoft Entra ID to govern your organization's identity and authentication in:

1) Microsoft cloud resources, such as Azure Storage, Azure Virtual Machines (Linux and Windows), Azure Key Vault, PaaS, and SaaS applications.

2) Your organization's resources, such as applications on Azure, third-party applications running on your corporate network resources, and third-party SaaS applications.

3) Your enterprise identities in Active Directory by synchronization to Microsoft Entra ID to ensure a consistent and centrally managed identity strategy.

For the Azure services that apply, avoid use of local authentication methods and instead use Microsoft Entra ID to centralize your service authentications.

#### NOTE: As soon as it is technically feasible, you should migrate on-premises Active Directory based applications to Microsoft Entra ID. This could be an Microsoft Entra ID Enterprise Directory, Business to Business configuration, or Business to consumer configuration.

AWS guidance: AWS IAM (Identity and Access Management) is AWS' default identity and authentication management service. Use AWS IAM to govern your AWS identity and access management. Alternatively, through AWS and Azure Single Sign-On (SSO), you can also use Micrsoft Entra ID to manage the identity and access control of AWS to avoid managing duplicate accounts separately in two cloud platforms.

AWS supports Single Sign-On which allows you to bridge your corporate's third party identities (such as Windows Active Directory, or other identity stores) with the AWS identities to avoid creating duplicate accounts to access AWS resources.

GCP guidance: Google Cloud's Identity and Access Management (IAM) system is Google Cloud's default identity and authentication management service used for Google Cloud Identity accounts. Use Google Cloud IAM to govern your GCP identity and access management. Alternatively, through the Google Cloud Identity and Azure Sigle Sign-On (SSO), you can also use Microsoft Entra ID to manage the identity and access control of GCP to avoid managing duplicate accounts separately in a mutli-cloud environment.

Google Cloud Identity is the identity provider for all Google services. It supports Single Sign-On which allows you to bridge your corporate's third party identities (such as Windows Active Directory, or other identity stores) with Google Cloud identities to avoid creating duplicate accounts to access GCP resources.

#### NOTE: Using Google Cloud Directory Sync. Google provides connector tool that integrates with most enterprise LDAP management systems and synchronizes identities on a schedule. By configuring a Cloud Identity account and using Google Cloud Directory Sync, you can configure which of your user accounts – including users, groups , and user profiles, aliases and more – will synchronize on a schedule between your local identity management system and your GCP system.

### IM-2: Protect identity and authentication systems

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| 5.4, 6.5          | AC-2, AC-3, IA-2, IA-8, SI-4 | 8.2, 8.3           |

Security principle: Secure your identity and authentication system as a high priority in your organization's cloud security practice. Common security controls include:

1) Restrict privileged roles and accounts

2) Require strong authentication for all privileged access

3) Monitor and audit high risk activities

Azure guidance: Use the Microsoft Entra ID security baseline and the Microsoft Entra ID Identity Secure Score to evaluate your Microsoft Entra ID identity security posture, and remediate security and configuration gaps. The Microsoft Entra ID Identity Secure Score evaluates Microsoft Entra ID for the following configurations:

1) Use limited administrative roles

2) Turn on user risk policy

3) Designate more than one global admin

4) Enable policy to block legacy authentication

5) Ensure all users can complete multi-factor authentication for secure access

6) Require MFA for administrative roles

7) Enable self-service password reset

8) Do not expire passwords

9) Turn on sign-in risk policy

10) Do not allow users to grant consent to unmanaged applications

Use Microsoft Entra ID Identity Protection to detect, investigate, and remediate identity-based risks. To similarly protect your on-premises Active Directory domain, use Defender for Identity.

#### NOTE: Follow published best practices for all other identity components, including your on-premises Active Directory and any third party capabilities, and the infrastructures (such as operating systems, networks, databases) that host them.

AWS guidance: Use the following security best practices to secure your AWS IAM:

1) Set up AWS account root user access keys for emergency access as described in PA-5 (Set up emergency access).

2) Follow least privilege principles for access assignments.

3) Leverage IAM groups to apply policies instead of individual user(s).

4) Follow strong authentication guidance in IM-6 (Use strong authentication controls) for all users.

5) Use AWS Organizations SCP (Service Control Policy) and permission boundaries.

6) Use IAM Access Advisor to audit service access.

7) Use IAM credential report to track user accounts and credential status.

#### NOTE: Follow published best practices if you have other identity and authentication systems, e.g., follow the Microsoft Entra ID security baseline if you use Microsoft Entra ID to manage AWS identity and access.

GCP guidance: Use the following security best practices to secure to your Google Cloud IAM and Cloud Identity services for your organizations:

1) Set up a super admin account for emergency access by following the recommendations in PA-5 ("Set up emergency access").

2) Create a super admin email address (as the Google Workspace or Cloud Identity super admin account) and this account should be not specific to a particular user in case an emergency recovery is needed.

3) Follow least privilege and separation of duties principles.

4) Avoid using super admin account for daily activities.

5) Leverage Google Cloud Identity groups to apply policies instead of applying policies to individual user(s).

6) Follow strong authentication guidance as described in IM-6 ("Use strong authentication controls") for all users that have elevated privileges.

7) Use IAM policies to restrict access to resources.

8) Use the Organization Policy Service to control and configure constraints on resources.

9) Use IAM audit logging within Cloud Audit logs to review privileged activities.

#### NOTE: Follow published best practices if you have other identity and authentication systems, e.g., follow the Microsoft Entra ID security baseline if you use Microsoft Entra ID to manage GCP identity and access.

### IM-3: Manage application identities securely and automatically

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| N/A          | AC-2, AC-3, IA-4, IA-5, IA-9 | N/A           |

Security principle: Use managed application identities instead of creating human accounts for applications to access resources and execute code. Managed application identities provide benefits such as reducing the exposure of credentials. Automate the rotation of credentials to ensure the security of the identities.

Azure guidance: Use Azure managed identities, which can authenticate to Azure services and resources that support Microsoft Entra ID authentication. Managed identity credentials are fully managed, rotated, and protected by the platform, avoiding hard-coded credentials in source code or configuration files.

For services that don't support managed identities, use Microsoft Entra ID to create a service principal with restricted permissions at the resource level. It is recommended to configure service principals with certificate credentials and fall back to client secrets for authentication.

AWS guidance: Use AWS IAM roles instead of creating user accounts for resources that support this feature. IAM roles are managed by the platform at the backend and the credentials are temporary and rotated automatically. This avoids creating long-term access keys or a username/password for applications and hard-coded credentials in source code or configuration files.

You may use service-linked roles which are attached with pre-defined permission policies for access between AWS services instead of customizing your own role permissions for the IAM roles.

#### NOTE: For services that don't support IAM roles, use access keys but follow the security best practice such as IM-8 Restrict the exposure of credential and secrets to secure your keys.

GCP guidance: Use Google-managed service accounts instead of creating user-managed accounts for resources that support this feature. Google-managed service accounts are managed by the platform at the backend and the service account keys are temporary and rotated automatically. This avoids creating long-term access keys or a username/password for applications and hard-coded hard-coding credentials in source code or configuration files.

Use Policy Intelligence to understand and recognize suspicious activity for service accounts.

### IM-4: Authenticate server and services

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| N/A          | IA-9                           | N/A           |

Security principle: Authenticate remote servers and services from your client side to ensure you are connecting to trusted server and services. The most common server authentication protocol is Transport Layer Security (TLS), where the client-side (often a browser or client device) verifies the server by verifying the server’s certificate was issued by a trusted certificate authority.

#### NOTE: Mutual authentication can be used when both the server and the client authenticate one another.

Azure guidance: Many Azure services support TLS authentication by default. For services that don't support TLS authentication by default, or support disabling TLS, ensure it is always enabled to support the server/client authentication. Your client application should also be designed to verify server/client identity (by verifying the server’s certificate issued by a trusted certificate authority) in the handshake stage.

Services such as API Management and API Gateway supports TLS mutual authentication.

AWS guidance: Many AWS services support TLS authentication by default. For services that don't support TLS authentication by default, or support disabling TLS, ensure it is always enabled to support the server/client authentication. Your client application should also be designed to verify server/client identity (by verifying the server’s certificate issued by a trusted certificate authority) in the handshake stage.

#### NOTE: Services such as API Gateway supports TLS mutual authentication.

GCP guidance: Many GCP services support TLS authentication by default. For services that don't support this by default or support disabling TLS, ensure it is always enabled to support the server/client authentication. Your client application should also be designed to verify server/client identity (by verifying the server’s certificate issued by a trusted certificate authority) in the handshake stage.

#### NOTE: Services such as Cloud Load Balancing support TLS mutual authentication.

### IM-5: Use single sign-on (SSO) for application access

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
|  12.5          | IA-2, IA-4, IA-8 | N/A           |


Security principle: Use single sign-on (SSO) to simplify the user experience for authenticating to resources including applications and data across cloud services and on-premises environments.

Azure guidance: Use Microsoft Entra ID for workload application access (customer facing) access through Microsoft Entra ID single sign-on (SSO), reducing the need for duplicate accounts. Microsoft Entra ID provides identity and access management to Azure resources (in the management plane, including CLI, PowerShell, the portal), cloud applications, and on-premises applications.

Microsoft Entra ID also supports SSO for enterprise identities such as corporate user identities, as well as external user identities from trusted third-party and public users.

AWS guidance: Use AWS Cognito to manage acccess to your customer-facing applications workloads through single sign-on (SSO) to allow customers to bridge their third-party identities from different identity providers.

For SSO access to the AWS native resources (including AWS console access or service management and data plane level access), use AWS Single Sign-On to reduce the need for duplicate accounts.

AWS SSO also allows you to bridge corporate identities (such as identities from Microsoft Entra ID) with AWS identities, as well as external user identities from trusted third-party and public users.

GCP guidance: Use Google Cloud Identity to manage access to your customer facing workload application through Google Cloud Identity Single Sign-On, reducing the need for duplicate accounts. Google Cloud Identity provides identity and access management to GCP (in the management plane including Google Cloud CLI, Console access), cloud applications, and on-premises applications.

Google Cloud Identity also supports SSO for enterprise identities such as corporate user identities from Microsoft Entra ID or Active Directory, as well as external user identities from trusted third-party and public users. GCP implementation and additional context:

### IM-6: Use strong authentication controls

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| 6.3, 6.4          | AC-2, AC-3, IA-2, IA-5, IA-8 | 7.2, 8.2, 8.3, 8.4           |

Security principle: Enforce strong authentication controls (strong passwordless authentication or multi-factor authentication) with your centralized identity and authentication management system for all access to resources. Authentication based on password credentials alone is considered legacy, as it is insecure and does not stand up to popular attack methods.

When deploying strong authentication, configure administrators and privileged users first, to ensure the highest level of the strong authentication method, quickly followed by rolling out the appropriate strong authentication policy to all users.

#### NOTE: If legacy password-based authentication is required for legacy applications and scenarios, ensure password security best practices such as complexity requirements, are followed.

Azure guidance: Microsoft Entra ID supports strong authentication controls through passwordless methods and multi-factor authentication (MFA).

1) Passwordless authentication: Use passwordless authentication as your default authentication method. There are three options available in passwordless authentication: Windows Hello for Business, Microsoft Authenticator app phone sign-in, and FIDO2 security keys. In addition, customers can use on-premises authentication methods such as smart cards.

2) Multi-factor authentication: Azure MFA can be enforced on all users, select users, or at the per-user level based on sign-in conditions and risk factors. Enable Azure MFA and follow Microsoft Defender for Cloud identity and access management recommendations for your MFA setup.

If legacy password-based authentication is still used for Microsoft Entra ID authentication, be aware that cloud-only accounts (user accounts created directly in Azure) have a default baseline password policy. And hybrid accounts (user accounts that come from on-premises Active Directory) follow the on-premises password policies.

For third-party applications and services that may have default IDs and passwords, you should disable or change them during initial service setup.

AWS guidance: AWS IAM supports strong authentication controls through multi-factor authentication (MFA). MFA can be enforced on all users, select users, or at the per-user level based on defined conditions.

If you use corporate accounts from a third-party directory (such as Windows Active Directory) with AWS identities, follow the respective security guidance to enforce strong authentication. Refer to the Azure Guidance for this control if you use Microsoft Entra ID to manage AWS access.

#### NOTE: For third-party applications and AWS services that may have default IDs and passwords, you should disable or change them during initial service setup.

GCP guidance: Google Cloud Identity supports strong authentication controls through multi-factor authentication (MFA). MFA can be enforced on all users, select users, or at the per-user level based on defined conditions. To protect Cloud Identity (and Workspace) super admin accounts, consider using security keys and the Google Advanced Protection Program for maximum security.

If you use corporate accounts from a third-party directory (such as Windows Active Directory) with Google Cloud identities, follow the respective security guidance to enforce strong authentication. Refer to the Azure Guidance for this control if you use Microsoft Entra ID to manage Google Cloud access.

Use Identity-Aware Proxy to establish a central authorization layer for applications accessed by HTTPS, so you can use an application-level access control model instead of relying on network-level firewalls.

#### NOTE: For third-party applications and GCP services that may have default IDs and passwords, you should disable or change them during the initial service setup.

### IM-7: Restrict resource access based on conditions

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------|---------------------|
| 3.3, 6.4, 13.5         | AC-2, AC-3, AC-6 | 7.2           |

Security principle: Explicitly validate trusted signals to allow or deny user access to resources, as part of a zero-trust access model. Signals to validate should include strong authentication of user account, behavioral analytics of user account, device trustworthiness, user or group membership, locations and so on.

Azure guidance: Use Microsoft Entra ID conditional access for more granular access controls based on user-defined conditions, such as requiring user logins from certain IP ranges (or devices) to use MFA. Microsoft Entra ID Conditional Access allows you to enforce access controls on your organization’s apps based on certain conditions.

Define the applicable conditions and criteria for Microsoft Entra ID conditional access in the workload. Consider the following common use cases:

1) Requiring multi-factor authentication for users with administrative roles.

2) Requiring multi-factor authentication for Azure management tasks.

3) Blocking sign-ins for users attempting to use legacy authentication protocols.

4) Requiring trusted locations for Microsoft Entra ID Multi-Factor Authentication registration.

5) Blocking or granting access from specific locations.

6) Blocking risky sign-in behaviors.

7) Requiring organization-managed devices for specific applications.

#### NOTE: Granular authentication session management controls can also be implemented through Microsoft Entra ID conditional access policy, such as sign-in frequency and persistent browser session.

AWS guidance: Create IAM policy and define conditions for more granular access controls based on user-defined conditions, such as requiring user logins from certain IP ranges (or devices) to use multi-factor authentication. Condition settings may include single or multiple conditions as well as logics.

Policies can be defined from six different dimensions: identity-based policies, resource-based policies, permissions boundaries, AWS Organizations service control policy (SCP) , Access Control Lists(ACL), and session policies.

GCP guidance: Create and define IAM Conditions for more granular attribute-based access controls based on user-defined conditions, such as requiring user logins from certain IP ranges (or devices) to use multi-factor authentication. Condition settings may include single or multiple conditions as well as logic.

Conditions are specified in the role bindings of a resource's allow policy. Condition attributes are based on the requested resource—for example, its type or name—or on details about the request—for example, its timestamp or destination IP address.

