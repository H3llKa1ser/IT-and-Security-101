# Design security information and event management (SIEM) solutions

Microsoft Sentinel is a cloud-native Security Information and Event Management (SIEM) and Security Orchestration, Automation, and Response (SOAR) solution. It helps enterprises collect large volumes of security data, detect and investigate potential threats, and automate response actions. By integrating with a wide array of data sources and using advanced analytics, Microsoft Sentinel streamlines security operations and reduces the time needed to address threats.

A Log Analytics workspace is a data store into which you can collect any type of log data from all of your Azure and non-Azure resources and applications. Microsoft Sentinel, and other Azure services, including Azure Monitor and Microsoft Defender for Cloud use a Log Analytics workspace as the underlying storage and analytics engine for all ingested data. Microsoft Sentinel uses the data in the workspace to power its core features, including analytics rules, threat hunting, incident investigation, and workbooks.

Because the Log Analytics workspace is where all ingested data is stored, organizations need to consider factors including the number of workspaces needed for their environment and the configuration and placement of those workspaces to meet their requirements while optimizing costs. This unit presents criteria to consider when designing your workspace architecture. For information on Microsoft Sentinel capabilities, see What is Microsoft Sentinel? For information on concepts related to Log Analytics workspaces, see Log Analytics workspace overview.

## Design strategy

Your design should always start with a single workspace to reduce the complexity of managing multiple workspaces and in querying data from them. There are no performance limitations from the amount of data in your workspace. Multiple services and data sources can send data to the same workspace. As you identify criteria to create more workspaces, your design should use the fewest number of workspaces to meet your requirements.

Designing a workspace configuration includes evaluation of multiple criteria. But some of the criteria might be in conflict. For example, you might be able to reduce egress charges by creating a separate workspace in each Azure region. Consolidating into a single workspace might allow you to reduce charges even more with a commitment tier. Evaluate each of the criteria independently. Consider your requirements and priorities to determine which design is most effective for your environment.

## Design criteria

The following table presents criteria to consider when you design your workspace architecture.

| **Criteria**                     | **Description**                                                                                                                                                              |
|-----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Operational and security data** | You may choose to combine operational data from Azure Monitor in the same workspace as security data from Microsoft Sentinel or separate them into their own workspace. Combining them gives you better visibility across all your data, while security standards might require separation for dedicated security workspaces. This also has cost implications. |
| **Azure tenants**                 | If you have multiple Azure tenants, you will usually create a workspace in each one. Several data sources can only send monitoring data to a workspace in the same Azure tenant. |
| **Azure regions**                 | Each workspace resides in a specific Azure region. You may have regulatory or compliance requirements to store data in certain locations. |
| **Data ownership**                | You might create separate workspaces based on data ownership, such as by subsidiaries or affiliated companies. |
| **Split billing**                 | By placing workspaces in separate subscriptions, they can be billed to different parties. |
| **Data retention**                | You can set different retention settings for each workspace and each table within a workspace. If you need different retention settings for different resources, separate workspaces are required. |
| **Commitment tiers**              | Commitment tiers reduce ingestion costs by committing to a minimum amount of daily data in a single workspace. |
| **Legacy agent limitations**      | Legacy virtual machine agents have limitations on the number of workspaces they can connect to. |
| **Data access control**          | Configure access to the workspace and different tables or data from various resources. |
| **Resilience**                    | To ensure data availability in the event of a region failure, you can ingest data into multiple workspaces located in different regions. |

## Work with multiple workspaces

Many designs include multiple workspaces. For example, a central security operations team might use its own Microsoft Sentinel workspaces to manage centralized artifacts like analytics rules or workbooks.

Microsoft Sentinel includes features to assist you in analyzing this data across workspaces. For more information, see Extend Microsoft Sentinel across workspaces and tenants

When naming each workspace, we recommend including a meaningful indicator in the name so that you can easily identity the purpose of each workspace.

## Multiple tenant strategies

Environments with multiple Azure tenants, including Microsoft service providers (MSPs), independent software vendors (ISVs), and large enterprises, often require a strategy where a central administration team has access to administer workspaces located in other tenants. Each of the tenants might represent separate customers or different business units.

