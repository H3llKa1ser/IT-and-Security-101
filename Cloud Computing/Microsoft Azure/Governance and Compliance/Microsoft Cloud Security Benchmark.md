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

