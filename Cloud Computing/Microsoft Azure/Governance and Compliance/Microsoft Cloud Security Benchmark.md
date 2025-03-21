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

