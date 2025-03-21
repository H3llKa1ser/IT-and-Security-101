# Azure Blueprints

Just as a blueprint allows an engineer or an architect to sketch a project's design parameters, Azure Blueprints enables cloud architects and central information technology groups to define a repeatable set of Azure resources that implements and adheres to an organization's standards, patterns, and requirements. Azure Blueprints makes it possible for development teams to rapidly build and start up new environments with trust they're building within organizational compliance with a set of built-in components, such as networking, to speed up development and delivery.

Blueprints are a declarative way to orchestrate the deployment of various resource templates and other artifacts such as:

1) Role Assignments

2) Policy Assignments

3) Azure Resource Manager templates (Azure Resource Manager templates)

4) Resource Groups

The Azure Blueprints service is backed by the globally distributed Azure Cosmos DB. Blueprint objects are replicated to multiple Azure regions. This replication provides low latency, high availability, and consistent access to your blueprint objects, regardless of which region Azure Blueprints deploys your resources to.

## How it's different from Azure Resource Manager templates

The service is designed to help with environment setup. This setup often consists of a set of resource groups, policies, role assignments, and Azure Resource Manager template deployments. A blueprint is a package to bring each of these artifact types together and allow you to compose and version that package, including through a continuous integration and continuous delivery (CI/CD) pipeline. Ultimately, each is assigned to a subscription in a single operation that can be audited and tracked.

Nearly everything that you want to include for deployment in Azure Blueprints can be accomplished with an Azure Resource Manager template. However, an Azure Resource Manager template is a document that doesn't exist natively in Azure - each is stored either locally or in source control or in Templates (preview). The template gets used for deployments of one or more Azure resources, but once those resources deploy there's no active connection or relationship to the template.

With Azure Blueprints, the relationship between the blueprint definition (what should be deployed) and the blueprint assignment (what was deployed) is preserved. This connection supports improved tracking and auditing of deployments. Azure Blueprints can also upgrade several subscriptions at once that are governed by the same blueprint.

There's no need to choose between an Azure Resource Manager template and a blueprint. Each blueprint can consist of zero or more Azure Resource Manager template artifacts. This support means that previous efforts to develop and maintain a library of Azure Resource Manager templates are reusable in Azure Blueprints.

## How it's different from Azure Policy

A blueprint is a package or container for composing focus-specific sets of standards, patterns, and requirements related to the implementation of Azure cloud services, security, and design that can be reused to maintain consistency and compliance.

A policy is a default allow and explicit deny system focused on resource properties during deployment and for already existing resources. It supports cloud governance by validating that resources within a subscription adhere to requirements and standards.

Including a policy in a blueprint enables the creation of the right pattern or design during assignment of the blueprint. The policy inclusion makes sure that only approved or expected changes can be made to the environment to protect ongoing compliance to the intent of the blueprint.

A policy can be included as one of many artifacts in a blueprint definition. Blueprints also support using parameters with policies and initiatives.

## Blueprint Definition

A blueprint is composed of artifacts. Azure Blueprints currently supports the following resources as artifacts:

| Resource                      | Hierarchy options       | Description |
|--------------------------------|------------------------|-------------|
| **Resource Groups**            | Subscription          | Create a new resource group for use by other artifacts within the blueprint. These placeholder resource groups enable you to organize resources exactly the way you want them structured and provide a scope limiter for included policy and role assignment artifacts and Azure Resource Manager templates. |
| **Azure Resource Manager template** | Subscription, Resource Group | Templates, including nested and linked templates, are used to compose complex environments. Example environments: a SharePoint farm, Azure Automation State Configuration, or a Log Analytics workspace. |
| **Policy Assignment**          | Subscription, Resource Group | Allows assignment of a policy or initiative to the subscription the blueprint is assigned to. The policy or initiative must be within the scope of the blueprint definition location. If the policy or initiative has parameters, these parameters are assigned at creation of the blueprint or during blueprint assignment. |
| **Role Assignment**            | Subscription, Resource Group | Add an existing user or group to a built-in role to make sure the right people always have the right access to your resources. Role assignments can be defined for the entire subscription or nested to a specific resource group included in the blueprint. |

