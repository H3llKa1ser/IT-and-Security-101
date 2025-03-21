# Microsoft Cloud Security Benchmark

## Security Control: Asset management

Asset Management covers controls to ensure security visibility and governance over your resources, including recommendations on permissions for security personnel, security access to asset inventory, and managing approvals for services and resources (inventory, track, and correct).

### AM-1: Track asset inventory and their risks

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 1.1, 1.5, 2.1, 2.4  | CM-8, PM-5           | 2.4                |

Security principle: Track your asset inventory by query and discover all your cloud resources. Logically organize your assets by tagging and grouping your assets based on their service nature, location, or other characteristics. Ensure your security organization has access to a continuously updated inventory of assets.

Ensure your security organization can monitor the risks to cloud assets by always having security insights and risks aggregated centrally.

Azure guidance: The Microsoft Defender for Cloud inventory feature and Azure Resource Graph can query for and discover all resources in your subscriptions, including Azure services, applications, and network resources. Logically organize assets according to your organization's taxonomy using tags as well as other metadata in Azure (Name, Description, and Category).

Ensure that security organizations have access to a continuously updated inventory of assets on Azure. Security teams often need this inventory to evaluate their organization's potential exposure to emerging risks, and as an input for continuous security improvements.

Ensure security organizations are granted Security Reader permissions in your Azure tenant and subscriptions so they can monitor for security risks using Microsoft Defender for Cloud. Security Reader permissions can be applied broadly to an entire tenant (Root Management Group) or scoped to management groups or specific subscriptions.

#### NOTE: Additional permissions might be required to get visibility into workloads and services.

GCP guidance: Use Google Cloud Asset Inventory to provide inventory services based on a time series database. This database keeps a five-week history of GCP asset metadata. The Cloud Asset Inventory export service allows you to export all asset metadata at a certain timestamp or export event change history during a timeframe.

Additionally, Google Cloud Security Command Center supports a different naming convention. Assets are an organization’s Google Cloud resources. The IAM roles for Security Command Center can be granted at the organization, folder, or project level. Your ability to view, create, or update findings, assets, and security sources depends on the level for which you are granted access.

AWS guidance: Use the AWS Systems Manager Inventory feature to query for and discover all resources in your EC2 instances, including application level and operating system level details. In addition, use AWS Resource Groups - Tag Editor to browse AWS resource inventories.

Logically organize assets according to your organization's taxonomy using tags as well as other metadata in AWS (Name, Description, and Category).

Ensure that security organizations have access to a continuously updated inventory of assets on AWS. Security teams often need this inventory to evaluate their organization's potential exposure to emerging risks, and as an input for continuous security improvements.

#### NOTE: Additional permissions might be required to get visibility into workloads and services.

GCP guidance: Use Google Cloud Organization Policy Service to audit and restrict which services users can provision in your environment. You can also use Cloud Monitoring in Operations Suite and/or Organization Policy to create rules to trigger alerts when a non-approved service is detected.

### AM-2: Use only approved services

| CIS Controls v8 ID(s)  | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|-----------------------|----------------------|--------------------|
| 2.5, 2.6, 2.7, 4.8   | CM-8, PM-5           | 6.3                |

Security principle: Ensure that only approved cloud services can be used, by auditing and restricting which services users can provision in the environment.

Azure guidance: Use Azure Policy to audit and restrict which services users can provision in your environment. Use Azure Resource Graph to query for and discover resources within their subscriptions. You can also use Azure Monitor to create rules to trigger alerts when a non-approved service is detected.

AWS guidance: Use AWS Config to audit and restrict which services users can provision in your environment. Use AWS Resource Groups to query for and discover resources within their accounts. You can also use CloudWatch and/or AWS Config to create rules to trigger alerts when a non-approved service is detected.

GCP guidance: Establish or update security policies/process that address asset lifecycle management processes for potentially high impact modifications. These modifications include changes to identity providers and access, sensitive data, network configuration, and administrative privilege assessment. Use Google Cloud Security Command Center and check Compliance tab for assets at risk.

Additionally, use Automated Cleanup of Unused Google Cloud Projects, and Cloud Recommender service to provide recommendations and insights for using resources on Google Cloud. These recommendations and insights are per-product or per-service, and are generated based on heuristic methods, machine learning, and current resource usage.

### AM-3: Ensure security of asset lifecycle management

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 1.1, 2.1           | CM-8, CM-7           | 2.4                |

Security principle: Ensure security attributes or configurations of the assets are always updated during the asset lifecycle.

Azure guidance: Establish or update security policies/process that address asset lifecycle management processes for potentially high impact modifications. These modifications include changes to identity providers and access, data sensitivity level, network configuration, and administrative privilege assignment.

Identify and remove Azure resources when they are no longer needed.

AWS guidance: Establish or update security policies/process that address asset lifecycle management processes for potentially high impact modifications. These modifications include changes to identity providers and access, data sensitivity level, network configuration, and administrative privilege assignment.

Identify and remove AWS resources when they are no longer needed.

GCP guidance: Use Google Cloud Identity and Access Management (IAM) to restrict access to specific resource. You can specify allow or deny actions as well as conditions under which actions are triggered. You can specify one condition or combined methods of resource-level permissions, resource based policies, tag-based authorization, temporary credentials, or service-linked roles to have fine-grain control access controls for your resources.

Additionally, you can use VPC Service Controls to protect against accidental or targeted action by external entities or insiders entities, which helps to minimize unwarranted data exfiltration risks from Google Cloud services. You can use VPC Service Controls to create perimeters that protect the resources and data of services that you explicitly specify.

### AM-4: Limit access to asset management

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 3.3                  | AC-3                 | N/A                |

Security principle: Limit users' access to asset management features, to avoid accidental or malicious modification of the assets in your cloud.

Azure guidance: Azure Resource Manager is the deployment and management service for Azure. It provides a management layer that enables you to create, update, and delete resources (assets) in Azure. Use Azure AD Conditional Access to limit users' ability to interact with Azure Resource Manager by configuring "Block access" for the "Microsoft Azure Management" App.

Use Azure Role-based Access Control (Azure RBAC) to assign roles to identities to control their permissions and access to Azure resources. For example, a user with only the 'Reader' Azure RBAC role can view all resources, but is not allowed to make any changes.

Use Resource Locks to prevent either deletions or modifications to resources. Resource Locks may also be administered through Azure Blueprints.

AWS guidance: Use AWS IAM to restrict access to a specific resource. You can specify allowed or deny actions as well as the conditions under which actions are triggered. You may specify one condition or combine methods of resource-level permissions, resource-based policies, tag-based authorization, temporary credentials, or service-linked roles to have a fine-grain control access control for your resources.

GCP guidance: Use Google Cloud VM Manager to discover the applications installed on Compute Engines instances. OS inventory and configuration management can be used ensure that non-authorized software is blocked from executing on Compute Engine instances.

You can also use a third-party solution to discover and identify unapproved software.

### AM-5: Use only approved applications in virtual machine

| CIS Controls v8 ID(s)  | NIST SP 800-53 r4 ID(s)         | PCI-DSS ID(s) v3.2.1 |
|-----------------------|--------------------------------|--------------------|
| 2.5, 2.6, 2.7, 4.8   | CM-8, CM-7, CM-10, CM-11      | 6.3                |

Security principle: Ensure that only authorized software executes by creating an allow list and block the unauthorized software from executing in your environment.