#### NOTE: For partners and service providers who are part of the Cloud Solution Provider (CSP) program, Log Analytics in Azure Monitor is one of the Azure services available in Azure CSP subscriptions.

Two basic strategies for this functionality are described in the following sections.

### Distributed architecture

In a distributed architecture, a Log Analytics workspace is created in each Azure tenant. This option is the only one you can use if you're monitoring Azure services other than virtual machines.

There are two options to allow service provider administrators to access the workspaces in the customer tenants:

1) Use Azure Lighthouse to access each customer tenant. The service provider administrators are included in a Microsoft Entra user group in the service provider's tenant. This group is granted access during the onboarding process for each customer. The administrators can then access each customer's workspaces from within their own service provider tenant instead of having to sign in to each customer's tenant individually. For more information, see Monitor customer resources at scale.

2) Add individual users from the service provider as Microsoft Entra guest users (B2B). The customer tenant administrators manage individual access for each service provider administrator. The service provider administrators must sign in to the directory for each tenant in the Azure portal to access these workspaces.

#### Advantages to this strategy:

Logs can be collected from all types of resources.

The customer can confirm specific levels of permissions with Azure delegated resource management. Or the customer can manage access to the logs by using their own Azure RBAC.

Each customer can have different settings for their workspace, such as retention and data cap.

Isolation between customers for regulatory and compliance.

The charge for each workspace is included in the bill for the customer's subscription.

#### Disadvantages to this strategy:

Running a query over a large number of workspaces is slow and can't scale above 100 workspaces. This means that you can create a central visualization and data analytics but it's slow if there are more than a few dozen workspaces. This situation is less acute if all workspaces are colocated on the same dedicated cluster. See here for more details on running queries across workspaces.

If customers aren't onboarded for Azure delegated resource management, service provider administrators must be provisioned in the customer directory. This requirement makes it more difficult for the service provider to manage many customer tenants at once.

When running a query on a workspace, the workspace admins might have visibility to the full text of the query via query audit.

### Centralized

A single workspace is created in the service provider's subscription. This option can collect data from customer virtual machines and Azure PaaS services based on diagnostics settings. Agents installed on the virtual machines and PaaS services can be configured to send their logs to this central workspace.

#### Advantages to this strategy:

It's easy to manage many customers.

The service provider has full ownership over the logs and the various artifacts, such as functions and saved queries.

A service provider can perform analytics across all of its customers.

#### Disadvantages to this strategy:

Logs can only be collected from virtual machines with an agent or Azure PaaS services (via Azure Lighthouse delegation). It won't work with SaaS connectors, or Azure Service Fabric data sources.

It might be difficult to separate data between customers because their data shares a single workspace. Queries need to use the computer's fully qualified domain name or the Azure subscription ID.

All data from all customers will be stored in the same region with a single bill and the same retention and configuration settings.

### Hybrid

In a hybrid model, each tenant has its own workspace. A mechanism is used to pull data into a central location for reporting and analytics. This data could include a small number of data types or a summary of the activity, such as daily statistics.

There are several options to implement logs in a central location:

1) Central workspace: The service provider creates a workspace in its tenant and pulls data from the various workspaces using:

A script that uses the Query API with the logs ingestion API to send the data from the tenant workspaces to the central workspace.

Azure Logic Apps to copy data to the central workspace.

Data export from the source workspace and reingestion to the central workspace. You can also create summary rules to export an aggregation of key data from the original workspaces into the central workspace.

2) Power BI: The tenant workspaces export data to Power BI by using the integration between the Log Analytics workspace and Power BI.

## Manage access to workspaces

The factors that determine which data you can access in a Log Analytics workspace are:

1) The settings on the workspace itself.

2) Your access permissions to resources that send data to the workspace.

3) The method used to access the workspace.

The factors that define the data you can access are described in the following table.