#### NOTE: Each artifact must be 2 MB or less. If the artifact exceeds 2 MB, you'll get an HTTP 500 error (Internal Server Error).

### Blueprint Definition Locations

When creating a blueprint definition, you'll define where the blueprint is saved. Blueprints can be saved to a management group or subscription that you have Contributor access to. If the location is a management group, the blueprint is available to assign to any child subscription of that management group.

### Blueprint parameters

Blueprints can pass parameters to either a policy/initiative or an Azure Resource Manager template. When adding either artifact to a blueprint, the author decides to provide a defined value for each blueprint assignment or to allow each blueprint assignment to provide a value at assignment time. This flexibility provides the option to define a pre-determined value for all uses of the blueprint or to enable that decision to be made at the time of assignment.

#### NOTE: A blueprint can have its own parameters, but these can currently only be created if a blueprint is generated from REST API instead of through the Portal. For more information, see blueprint parameters.

### Blueprint publishing

When a blueprint is first created, it's considered to be in Draft mode. When it's ready to be assigned, it needs to be Published. Publishing requires defining a Version string (letters, numbers, and hyphens with a max length of 20 characters) along with optional Change notes. The Version differentiates it from future changes to the same blueprint and allows each version to be assigned. This versioning also means different Versions of the same blueprint can be assigned to the same subscription. When additional changes are made to the blueprint, the Published Version still exists, as do the Unpublished changes. Once the changes are complete, the updated blueprint is Published with a new and unique Version and can now also be assigned.

## Blueprint assignment

Each Published Version of a blueprint can be assigned (with a max name length of 90 characters) to an existing management group or subscription. In the portal, the blueprint defaults the Version to the one Published most recently. If there are artifact parameters or blueprint parameters, then the parameters are defined during the assignment process.

#### NOTE: Assigning a blueprint definition to a management group means the assignment object exists at the management group. The deployment of artifacts still targets a subscription. To perform a management group assignment, the Create Or Update REST API must be used and the request body must include a value for properties.scope to define the target subscription.

## Permissions in Azure Blueprints

To use blueprints, you must be granted permissions through Azure role-based access control (Azure RBAC). To read or view a blueprint in Azure portal, your account must have read access to the scope where the blueprint definition is located.

To create blueprints, your account needs the following permissions:

1) Microsoft.Blueprint/blueprints/write - Create a blueprint definition

2) Microsoft.Blueprint/blueprints/artifacts/write - Create artifacts on a blueprint definition

3) Microsoft.Blueprint/blueprints/versions/write - Publish a blueprint

To delete blueprints, your account needs the following permissions:

1) Microsoft.Blueprint/blueprints/delete

2) Microsoft.Blueprint/blueprints/artifacts/delete

3) Microsoft.Blueprint/blueprints/versions/delete

#### NOTE: The blueprint definition permissions must be granted or inherited on the management group or subscription scope where it is saved.

To assign or unassign a blueprint, your account needs the following permissions:

1) Microsoft.Blueprint/blueprintAssignments/write - Assign a blueprint

2) Microsoft.Blueprint/blueprintAssignments/delete - Unassign a blueprint

#### NOTE: As blueprint assignments are created on a subscription, the blueprint assign and unassign permissions must be granted on a subscription scope or be inherited onto a subscription scope.

The following built-in roles are available:

| Azure Role             | Description |
|------------------------|-------------|
| **Owner**             | In addition to other permissions, includes all Azure Blueprints related permissions. |
| **Contributor**       | In addition to other permissions, can create and delete blueprint definitions, but doesn't have blueprint assignment permissions. |
| **Blueprint Contributor** | Can manage blueprint definitions, but not assign them. |
| **Blueprint Operator**  | Can assign existing published blueprints, but can't create new blueprint definitions. Blueprint assignment only works if the assignment is done with a user-assigned managed identity. |