Azure guidance: Use Microsoft Defender for Cloud adaptive application controls to discover and generate an application allow list. You can also use ASC adaptive application controls to ensure that only authorized software can executes, and all unauthorized software is blocked from executing on Azure Virtual Machines.

Use Azure Automation Change Tracking and Inventory to automate the collection of inventory information from your Windows and Linux VMs. Software name, version, publisher, and refresh time information are available from the Azure portal. To get the software installation date and other information, enable guest-level diagnostics and direct the Windows Event Logs to a Log Analytics workspace.

Depending on the type of scripts, you can use operating system-specific configurations or third-party resources to limit users' ability to execute scripts in Azure compute resources.

You can also use a third-party solution to discover and identify unapproved software.

AWS guidance: Use the AWS Systems Manager Inventory feature to discover the applications installed in your EC2 instances. Use AWS Config rules to ensure that non-authorized software is blocked from executing on EC2 instances.

You can also use a third-party solution to discover and identify unapproved software.

## Security Control: Backup and recovery

Backup and Recovery covers controls to ensure that data and configuration backups at the different service tiers are performed, validated, and protected.

### BR-2: Protect backup and recovery data

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 11.3                 | CP-6, CP-9           | 3.4                |

Security principle: Ensure backup data and operations are protected from data exfiltration, data compromise, ransomware/malware and malicious insiders. The security controls that should be applied include user and network access control, data encryption at-rest and in-transit.

Azure guidance: Use multi-factor authentication and Azure RBAC to secure the critical Azure Backup operations (such as delete, change retention, updates to backup config). For Azure Backup supported resources, use Azure RBAC to segregate duties and enable fine grained access, and create private endpoints within your Azure Virtual Network to securely backup and restore data from your Recovery Services vaults.

For Azure Backup supported resources, backup data is automatically encrypted using Azure platform-managed keys with 256-bit AES encryption. You can also choose to encrypt the backups using a customer managed key. In this case, ensure the customer-managed key in the Azure Key Vault is also in the backup scope. If you use a customer-managed key, use soft delete and purge protection in Azure Key Vault to protect keys from accidental or malicious deletion. For on-premises backups using Azure Backup, encryption-at-rest is provided using the passphrase you provide.

Safeguard backup data from accidental or malicious deletion, such as ransomware attacks/attempts to encrypt or tamper backup data. For Azure Backup supported resources, enable soft delete to ensure recovery of items with no data loss for up to 14 days after an unauthorized deletion, and enable multi-factor authentication using a PIN generated in the Azure portal. Also enable geo-redundant storage or cross-region restoration to ensure backup data is restorable when there is a disaster in primary region. You can also enable Zone-redundant Storage (ZRS) to ensure backups are restorable during zonal failures.

#### NOTE: If you use a resource's native backup feature or backup services other than Azure Backup, refer to the Microsoft Cloud Security Benchmark (and service baselines) to implement the above controls.

AWS guidance: Use AWS IAM access control to secure AWS Backup. This includes securing the AWS Backup service access and backup and restore points. Example controls include:

Use multi-factor authentication (MFA) for critical operations such as deletion of a backup/restore point.

Use Secure Sockets Layer (SSL)/Transport Layer Security (TLS) to communicate with AWS resources.

Use AWS KMS in conjunction with AWS Backup to encrypt the backup data either using customer-managed CMK or an AWS-managed CMK associated with the AWS Backup service.

Use AWS Backup Vault Lock for immutable storage of critical data.

Secure S3 buckets through access policy, disabling public access, enforcing data at-rest encryption, and versioning control.

GCP guidance: Use dedicated accounts with the strongest authentication to performing critical backup and recovery operations, such as delete, change retention, updates to backup config. This would safeguard backup data from accidental or malicious deletion, such as ransomware attacks/attempts to encrypt or tamper backup data.

For GCP Backup supported resources, use Google IAM with roles and permissions to segregate duties and enable fine grained access, and set up a private services access connection to VPC to securely backup and restore data from Backup/Recovery appliance.

Backup data is automatically encrypted by default at the platform level using Advanced Encryption Standard (AES) algorithm, AES-256.

#### NOTE: If you use a resource's native backup feature or backup services other than GCP Backup, you should refer to the respective guideline to implement the security controls. For example, you can also protect specific VM instances from deletion by setting the deletionProtection property on a VM instance resource.

## Security Control: Data protection

Data Protection covers control of data protection at rest, in transit, and via authorized access mechanisms, including discover, classify, protect, and monitor sensitive data assets using access control, encryption, key management and certificate management.

### DP-2: Monitor anomalies and threats targeting sensitive data

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 3.13                 | AC-4, SI-4           | A3.2               |

Security principle: Monitor for anomalies around sensitive data, such as unauthorized transfer of data to locations outside of enterprise visibility and control. This typically involves monitoring for anomalous activities (large or unusual transfers) that could indicate unauthorized data exfiltration.

Azure guidance: Use Azure Information protection (AIP) to monitor the data that has been classified and labeled.

Use Microsoft Defender for Storage, Microsoft Defender for SQL, Microsoft Defender for open-source relational databases, and Microsoft Defender for Cosmos DB to alert on anomalous transfer of information that might indicate unauthorized transfers of sensitive data information.

#### NOTE: If required for compliance of data loss prevention (DLP), you can use a host-based DLP solution from Azure Marketplace or a Microsoft 365 DLP solution to enforce detective and/or preventative controls to prevent data exfiltration.

AWS guidance: Use AWS Macie to monitor the data that has been classified and labeled, and use GuardDuty to detect anomalous activities on some resources (S3, EC2 or Kubernetes or IAM resources). Findings and alerts can be triaged, analyzed, and tracked using EventBridge and forwarded to Microsoft Sentinel or Security Hub for incident aggregation and tracking.

You may also connect your AWS accounts to Microsoft Defender for Cloud for compliance checks, container security, and endpoint security capabilities.

#### NOTE: If required for compliance of data loss prevention (DLP), you can use a host-based DLP solution from AWS Marketplace.

GCP guidance: Use Google Cloud Security Command Center/Event Threat Detection/Anomaly Detection to alert on anomalous transfer of information that might indicate unauthorized transfers of sensitive data information.

You may also connect your GCP accounts to Microsoft Defender for Cloud for compliance checks, container security, and endpoint security capabilities.

### DP-3: Encrypt sensitive data in transit

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|---------------------------|
| 3.10                 | SC-8                 | 3.5, 3.6, 4.1             |

Security principle: Protect the data in transit against 'out of band' attacks (such as traffic capture) using encryption to ensure that attackers cannot easily read or modify the data.

Set the network boundary and service scope where data in transit encryption is mandatory inside and outside of the network. While this is optional for traffic on private networks, this is critical for traffic on external and public networks.

Azure guidance: Enforce secure transfer in services such as Azure Storage, where a native data in transit encryption feature is built in.

Enforce HTTPS for web application workloads and services by ensuring that any clients connecting to your Azure resources use transport layer security (TLS) v1.2 or later. For remote management of VMs, use SSH (for Linux) or RDP/TLS (for Windows) instead of an unencrypted protocol.

#### NOTE: Data in transit encryption is enabled for all Azure traffic traveling between Azure datacenters. TLS v1.2 or later is enabled on most Azure services by default. And some services such as Azure Storage and Application Gateway can enforce TLS v1.2 or later on the server side.