| **Factor**                         | **Description**                                                                                                                                                                                                                      |
|------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Access mode**                    | Method used to access the workspace. Defines the scope of the data available and the access control mode that's applied.                                                                                                              |
| **Access control mode**            | Setting on the workspace that defines whether permissions are applied at the workspace or resource level.                                                                                                                               |
| **Azure role-based access control (RBAC)** | Permissions applied to individuals or groups of users for the workspace or resource sending data to the workspace. Defines what data you have access to.                                                                               |
| **Table-level Azure RBAC**         | Optional permissions that define specific data types in the workspace that you can access.                                                                                                                                               |

Access mode. The access mode refers to how you access a Log Analytics workspace and defines the data you can access during the current session. The mode is determined according to the scope you select in Log Analytics.

There are two access modes:

1) Workspace-context: You can view all logs in the workspace for which you have permission. Queries in this mode are scoped to all data in tables that you have access to in the workspace. This access mode is used when logs are accessed with the workspace as the scope.

2) Resource-context: When you access the workspace for a particular resource, resource group, or subscription, such as when you select Logs from a resource menu in the Azure portal, you can view logs for only resources in all tables that you have access to. Queries in this mode are scoped to only data associated with that resource. This mode also enables granular Azure RBAC. Workspaces use a resource-context log model where every log record emitted by an Azure resource is automatically associated with this resource.

Access control mode. The access control mode is a setting on each workspace that defines how permissions are determined for the workspace.

1) Require workspace permissions. This control mode doesn't allow granular Azure RBAC. To access the workspace, the user must be granted permissions to the workspace or to specific tables.

2) Use resource or workspace permissions. This control mode allows granular Azure RBAC.

Azure RBAC. Access to a workspace is managed by using Azure RBAC. You grant access to the Log Analytics workspace by using Azure permissions. To learn more, see Workspace permissions

Table-level Azure RBAC. Table-level access settings let you grant specific users or groups read-only permission to data in a table. Users with table-level read access can read data from the specified table in both the workspace and the resource context. To learn more, see Manage table-level read access in a Log Analytics workspace.

### Manage access to Microsoft Sentinel data by resource

Typically, users who have access to a Log Analytics workspace enabled for Microsoft Sentinel also have access to all the workspace data, including security content. Administrators can use Azure roles to configure access to specific features in Microsoft Sentinel, depending on the access requirements in their team.

However, you may have some users who need to access only specific data in your workspace, but shouldn't have access to the entire Microsoft Sentinel environment. For example, you may want to provide a nonsecurity operations (non-SOC) team with access to the Windows event data for the servers they own.

In such cases, we recommend that you configure your role-based access control (RBAC) based on the resources that are allowed to your users, instead of providing them with access to the workspace or specific Microsoft Sentinel features. This method is also known as setting up resource-context RBAC.

The following table highlights the scenarios where resource-context RBAC is most helpful. Note the differences in access requirements between SOC teams and non-SOC teams.

| **Requirement type** | **SOC team**                                                                 | **Non-SOC team**                                         |
|----------------------|----------------------------------------------------------------------------|---------------------------------------------------------|
| **Permissions**       | The entire workspace                                                      | Specific resources only                                  |
| **Data access**       | All data in the workspace                                                  | Only data for resources that the team is authorized to access |
| **Experience**        | The full Microsoft Sentinel experience, possibly limited by roles and permissions | Log queries and Workbooks only                            |

The following image shows a simplified version of a workspace architecture where security and operations teams need access to different sets of data, and resource-context RBAC is used to provide the required permissions.

![image](https://github.com/user-attachments/assets/51db4124-39f1-4b51-853b-3fd2d9e3dd94)

In this image:

1) The Log Analytics workspace enabled for Microsoft Sentinel is placed in a separate subscription to better isolate permissions from the subscription that the applications teams use to host their workloads.

2) The applications teams are granted access to their respective resource groups, where they can manage their resources.

This separate subscription and resource-context RBAC allows these teams to view logs generated by any resources they have access to, even when the logs are stored in a workspace where they don't have direct access. The applications teams can access their logs via the Logs area of the Azure portal, to show logs for a specific resource, or via Azure Monitor, to show all of the logs they can access at the same time.