If these built-in roles don't fit your security needs, consider creating a custom role.

#### NOTE: If using a system-assigned managed identity, the service principal for Azure Blueprints requires the Owner role on the assigned subscription in order to enable deployment. If using the portal, this role is automatically granted and revoked for the deployment. If using the REST API, this role must be manually granted, but is still automatically revoked after the deployment completes. If using a user-assigned managed identity, only the user creating the blueprint assignment needs the Microsoft.Blueprint/blueprintAssignments/write permission, which is included in both the Owner and Blueprint Operator built-in roles.

## Naming Limits

The following limitations exist for certain fields:

| Object                | Field     | Allowed Characters                           | Max. Length |
|-----------------------|----------|----------------------------------------------|-------------|
| **Blueprint**         | Name     | letters, numbers, hyphens, and underscores  | 48          |
| **Blueprint**         | Version  | letters, numbers, hyphens, and periods      | 20          |
| **Blueprint assignment** | Name | letters, numbers, hyphens, and underscores  | 90          |
| **Blueprint artifact**   | Name | letters, numbers, hyphens, and periods      | 48          |

## Architecture

The foundational environment created by this blueprint sample is based on the architecture principals of a hub and spoke model. The blueprint deploys a hub virtual network that contains common and shared resources, services, and artifacts such as Azure Bastion, gateway and firewall for connectivity, management and jump box subnets to host additional/optional management, maintenance, administration, and connectivity infrastructure. One or more spoke virtual networks are deployed to host application workloads such as web and database services. Spoke virtual networks are connected to the hub virtual network using Azure virtual network peering for seamless and secure connectivity. Additional spokes can be added by reassigning the sample blueprint or manually creating an Azure virtual network and peering it with the hub virtual network. All external connectivity to the spoke virtual network(s) and subnet(s) is configured to route through the hub virtual network and, via firewall, gateway, and management jump boxes.

![image](https://github.com/user-attachments/assets/e1f6007c-e387-4fbc-8d22-25ef1dbec998)

This blueprint deploys several Azure services to provide a secure, monitored, enterprise-ready foundation. This environment is composed of:

This blueprint deploys several Azure services to provide a secure, monitored, enterprise-ready foundation. This environment is composed of:

1) Azure Monitor Logs and an Azure storage account to ensure resource logs, activity logs, metrics, and networks traffic flows are stored in a central location for easy querying, analytics, archival, and alerting.

2) MIcrosoft Dedender for Cloud (standard version) to provide threat protection for Azure resources.

3) Azure Virtual Network in the hub supporting subnets for connectivity back to an on-premises network, an ingress and egress stack to/for Internet connectivity, and optional subnets for deployment of additional administrative or management services. Virtual Network in the spoke contains subnets for hosting application workloads. Additional subnets can be created after deployment as needed to support applicable scenarios.

4) Azure Firewall to route all outbound internet traffic and to enable inbound internet traffic via jump box. (Default firewall rules block all internet inbound and outbound traffic and rules must be configured after deployment, as applicable.)

5) Network security groups (NSGs) assigned to all subnets (except service-owned subnets such as Azure Bastion, Gateway and Azure Firewall) configured to block all internet inbound and outbound traffic.

6) Application security groups to enable grouping of Azure Virtual Machines to apply common network security policies.

7) Route tables to route all outbound internet traffic from subnets through the firewall. (Azure Firewall and NSG rules will need to be configured after deployment to open connectivity.)

8) Azure Network Watcher to monitor, diagnose, and view metrics of resources in the Azure virtual network.

9) Azure DDoS Protection to protect Azure resources against DDoS attacks.

10) Azure Bastion to provide seamless and secure connectivity to a virtual machine that does not require a public IP address, agent, or special client software.

11) Azure VPN Gateway to enable encrypted traffic between an Azure virtual network and an on-premises location over the public Internet.

The Azure Security Benchmark Foundation lays out a foundational architecture for workloads.