AWS guidance: Enforce secure transfer in services such as Amazon S3, RDS and CloudFront, where a native data in transit encryption feature is built in.

Enforce HTTPS (such as in AWS Elastic Load Balancer) for workload web application and services (either on the server side or client side, or on both) by ensuring that any clients connecting to your AWS resources use TLS v1.2 or later.

For remote management of EC2 instances, use SSH (for Linux) or RDP/TLS (for Windows) instead of an unencrypted protocol. For secure file transfer, use AWS Transfer SFTP or FTPS service instead of a regular FTP service.

#### NOTE: All network traffic between AWS data centers is transparently encrypted at the physical layer. All traffic within a VPC and between peered VPCs across regions is transparently encrypted at the network layer when using supported Amazon EC2 instance types. TLS v1.2 or later is enabled on most AWS services by default. And some services such as AWS Load Balancer can enforce TLS v1.2 or later on the server side.

GCP guidance: Enforce secure transfer in services such as Google Cloud Storage, where a native data in transit encryption feature is built in.

Enforce HTTPS for web application workloads and services ensuring that any clients connecting to your GCP resources use transport layer security (TLS) v1.2 or later.

For remote management Google Cloud Compute Engine use SSH (for Linux) or RDP/TLS (for Windows) instead of an unencrypted protocol. For secure file transfer, use the SFTP/FTPS service in services such as Google Cloud Big Query or Cloud App Engine instead of a regular FTP service.

### DP-6: Use a secure key management process

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)       | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------------|--------------------|
| N/A                  | IA-5, SC-12, SC-28         | 3.6                |

Security principle: Document and implement an enterprise cryptographic key management standard, processes, and procedures to control your key lifecycle. When there is a need to use customer-managed key in the services, use a secured key vault service for key generation, distribution, and storage. Rotate and revoke your keys based on the defined schedule and when there is a key retirement or compromise.

Azure guidance: Use Azure Key Vault to create and control your encryption keys life cycle, including key generation, distribution, and storage. Rotate and revoke your keys in Azure Key Vault and your service based on the defined schedule and when there is a key retirement or compromise. Require a certain cryptographic type and minimum key size when generating keys.

When there is a need to use customer-managed key (CMK) in the workload services or applications, ensure you follow the best practices:

1) Use a key hierarchy to generate a separate data encryption key (DEK) with your key encryption key (KEK) in your key vault.

2) Ensure keys are registered with Azure Key Vault and implemented via key IDs in each service or application.

To maximize the key material lifetime and portability, bring your own key (BYOK) to the services (i.e., importing HSM-protected keys from your on-premises HSMs into Azure Key Vault). Follow the recommended guideline to perform the key generation and key transfer.

#### NOTE: Refer to the below for the FIPS 140-2 level for Azure Key Vault types and FIPS compliance/validation level.

1) Software-protected keys in vaults (Premium & Standard SKUs): FIPS 140-2 Level 1

2) HSM-protected keys in vaults (Premium SKU): FIPS 140-2 Level 2

3) HSM-protected keys in Managed HSM: FIPS 140-2 Level 3

Azure Key Vault Premium uses a shared HSM infrastructure in the backend. Azure Key Vault Managed HSM uses dedicated, confidential service endpoints with a dedicated HSM for when you need a higher level of key security.

AWS guidance: Use AWS Key Management Service (KMS) to create and control your encryption keys life cycle, including key generation, distribution, and storage. Rotate and revoke your keys in KMS and your service based on the defined schedule and when there is a key retirement or compromise.

When there is a need to use customer-managed customer master key in the workload services or applications, ensure you follow the best practices:

1) Use a key hierarchy to generate a separate data encryption key (DEK) with your key encryption key (KEK) in your KMS.

2) Ensure keys are registered with KMS and implement via IAM policies in each service or application.

To maximize the key material lifetime and portability, bring your own key (BYOK) to the services (i.e., importing HSM-protected keys from your on-premises HSMs into KMS or Cloud HSM). Follow the recommended guideline to perform the key generation and key transfer.

#### NOTE: AWS KMS uses shared HSM infrastructure in the backend. Use AWS KMS Custom Key Store backed by AWS CloudHSM when you need to manage your own key store and dedicated HSMs (e.g. regulatory compliance requirement for higher level of key security) to generate and store your encryption keys.

Refer to the below for the FIPS 140-2 level for FIPS compliance level in AWS KMS and CloudHSM:

1) AWS KMS default: FIPS 140-2 Level 2 validated

2) AWS KMS using CloudHSM: FIPS 140-2 Level 3 (for certain services) validated

3) AWS CloudHSM: FIPS 140-2 Level 3 validated

#### NOTE:  For secrets management(credentials, password, API keys etc.), use AWS Secrets Manager.

GCP guidance: Use Cloud Key Management Service (Cloud KMS) to create and manage encryption key lifecycles in compatible Google Cloud services and in your workload applications. Rotate and revoke your keys in Cloud KMS and your service based on the defined schedule and when there is a key retirement or compromise.

Use Google’s Cloud HSM service to provide hardware-backed keys to Cloud KMS (Key Management Service) It gives you ability to manage and use your own cryptographic keys while being protected by fully managed Hardware Security Modules (HSM).

The Cloud HSM service uses HSMs, which are FIPS 140-2 Level 3-validated and are always running in FIPS mode. FIPS 140-2 Level 3-validated and are always running in FIPS mode. FIPS standard specifies the cryptographic algorithms and random number generation used by the HSMs.

### DP-7: Use a secure certificate management process

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)       | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------------|--------------------|
| N/A                  | IA-5, SC-12, SC-17         | 3.6                |

Security principle: Document and implement an enterprise certificate management standard, processes and procedures which includes the certificate lifecycle control, and certificate policies (if a public key infrastructure is needed).

Ensure certificates used by the critical services in your organization are inventoried, tracked, monitored, and renewed timely using automated mechanism to avoid service disruption.

Azure guidance: Use Azure Key Vault to create and control the certificate lifecycle, including the creation/import, rotation, revocation, storage, and purge of the certificate. Ensure the certificate generation follows the defined standard without using any insecure properties, such as insufficient key size, overly long validity period, insecure cryptography and so on. Setup automatic rotation of the certificate in Azure Key Vault and supported Azure services based on the defined schedule and when a certificate expires. If automatic rotation is not supported in the frontend application, use a manual rotation in Azure Key Vault.

Avoid using a self-signed certificate and wildcard certificate in your critical services due to the limited security assurance. Instead, you can create public signed certificates in Azure Key Vault. The following Certificate Authorities (CAs) are the partnered providers that are currently integrated with Azure Key Vault.

1) DigiCert: Azure Key Vault offers OV TLS/SSL certificates with DigiCert.

2) GlobalSign: Azure Key Vault offers OV TLS/SSL certificates with GlobalSign.

#### NOTE: Use only approved CA and ensure that known bad root/intermediate certificates issued by these CAs are disabled.

AWS guidance: Use AWS Certificate Manager (ACM) to create and control the certificate lifecycle, including creation/import, rotation, revocation, storage, and purge of the certificate. Ensure the certificate generation follows the defined standard without using any insecure properties, such as insufficient key size, overly long validity period, insecure cryptography and so on. Setup automatic rotation of the certificate in ACM and supported AWS services based on the defined schedule and when a certificate expires. If automatic rotation is not supported in the frontend application, use manual rotation in ACM. In the meantime, you should always track your certificate renewal status to ensure the certificate validity.

