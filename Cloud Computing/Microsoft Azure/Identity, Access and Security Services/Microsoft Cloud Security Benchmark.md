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
| N/A          | IA-9 | N/A           |
