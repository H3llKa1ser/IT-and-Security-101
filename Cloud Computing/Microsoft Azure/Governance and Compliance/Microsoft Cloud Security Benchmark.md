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