Avoid using a self-signed certificate and wildcard certificate in your critical services due to the limited security assurance. Instead, create public-signed certificates (signed by the Amazon Certificate Authority) in ACM and deploy it programmatically in services such as CloudFront, Load Balancers, API Gateway etc. You also can use ACM to establish your private certificate authority (CA) to sign the private certificates.

#### NOTE: Use only an approved CA and ensure that known bad CA root/intermediate certificates issued by these CAs are disabled.

GCP guidance: Use Google Cloud Certificate Manager to create and control the certificate lifecycle, including creation/import, rotation, revocation, storage, and purge of the certificate. Ensure the certificate generation follows the defined standard without using any insecure properties, such as insufficient key size, overly long validity period, insecure cryptography and so on. Setup automatic rotation of the certificate in Certificate Manager and supported GCP services based on the defined schedule and when a certificate expires. If automatic rotation is not supported in the frontend application, use manual rotation in Certificate Manager. In the meantime, you should always track your certificate renewal status to ensure the certificate validity.

Avoid using a self-signed certificate and wildcard certificate in your critical services due to the limited security assurance. Instead, you can create signed public certificates in Certificate Manager and deploy it programmatically in services such as Load Balancer and Cloud DNS etc. You also can use Certificate Authority Service to establish your private certificate authority (CA) to sign the private certificates.

#### NOTE: You can also use Google Cloud Secret Manager to store TLS certificates.

### DP-8: Ensure security of key and certificate repository

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)       | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------------|--------------------|
| N/A                  | IA-5, SC-12, SC-17         | 3.6                |

Security principle: Ensure the security of the key vault service used for the cryptographic key and certificate lifecycle management. Harden your key vault service through access control, network security, logging and monitoring and backup to ensure keys and certificates are always protected using the maximum security.

Azure guidance: Secure your cryptographic keys and certificates by hardening your Azure Key Vault service through the following controls:

1) Implement access control using RBAC policies in Azure Key Vault Managed HSM at the key level to ensure the least privilege and separation of duties principles are followed. For example, ensure separation of duties are in place for users who manage encryption keys so they do not have the ability to access encrypted data, and vice versa. For Azure Key Vault Standard and Premium, create unique vaults for different applications to ensure the least privilege and separation of duties principles are followed.

2) Turn on Azure Key Vault logging to ensure critical management plane and data plane activities are logged.

3) Secure the Azure Key Vault using Private Link and Azure Firewall to ensure minimal exposure of the service

4) Use managed identity to access keys stored in Azure Key Vault in your workload applications.

5) When purging data, ensure your keys are not deleted before the actual data, backups and archives are purged.

6) Backup your keys and certificates using Azure Key Vault. Enable soft delete and purge protection to avoid accidental deletion of keys.When keys need to be deleted, consider disabling keys instead of deleting them to avoid accidental deletion of keys and cryptographic erasure of data.

7) For bring your own key (BYOK) use cases, generate keys in an on-premises HSM and import them to maximize the lifetime and portability of the keys.

8) Never store keys in plaintext format outside of the Azure Key Vault. Keys in all key vault services are not exportable by default.

9) Use HSM-backed key types (RSA-HSM) in Azure Key Vault Premium and Azure Managed HSM for the hardware protection and the strongest FIPS levels.

Enable Microsoft Defender for Key Vault for Azure-native, advanced threat protection for Azure Key Vault, providing an additional layer of security intelligence.

AWS guidance: For cryptographic keys security, secure your keys by hardening your AWS Key Management Service (KMS) service through the following controls:

1) Implement access control using key policies (key-level access control) in conjunction with IAM policies (identity-based access control) to ensure the least privilege and separation of duties principles are followed. For example, ensure separation of duties are in place for users who manage encryption keys so they do not have the ability to access encrypted data, and vice versa.

2) Use detective controls such as CloudTrails to log and track the usage of keys in KMS and alert you on critical actions.

3) Never store keys in plaintext format outside of KMS.

4) When keys need to be deleted, consider disabling keys in KMS instead of deleting them to avoid accidental deletion of keys and cryptographic erasure of data.

5) When purging data, ensure your keys are not deleted before the actual data, backups and archives are purged.

6) For bring your own key (BYOK) uses cases, generate keys in an on-premise HSM and import them to maximize the lifetime and portability of the keys.

For certificates security, secure your certificates by hardening your AWS Certificate Manager (ACM) service through the following controls:

1) Implement access control using resource-level policies in conjunction with IAM policies (identity-based access control) to ensure the least privilege and separation of duties principles are followed. For example, ensure separation of duties is in place for user accounts: user accounts who generate certificates are separate from the user accounts who only require read-only access to certificates.

2) Use detective controls such as CloudTrails to log and track the usage of the certificates in ACM, and alert you on critical actions.

3) Follow the KMS security guidance to secure your private key (generated for certificate request) used for service certificate integration.

GCP guidance: For cryptographic keys security, secure your keys by hardening your Key Management Service through the following controls:

1) Implement access control using IAM roles to ensure the least privilege and separation of duties principles are followed. For example, ensure separation of duties are in place for users who manage encryption keys so they do not have the ability to access encrypted data, and vice versa.

2) Create a separate key ring for each project which allows you to easily manage and control access to the keys following least privilege best practice. It also makes it easier to audit who has access to which keys at when.

3) Enable automatic rotation of keys to ensure keys are regularly updated and refreshed. This helps to protect against potential security threats such as brute force attacks or malicious actors attempting to gain access to sensitive information.

4) Setup up an audit log sink to track all the activities that occur within you GCP KMS environment.

For certificates security, secure your certificates by hardening your GCP Certificate Manager and Certificate Authority Service through the following controls:

1) Implement access control using resource-level policies in conjunction with IAM policies (identity-based access control) to ensure the least privilege and separation of duties principles are followed. For example, ensure separation of duties is in place for user accounts: user accounts who generate certificates are separate from the user accounts who only require read-only access to certificates.

2) Use detective controls such as Cloud Audit Logs to log and track the usage of the certificates in Certificate Manager, and alert you on critical actions.

3) Secret Manager also support storage of TLS certificate. You need to follow the similar security practice to implement the security controls in Secret Manager.

## Security Control: Endpoint security

Endpoint Security covers controls in endpoint detection and response, including use of endpoint detection and response (EDR) and anti-malware service for endpoints in cloud environments.

### ES-1: Use Endpoint Detection and Response (EDR)

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)       | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------------|--------------------|
| 13.7                 | SC-3, SI-2, SI-3, SI-16     | 11.5               |

Security principle: Enable Endpoint Detection and Response (EDR) capabilities for VMs and integrate with SIEM and security operations processes.

Azure guidance: Microsoft Defender for servers (with Microsoft Defender for Endpoint integrated) provides EDR capability to prevent, detect, investigate, and respond to advanced threats.

Use Microsoft Defender for Cloud to deploy Microsoft Defender for servers on your endpoints and integrate the alerts to your SIEM solution such as Microsoft Sentinel.

AWS guidance: Onboard your AWS account into Microsoft Defender for Cloud and deploy Microsoft Defender for servers (with Microsoft Defender for Endpoint integrated) on your EC2 instances to provide EDR capabilities to prevent, detect, investigate, and respond to advanced threats.

Alternatively, use Amazon GuardDuty integrated threat intelligence capability to monitor and protect your EC2 instances. Amazon GuardDuty can detect anomalous activities such as activity indicating an instance compromise, such as cryptocurrency mining, malware using domain generation algorithms (DGAs), outbound denial of service activity, unusually high volume of network traffic, unusual network protocols, outbound instance communication with a known malicious IP, temporary Amazon EC2 credentials use by an external IP address, and data exfiltration using DNS.

GCP guidance: Onboard your GCP project into Microsoft Defender for Cloud and deploy Microsoft Defender for servers (with Microsoft Defender for Endpoint integrated) on your virtual machine instances to provide EDR capabilities to prevent, detect, investigate, and respond to advanced threats.

Alternatively, use Google's Security Command Center for integrated threat intelligence to monitor and protect your virtual machine instances. Security Command Center can detect anomalous activity such as potentially leaked credentials, cryptocurrency mining, potentially malicious applications, malicious network activity, and more.

### ES-2: Use modern anti-malware software

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)       | PCI-DSS ID(s) v3.2.1 |
|----------------------|-----------------------------|--------------------|
| 10.1                 | SC-3, SI-2, SI-3, SI-16     | 5.1                |

Security principle: Use anti-malware solutions (also known as endpoint protection) capable of real-time protection and periodic scanning.

Azure guidance: Microsoft Defender for Cloud can automatically identify the use of a number of popular anti-malware solutions for your virtual machines and on-premises machines with Azure Arc configured and report the endpoint protection running status and make recommendations.

Microsoft Defender Antivirus is the default anti-malware solution for Windows server 2016 and above. For Windows server 2012 R2, use Microsoft Antimalware extension to enable SCEP (System Center Endpoint Protection). For Linux VMs, use Microsoft Defender for Endpoint on Linux for the endpoint protection feature.

For both Windows and Linux, you can use Microsoft Defender for Cloud to discover and assess the health status of the anti-malware solution.

#### NOTE: You can also use Microsoft Defender for Cloud's Defender for Storage to detect malware uploaded to Azure Storage accounts.

AWS guidance: Onboard your AWS account into Microsoft Defender for Cloud to allow Microsoft Defender for Cloud to automatically identify the use some popular anti-malware solutions for EC2 instances with Azure Arc configured and report the endpoint protection running status and make recommendations.

Deploy Microsoft Defender Antivirus which is the default anti-malware solution for Windows server 2016 and above. For EC2 instances running Windows server 2012 R2, use Microsoft Antimalware extension to enable SCEP (System Center Endpoint Protection). For EC2 instances running Linux, use Microsoft Defender for Endpoint on Linux for the endpoint protection feature.

For both Windows and Linux, you can use Microsoft Defender for Cloud to discover and assess the health status of the anti-malware solution.

#### NOTE: Microsoft Defender Cloud also supports certain third-party endpoint protection products for the discovery and health status assessment.

GCP guidance: Onboard your GCP projects into Microsoft Defender for Cloud to allow Microsoft Defender for Cloud to automatically identify the use of popular anti-malware solutions for virtual machine instances with Azure Arc configured and report the endpoint protection status and make recommendations.

Deploy Microsoft Defender Antivirus which is the default anti-malware solution for Windows server 2016 and above. For virtual machine instances running Windows server 2012 R2, use Microsoft Antimalware extension to enable SCEP (System Center Endpoint Protection). For virtual machine instances running Linux, use Microsoft Defender for Endpoint on Linux for the endpoint protection feature.

For both Windows and Linux, you can use Microsoft Defender for Cloud to discover and assess the health status of the anti-malware solution.

#### NOTE: Microsoft Defender Cloud also supports certain third-party endpoint protection products for the discovery and health status assessment.

### ES-3: Ensure anti-malware software and signatures are updated

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 10.2                 | SI-2, SI-3           | 5.2                |

Security principle: Ensure anti-malware signatures are updated rapidly and consistently for the anti-malware solution.

Azure guidance: Follow recommendations in Microsoft Defender for Cloud to keep all endpoints up to date with the latest signatures. Microsoft Antimalware (for Windows) and Microsoft Defender for Endpoint (for Linux) will automatically install the latest signatures and engine updates by default.

For third-party solutions, ensure the signatures are updated in the third-party anti-malware solution.

AWS guidance: With your AWS account onboarded into Microsoft Defender for Cloud, follow recommendations in Microsoft Defender for Cloud to keep all endpoints up to date with the latest signatures. Microsoft Antimalware (for Windows) and Microsoft Defender for Endpoint (for Linux) will automatically install the latest signatures and engine updates by default.

For third-party solutions, ensure the signatures are updated in the third-party anti-malware solution.

GCP guidance: With your GCP projects onboarded into Microsoft Defender for Cloud, follow recommendations in Microsoft Defender for Cloud to keep all EDR solutions up to date with the latest signatures. Microsoft Antimalware (for Windows) and Microsoft Defender for Endpoint (for Linux) will automatically install the latest signatures and engine updates by default.

For third-party solutions, ensure the signatures are updated in the third-party anti-malware solution.

## Security Control: Governance and strategy

Governance and Strategy provides guidance for ensuring a coherent security strategy and documented governance approach to guide and sustain security assurance, including establishing roles and responsibilities for the different cloud security functions, unified technical strategy, and supporting policies and standards.

### GS-5: Define and implement security posture management strategy

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)                                         | PCI-DSS ID(s) v3.2.1                               |
|----------------------|----------------------------------------------------------------|------------------------------------------------|
| 4.1, 4.2            | CA-1, CA-8, CM-1, CM-2, CM-6, RA-1, RA-3, RA-5, SI-1, SI-2, SI-5 | 1.1, 1.2, 2.2, 6.1, 6.2, 6.5, 6.6, 11.2, 11.3, 11.5 |

General guidance: Establish a policy, procedure and standard to ensure the security configuration management and vulnerability management are in place in your cloud security mandate.

The security configuration management in cloud should include the following areas:

1) Define the secure configuration baselines for different resource types in the cloud, such as the web portal/console, management and control plane, and resources running in the IaaS, PaaS and SaaS services.
Ensure the security baselines address the risks in different control areas such as network security, identity management, privileged access, data protection and so on.

2) Use tools to continuously measure, audit, and enforce the configuration to prevent configuration deviating from the baseline.

3) Develop a cadence to stay updated with security features, for instance, subscribe to the service updates.

4) Utilize a security health or compliance check mechanism (such as Secure Score, Compliance Dashboard in Microsoft Defender for Cloud) to regularly review security configuration posture and remediate the gaps identified.

The vulnerability management in the cloud should include the following security aspects:

1) Regularly assess and remediate vulnerabilities in all cloud resource types, such as cloud native services, operating systems, and application components.

2) Use a risk-based approach to prioritize assessment and remediation.

3) Subscribe to the relevant CSPM's security advisory notices and blogs to receive the latest security updates.

4) Ensure the vulnerability assessment and remediation (such as schedule, scope, and techniques) meet the compliance requirements for your organization.dule, scope, and techniques) meet the regularly compliance requirements for your organization.

### GS-11: Define and implement multi-cloud security strategy

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| N/A                  | N/A                  | N/A                |

General guidance: Ensure a multi-cloud strategy is defined in your cloud and security governance, risk management, and operation process which should include the following aspects:

1) Multi-cloud adoption: For organizations that operate multi-cloud infrastructure and Educate your organization to ensure teams understand the feature difference between the cloud platforms and technology stack. Build, deploy, and/or migrate solutions that are portable. Allow for ease of movement between cloud platforms with minimum vendor lock-in while utilizing cloud native features adequately for the optimal result from the cloud adoption.

2) Cloud and security operations: Streamline security operations to support the solutions across each cloud, through a central set of governance and management processes which share common operations processes, regardless of where the solution is deployed and operated.

3) Tooling and technology stack: Choose the appropriate tooling that supports multicloud environment to help with establishing unified and centralized management platforms which may include all the security domains discussed in this security benchmark.

## Security Control: Identity management

Identity Management covers controls to establish a secure identity and access controls using identity and access management systems, including the use of single sign-on, strong authentications, managed identities (and service principals) for applications, conditional access, and account anomalies monitoring.

### IM-8: Restrict the exposure of credentials and secrets

| CIS Controls v8 ID(s)  | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|-----------------------|----------------------|--------------------|
| 16.9, 16.12          | IA-5                 | 3.5, 6.3, 8.2      |

Security principle: Ensure that application developers securely handle credentials and secrets:

1) Avoid embedding the credentials and secrets into the code and configuration files

2) Use key vault or a secure key store service to store the credentials and secrets

3) Scan for credentials in source code.

#### NOTE: This is often governed and enforced through a secure software development lifecycle (SDLC) and DevOps security process.

Azure guidance: When using a managed identity is not an option, ensure that secrets and credentials are stored in secure locations such as Azure Key Vault, instead of embedding them into the code and configuration files.

If you use Azure DevOps and GitHub for your code management platform:

1) Implement Azure DevOps Credential Scanner to identify credentials within the code.

2) For GitHub, use the native secret scanning feature to identify credentials or other form of secrets within the code.

Clients such as Azure Functions, Azure Apps services, and VMs can use managed identities to access Azure Key Vault securely. See Data Protection controls related to the use of Azure Key Vault for secrets management.

#### NOTE: Azure Key Vault provides automatic rotation for supported services. For secrets that cannot be automatically rotated, ensure they are manually rotated periodically and purged when no longer in use.

AWS guidance: When using an IAM role for application access is not an option, ensure that secrets and credentials are stored in secure locations such as AWS Secret Manager or Systems Manager Parameter Store, instead of embedding them into the code and configuration files.

Use CodeGuru Reviewer for static code analysis which can detect the secrets hard-coded in your source code.

If you use the Azure DevOps and GitHub for your code management platform:

1) Implement Azure DevOps Credential Scanner to identify credentials within the code.
2) For GitHub, use the native secret scanning feature to identify credentials or other forms of secrets within the code.

#### NOTE: Secrets Manager provides automatic secrets rotation for supported services. For secrets that cannot be automatically rotated, ensure they are manually rotated periodically and purged when no longer in use.

GCP guidance: When using a Google-managed service account for application access is not an option, ensure that secrets and credentials are stored in secure locations such as Google Cloud's Secret Manager instead of embedding them into the code and configuration files.

Use the Google Cloud Code extension on IDE's (Integrated development environment) such as Visual Studio Code to integrate secrets managed by Secret Manager into your code.

If you use the Azure DevOps or GitHub for your code management platform:

1) Implement Azure DevOps Credential Scanner to identify credentials within the code.

2) For GitHub, use the native secret scanning feature to identify credentials or other forms of secrets within the code.

#### NOTE: Set up rotation schedules for secrets stored in Secret Manager as a best practice.

## Security Control: Incident response

Incident Response covers controls in incident response life cycle - preparation, detection and analysis, containment, and post-incident activities, including using Azure services (such as Microsoft Defender for Cloud and Sentinel) and/or other cloud services to automate the incident response process.

### IR-4: Detection and analysis - investigate an incident

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| N/A                  | IR-4                 | 12.10              |

Security principle: Ensure the security operation team can query and use diverse data sources as they investigate potential incidents, to build a full view of what happened. Diverse logs should be collected to track the activities of a potential attacker across the kill chain to avoid blind spots. You should also ensure insights and learnings are captured for other analysts and for future historical reference.

Use the cloud native SIEM and incident management solution if your organization does not have an existing solution to aggregate security logs and alerts information. Correlate incident data based on the data sourced from different sources to facility the incident investigations.

Azure guidance: Ensure your security operations team can query and use diverse data sources that are collected from the in-scope services and systems. In addition, it sources can also include:

1) Identity and access log data: Use Azure AD logs and workload (such as operating systems or application level) access logs for correlating identity and access events.

2) Network data: Use network security groups' flow logs, Azure Network Watcher, and Azure Monitor to capture network flow logs and other analytics information.

3) Incident related activity data of from snapshots of the impacted systems, which can be obtained through:

 - The Azure Virtual Machine's snapshots capability, to create a snapshot of the running system's disk.

 - The operating system's native memory dump capability, to create a snapshot of the running system's memory.

 - The snapshot feature of other supported Azure services or your software's own capability, to create snapshots of the running systems.

Microsoft Sentinel provides extensive data analytics across virtually any log source and a case management portal to manage the full lifecycle of incidents. Intelligence information during an investigation can be associated with an incident for tracking and reporting purposes.

#### NOTE: When incident related data is captured for investigation, ensure there is adequate security in place to protect the data from unauthorized alteration, such as disabling logging or removing logs, which can be performed by the attackers during an in-flight data breach activity.

AWS guidance: The data sources for investigation are the centralized logging sources that collect from the in-scope services and running systems, but can also include:

1) Identity and access log data: Use IAM logs and workload (such as operating systems or application level) access logs for correlating identity and access events.

2) Network data: Use VPC Flow Logs, VPC Traffic Mirrors, and Azure CloudTrail and CloudWatch to capture network flow logs and other analytics information.

3) Snapshots of running systems, which can be obtained through:

 - Snapshot capability in Amazon EC2(EBS) to create a snapshot of the running system's disk.

 - The operating system's native memory dump capability, to create a snapshot of the running system's memory.

 - The snapshot feature of the AWS services or your software's own capability, to create snapshots of the running systems.

If you aggregate your SIEM related data into Microsoft Sentinel, it provides extensive data analytics across virtually any log source and a case management portal to manage the full lifecycle of incidents. Intelligence information during an investigation can be associated with an incident for tracking and reporting purposes.

#### NOTE: When incident related data is captured for investigation, ensure there is adequate security in place to protect the data from unauthorized alteration, such as disabling logging or removing logs, which can be performed by the attackers during an in-flight data breach activity.

GCP guidance: The data sources for investigation are the centralized logging sources that collect from the in-scope services and running systems, but can also include:

1) Identity and access log data: Use IAM logs and workload (such as operating systems or application level) access logs for correlating identity and access events.

2) Network data: Use VPC Flow Logs and VPC service controls to capture network flow logs and other analytics information.

3) Snapshots of running systems, which can be obtained through:

 - Snapshot capability in GCP VMs to create a snapshot of the running system's disk.

 - The operating system's native memory dump capability, to create a snapshot of the running system's memory.

 - The snapshot feature of the GCP services or your software's own capability, to create snapshots of the running systems.

If you aggregate your SIEM related data into Microsoft Sentinel, it provides extensive data analytics across virtually any log source and a case management portal to manage the full lifecycle of incidents. Intelligence information during an investigation can be associated with an incident for tracking and reporting purposes.

#### NOTE: When incident related data is captured for investigation, ensure there is adequate security in place to protect the data from unauthorized alteration, such as disabling logging or removing logs, which can be performed by the attackers during an in-flight data breach activity.

### IR-6: Containment, eradication and recovery - automate the incident handling

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)     | PCI-DSS ID(s) v3.2.1 |
|----------------------|--------------------------|--------------------|
| N/A                  | IR-4, IR-5, IR-6         | 12.10              |

Security principle: Automate the manual, repetitive tasks to speed up response time and reduce the burden on analysts. Manual tasks take longer to execute, slowing each incident and reducing how many incidents an analyst can handle. Manual tasks also increase analyst fatigue, which increases the risk of human error that causes delays and degrades the ability of analysts to focus effectively on complex tasks.

Azure guidance: Use workflow automation features in Microsoft Defender for Cloud and Microsoft Sentinel to automatically trigger actions or run a playbooks to respond to incoming security alerts. Playbooks take actions, such as sending notifications, disabling accounts, and isolating problematic networks.

AWS guidance: If you use Microsoft Sentinel to centrally manage your incident, you can also create automated actions or run a playbooks to respond to incoming security alerts.

Alternatively, use automation features in AWS System Manager to automatically trigger actions defined in the incident response plan, including notifying the contacts and/or running a runbook to respond to alerts, such as disabling accounts, and isolating problematic networks.

GCP guidance: If you use Microsoft Sentinel to centrally manage your incident, you can also create automated actions or run playbooks to respond to incoming security alerts.

Alternatively, use Playbook automations in Chronicle to automatically trigger actions defined in the incident response plan, including notifying the contacts and/or running a playbook to respond to alerts.

## Security Control: Logging and threat detection

Logging and Threat Detection covers controls for detecting threats on cloud, and enabling, collecting, and storing audit logs for cloud services, including enabling detection, investigation, and remediation processes with controls to generate high-quality alerts with native threat detection in cloud services; it also includes collecting logs with a cloud monitoring service, centralizing security analysis with a SIEM, time synchronization, and log retention.

### LT-1: Enable threat detection capabilities

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)               | PCI-DSS ID(s) v3.2.1 |
|----------------------|------------------------------------|--------------------|
| 8.11                 | AU-3, AU-6, AU-12, SI-4           | 10.6, 10.8, A3.5    |

Security principle: To support threat detection scenarios, monitor all known resource types for known and expected threats and anomalies. Configure your alert filtering and analytics rules to extract high-quality alerts from log data, agents, or other data sources to reduce false positives.

Azure guidance: Use the threat detection capability of Microsoft Defender for Cloud for the respective Azure services.

For threat detection not included in Microsoft Defender services, refer to Microsoft Cloud Security Benchmark service baselines for the respective services to enable the threat detection or security alert capabilities within the service. Ingest alerts and log data from Microsoft Defender for Cloud, Microsoft 365 Defender, and log data from other resources into your Azure Monitor or Microsoft Sentinel instances to build analytics rules, which detect threats and create alerts that match specific criteria across your environment.

For Operational Technology (OT) environments that include computers that control or monitor Industrial Control System (ICS) or Supervisory Control and Data Acquisition (SCADA) resources, use Microsoft Defender for IoT to inventory assets and detect threats and vulnerabilities.

For services that do not have a native threat detection capability, consider collecting the data plane logs and analyze the threats through Microsoft Sentinel.

AWS guidance: Use Amazon GuardDuty for threat detection which analyzes and processes the following data sources: VPC Flow Logs, AWS CloudTrail management event logs, CloudTrail S3 data event logs, EKS audit logs, and DNS logs. GuardDuty is capable of reporting on security issues such as privilege escalation, exposed credential usage , or communication with malicious IP addresses, or domains.

Configure AWS Config to check rules in SecurityHub for compliance monitoring such as configuration drift, and create findings when needed.

For threat detection not included in GuardDuty and SecurityHub, enable threat detection or security alert capabilities within the supported AWS services. Extract the alerts to your CloudTrail, CloudWatch, or Microsoft Sentinel to build analytics rules, which hunt threats that match specific criteria across your environment.

You can also use Microsoft Defender for Cloud to monitor certain services in AWS such as EC2 instances.

For Operational Technology (OT) environments that include computers that control or monitor Industrial Control System (ICS) or Supervisory Control and Data Acquisition (SCADA) resources, use Microsoft Defender for IoT to inventory assets and detect threats and vulnerabilities.

GCP guidance: Use the Event Threat Detection in Google Cloud Security Command Center for threat detection using log data such as Admin Activity, GKE Data Access, VPC Flow Logs, Cloud DNS, and Firewall Logs.

Additionally use the Security Operations suite for the modern SOC with Chronicle SIEM and SOAR. Chronicle SIEM and SOAR provides threat detection, investigation, and hunting capabilities

You can also use Microsoft Defender for Cloud to monitor certain services in GCP such as Compute VM instances.

For Operational Technology (OT) environments that include computers that control or monitor Industrial Control System (ICS) or Supervisory Control and Data Acquisition (SCADA) resources, use Microsoft Defender for IoT to inventory assets and detect threats and vulnerabilities.

### LT-3: Enable logging for security investigation

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)               | PCI-DSS ID(s) v3.2.1 |
|----------------------|------------------------------------|--------------------|
| 8.2, 8.5, 8.12       | AU-3, AU-6, AU-12, SI-4           | 10.1, 10.2, 10.3    |

Security principle: Enable logging for your cloud resources to meet the requirements for security incident investigations and security response and compliance purposes.

Azure guidance: Enable logging capability for resources at the different tiers, such as logs for Azure resources, operating systems and applications inside in your VMs and other log types.

Be mindful about different types of logs for security, audit, and other operational logs at the management/control plane and data plane tiers. There are three types of the logs available at the Azure platform:

1) Azure resource log: Logging of operations that are performed within an Azure resource (the data plane). For example, getting a secret from a key vault or making a request to a database. The content of resource logs varies by the Azure service and resource type.

2) Azure activity log: Logging of operations on each Azure resource at the subscription layer, from the outside (the management plane). You can use the Activity Log to determine what, who, and when for any write operations (PUT, POST, DELETE) taken on the resources in your subscription. There is a single Activity log for each Azure subscription.

3) Microsoft Entra ID logs: Logs of the history of sign-in activity and audit trail of changes made in the Microsoft Entra ID for a particular tenant.

You can also use Microsoft Defender for Cloud and Azure Policy to enable resource logs and log data collecting on Azure resources.

AWS guidance: Use AWS CloudTrail logging for management events (control plane operations) and data events (data plane operations) and monitor these trails with CloudWatch for automated actions.

The Amazon CloudWatch Logs service allows you to collect and store logs from your resources, applications, and services in near real time. There are three main categories of logs:

1) Vended logs: Logs natively published by AWS services on your behalf. Currently, Amazon VPC Flow Logs and Amazon Route 53 logs are the two supported types. These two logs are enabled by default.

2) Logs published by AWS services: Logs from more than 30 AWS services publish to CloudWatch. They include Amazon API Gateway, AWS Lambda, AWS CloudTrail, and many others. These logs can be enabled directly in the services and CloudWatch.

3) Custom logs: Logs from your own application and on-premises resources. You may need to collect these logs by installing CloudWatch Agent in your operating systems and forward them to CloudWatch.

While many services publish logs only to CloudWatch Logs, some AWS services can publish logs directly to AmazonS3 or Amazon Kinesis Data Firehose where you can use different logging storage and retention policies.

GCP guidance: Enable logging capability for resources at the different tiers, such as logs for Azure resources, operating systems and applications inside in your VMs and other log types.

Be mindful about different types of logs for security, audit, and other operational logs at the management/control plane and data plane tiers. Operations Suite Cloud Logging service collect and aggregate all kind of log events from resource tiers. Four categories of logs are supported in Cloud Logging:

1) Platform logs - logs written by your Google Cloud services.

2) Component logs - similar to platform logs, but they are logs generated by Google-provided software components that run on your systems.

3) Security logs - mainly audit logs that record administrative activities and accesses within your resources.

4) User-written - logs written by custom applications and services

5) Multicloud logs and Hybrid-cloud logs - logs from other cloud providers like Microsoft Azure and logs from on-premises infrastructure.

### LT-4: Enable network logging for security investigation

| CIS Controls v8 ID(s)  | NIST SP 800-53 r4 ID(s)               | PCI-DSS ID(s) v3.2.1 |
|-----------------------|------------------------------------|--------------------|
| 8.2, 8.5, 8.6, 8.7, 13.6 | AU-3, AU-6, AU-12, SI-4           | 10.8               |

Security principle: Enable logging for your network services to support network-related incident investigations, threat hunting, and security alert generation. The network logs may include logs from network services such as IP filtering, network and application firewall, DNS, flow monitoring and so on.

Azure guidance: Enable and collect network security group (NSG) resource logs, NSG flow logs, Azure Firewall logs, and Web Application Firewall (WAF) logs, and logs from virtual machines via the network traffic data collection agent for security analysis to support incident investigations, and security alert generation. You can send the flow logs to an Azure Monitor Log Analytics workspace and then use Traffic Analytics to provide insights.

Collect DNS query logs to assist in correlating other network data.

AWS guidance: Enable and collect network logs such as VPC Flow Logs, WAF Logs, and Route53 Resolver query logs for security analysis to support incident investigations, and security alert generation. The logs can be exported to CloudWatch for monitoring or an S3 storage bucket for ingesting into the Microsoft Sentinel solution for centralized analytics.

GCP guidance: Most of the network activities logs are available through the VPC Flow Logs which records a sample of network flows send from and received by resources, including instances used as Google Compute VMs, Kubernetes Engine nodes. These logs can be used for network monitoring, forensics, real-time security analysis, and expense optimization.

You can view flow logs in Cloud Logging, and export logs to the destination that Cloud Logging export supports. Flow logs are aggregated by connection from Compute Engine VM’s and exported in real time. By subscribing to Pub/Sub, you can analyze flow logs using real-time streaming APIs.

#### NOTE: You can also use Packet Mirroring clones the traffic of specified instances in your Virtual Private Cloud (VPC) network and forwards it for examination. Packet Mirroring captures all traffic and packet data, including payloads and headers.

### LT-5: Centralize security log management and analysis

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s)               | PCI-DSS ID(s) v3.2.1 |
|----------------------|------------------------------------|--------------------|
| 8.9, 8.11, 13.1      | AU-3, AU-6, AU-12, SI-4           | N/A                |

Security principle: Centralize logging storage and analysis to enable correlation across log data. For each log source, ensure that you have assigned a data owner, access guidance, storage location, what tools are used to process and access the data, and data retention requirements.

Use Cloud native SIEM if you don't have an existing SIEM solution for CSPs. or aggregate logs/alerts into your existing SIEM.

Azure guidance: Ensure that you are integrating Azure activity logs into a centralized Log Analytics workspace. Use Azure Monitor to query and perform analytics and create alert rules using the logs aggregated from Azure services, endpoint devices, network resources, and other security systems.

In addition, enable and onboard data to Microsoft Sentinel which provides security information event management (SIEM) and security orchestration automated response (SOAR) capabilities.

AWS guidance: Ensure that you are integrating your AWS logs into a centralized resource for storage and analysis. Use CloudWatch to query and perform analytics, and to create alert rules using the logs aggregated from AWS services, services, endpoint devices, network resources, and other security systems.

In addition, you can aggregate the logs in a S3 storage bucket and onboard the log data to Microsoft Sentinel which provides security information event management (SIEM) and security orchestration automated response (SOAR) capabilities.

GCP guidance: Ensure that you are integrating your GCP logs into a centralized resource (such as Operations Suite Cloud Logging bucket) for storage and analysis. Cloud Logging supports most of the Google Cloud native service logging as well as the third-party applications and on-premise applications. You can use Cloud Logging for query and perform analytics, and to create alert rules using the logs aggregated from GCP services, services, endpoint devices, network resources, and other security systems.

Use Cloud native SIEM if you don’t have an existing SIEM solution for CSP’s, or aggregate logs/alerts into your existing SIEM.

#### NOTE: Google provide two log query frontend, Logs Explorer and Log Analytics for query, view, and analyze logs. For troubleshooting and exploring of log data, it is recommended to use Logs Explorer. To generate insights and trends, it is recommended to use Log Analytics.

### LT-6: Configure log storage retention

| CIS Controls v8 ID(s) | NIST SP 800-53 r4 ID(s) | PCI-DSS ID(s) v3.2.1 |
|----------------------|----------------------|--------------------|
| 8.3, 8.10            | AU-11                | 10.5, 10.7          |

Security principle: Plan your log retention strategy according to your compliance, regulation, and business requirements. Configure the log retention policy at the individual logging services to ensure the logs are archived appropriately.

Azure guidance: Logs such as Azure Activity Logs are retained for 90 days and then deleted. You should create a diagnostic setting and route the logs to another location (such as Azure Monitor Log Analytics workspace, Event Hubs or Azure Storage) based on your needs. This strategy also applies to other resource logs and resources managed by yourself such as logs in the operating systems and applications inside VMs.

You have the log retention option as below:

1) Use Azure Monitor Log Analytics workspace for a log retention period of up to 1 year or per your response team requirements.

2) Use Azure Storage, Data Explorer or Data Lake for long-term and archival storage for greater than 1 year and to meet your security compliance requirements.

3) Use Azure Event Hubs to forward logs to an external resource outside of Azure.

#### NOTE: Microsoft Sentinel uses Log Analytics workspace as its backend for log storage. You should consider a long-term storage strategy if you plan to retain SIEM logs for longer time.

AWS guidance: By default, logs are kept indefinitely and never expire in CloudWatch. You can adjust the retention policy for each log group, keeping the indefinite retention, or choosing a retention period between 10 years and one day.

Use Amazon S3 for log archival from CloudWatch and apply object lifecycle management and archival policy to the bucket. You can use Azure Storage for central log archival by transferring the files from Amazon S3 to Azure Storage.

GCP guidance: By default, Operations Suite Cloud Logging retains the logs for 30 days, unless you configure custom retention for the Cloud Logging bucket. Admin Activity audit logs, System Event audit logs, and Access Transparency logs are retained 400 days by default. You can configure Cloud Logging to retain logs between 1 day and 3650 days.

Use Cloud Storage for log archival from Cloud Logging and apply object lifecycle management and archival policy to the bucket. You can use Azure Storage for central log archival by transferring the files from Google Cloud Storage to Azure Storage.

