# Azure Monitor Agent

The Azure Monitor Agent collects monitoring data from the guest operating system of Azure and hybrid virtual machines (VMs). It delivers the data to Azure Monitor for use by features, insights, and other services, such as Microsoft Sentinel and Microsoft Defender for Cloud. This article gives you an overview of the capabilities and supported use cases for the Azure Monitor Agent.

#### NOTE: The Azure Monitor Agent replaces the legacy Log Analytics agent for Azure Monitor. The Log Analytics agent is deprecated and isn't supported as of August 31, 2024. If you use the Log Analytics agent to ingest data to Azure Monitor, migrate now to the Azure Monitor Agent.

## Installation

The Azure Monitor Agent is one method of data collection for Azure Monitor. It's installed on VMs running in Azure, in other clouds, or on-premises, where it has access to local logs and performance data. Without the agent, you can collect data only from the host machine because you would have no access to the client operating system and to running processes.

The agent can be installed by using different methods, as described in Install and manage the Azure Monitor Agent. You can install the agent on a single machine or at scale by using Azure Policy or other tools. In some cases, the agent is automatically installed when you enable a feature that requires it, such as Microsoft Sentinel.

## Data collection

The Azure Monitor Agent collects all data by using a data collection rule (DCR). In a DCR, you define the following information:

1) The data type that's collected

2) How to transform the data, including filtering, aggregating, and shaping

3) The destination for collected data

A single DCR can contain multiple data sources of different types. Depending on your requirements, you can choose whether to include several data sources in a few DCRs or create separate DCRs for each data source. If you create separate DCRs for each data source, you can centrally define the logic for different data collection scenarios and apply them to different sets of machines. For recommendations on how to organize your DCRs, see Best practices for DCR creation and management in Azure Monitor.

A DCR is applied to a particular agent by creating a data collection rule association (DCRA) between the DCR and the agent. One DCR can be associated with multiple agents, and each agent can be associated with multiple DCRs. When an agent is installed, it connects to Azure Monitor to retrieve any DCRs that are associated with it. The agent periodically checks back with Azure Monitor to determine if there are any changes to existing DCRs or associations with new ones.

## Cost

There's no cost to use the Azure Monitor Agent, but you might incur charges for the data that's ingested and stored. For information on Log Analytics data collection and retention and for customer metrics, see Azure Monitor logs cost calculations and options and Analyze usage in a Log Analytics workspace.

## Supported regions

The Azure Monitor Agent is available for general availability features in all global Azure regions, Azure Government, and Azure operated by 21Vianet. It's not yet supported in air-gapped clouds. For more information, see Product availability by region.

## Collect data with Azure Monitor Agent

Azure Monitor agent (AMA) is used to collect data from Azure virtual machines, Virtual Machine scale sets, and Arc-enabled servers. Data collection rules (DCR) define the data to collect from the agent and where that data should be sent. This article describes how to use the Azure portal to create a DCR to collect different types of data and install the agent on any machines that require it.

If you're new to Azure Monitor or have basic data collection requirements, then you may be able to meet all of your requirements using the Azure portal and the guidance in this article. If you want to take advantage of additional DCR features such as transformations, then you may need to create a DCR using other methods or edit it after creating it in the portal. You can also use different methods to manage DCRs and create associations if you want to deploy using CLI, PowerShell, ARM templates, or Azure Policy.

#### NOTE: To send data across tenants, you must first enable Azure Lighthouse.

#### NOTE: The following cases may collect duplicate data which may result in additional charges.

Creating multiple DCRs with the same data source and associating them to the same agent. Ensure that you're filtering data in the DCRs such that each collects unique data.

Creating a DCR that collects security logs and enabling Sentinel for the same agents. In this case, you may collect the same events in the Event table and the SecurityEvent table.

Using both the Azure Monitor agent and the legacy Log Analytics agent on the same machine. Limit duplicate events to only the time when you transition from one agent to the other.

## Data sources

The table below lists the types of data you can currently collect with the Azure Monitor Agent and where you can send that data. The link for each is to an article describing the details of how to configure that data source. Follow this article to create the DCR and assign it to resources, and then follow the linked article to configure the data source.

| Data Source          | Description                                                   | Client OS | Destinations                  |
|----------------------|---------------------------------------------------------------|-----------|------------------------------|
| **Windows events**   | Information sent to the Windows event logging system, including Sysmon events. | Windows   | Log Analytics workspace      |
| **Performance counters** | Numerical values measuring performance of different aspects of the OS and workloads. | Windows, Linux | Azure Monitor Metrics (Preview), Log Analytics workspace |
| **Syslog**           | Information sent to the Linux event logging system.          | Linux     | Log Analytics workspace      |
| **Text log**         | Information sent to a text log file on a local disk.         | Windows, Linux | Log Analytics workspace  |
| **JSON log**         | Information sent to a JSON log file on a local disk.         | Windows, Linux | Log Analytics workspace  |
| **IIS logs**         | Internet Information Service (IIS) logs from the local disk of Windows machines. | Windows   | Log Analytics workspace      |

#### NOTE: Azure Monitor Agent also supports Azure service SQL Best Practices Assessment which is currently Generally available. For more information, refer Configure best practices assessment using Azure Monitor Agent.

## Prerequisites

Permissions to create Data Collection Rule objects in the workspace.

See the article describing each data source for any additional prerequisites.

## Create data collection rule (DCR)

The Azure portal provides a simplified experience for creating a DCR for virtual machines and virtual machine scale sets. Using this method, you don't need to understand the structure of a DCR unless you want to implement an advanced feature such as a transformation. You can also use other creation methods described in Create data collection rules (DCRs) in Azure Monitor.

On the Monitor menu in the Azure portal, select Data Collection Rules > Create to open the DCR creation page.

The Basic page includes basic information about the DCR.

| Setting                | Description |
|------------------------|-------------|
| **Rule Name**         | Name for the DCR. The name should be something descriptive that helps you identify the rule. |
| **Subscription**      | Subscription to store the DCR. The subscription doesn't need to be the same as the virtual machines. |
| **Resource group**    | Resource group to store the DCR. The resource group doesn't need to be the same as the virtual machines. |
| **Region**           | Region to store the DCR. Must match the region of any Log Analytics or Azure Monitor workspace used as a destination. If you have workspaces in different regions, create multiple DCRs for the same set of machines. |
| **Platform Type**     | Specifies the type of data sources for the DCR (Windows or Linux). "None" allows for both. |
| **Data Collection Endpoint (DCE)** | Specifies the DCE used to collect data. Required only if using Azure Monitor Private Links. The DCE must be in the same region as the DCR. |

#### NOTE: This option sets the kind attribute in the DCR. There are other values that can be set for this attribute, but they aren't available in the portal.

## Data collection rules (DCRs) in Azure Monitor

Data collection rules (DCRs) are part of an ETL-like data collection process that improves on legacy data collection methods for Azure Monitor. This process uses a common data ingestion pipeline for all data sources and a standard method of configuration that's more manageable and scalable than previous collection methods.

Specific advantages of DCR-based data collection include the following:

1) Consistent method for configuration of different data sources.

2) Ability to apply a transformation to filter or modify incoming data before it's sent to a destination.

3) Scalable configuration options supporting infrastructure as code and DevOps processes.

4) Option of edge pipeline in your own environment to provide high-end scalability, layered network configurations, and periodic connectivity.

## Viewing DCRs

Data collection rules (DCRs) are stored in Azure so they can be centrally deployed and managed like any other Azure resource. They provide a consistent and centralized way to define and customize different data collection scenarios.

View all of the DCRs in your subscription from the Data Collection Rules option of the Monitor menu in the Azure portal. Regardless of the method used to create the DCR and the details of the DCR itself, all DCRs in the subscription are listed in this screen.

## Replaced legacy data collection methods

The DCR collection process has either replaced or is in the process of replacing other data collection methods in Azure Monitor. The following table lists the legacy methods with their DCR-based replacements.

| **Legacy Method**         | **DCR Method**            | **Description** |
|---------------------------|---------------------------|-----------------|
| **Log Analytics agent**   | **Azure Monitor agent**   | The Azure Monitor agent is now used to monitor VMs and Kubernetes clusters supporting VM insights and Container insights. |
| **Diagnostic settings (metrics only)** | **Metrics export** | Diagnostic settings are still currently used to collect resource logs from Azure resources. Platform metrics can now be collected using Metrics export. |
| **Data Collector API**    | **Logs ingestion API**    | The Logs ingestion API is used to send data to a Log Analytics workspace from any REST client. It replaces the Data Collector API, which was less secure and less functional. |

## Azure Monitor Pipeline

The data collection process supported by DCRs is based on the Azure Monitor pipeline which provides a common processing path for incoming data. The cloud pipeline is one component of the Azure Monitor pipeline (see Edge pipeline below for the other component) and is automatically available in your Azure subscription as part of the Azure Monitor platform. It requires no configuration, and doesn't appear in the Azure portal.

Each data collection scenario using the Azure Monitor pipeline is defined in a DCR that provides instructions for how the cloud pipeline should process data it receives. Depending on the scenario, DCRs will specify all or some of the following:

1) Data to collect and send to the pipeline.

2) Schema of the incoming data.

3) Transformations to apply to the data before it's stored.

4) Destination where the data should be sent.

## Using a DCR

There are two fundamental ways that DCRs are specified for a particular data collection scenario as described in the following sections. Each scenario will support one of these methods, but not both.

#### NOTE: Workspace transformation DCRs are active as soon as they're created. They don't use either of the methods described in this section.

### Data collection rule associations (DCRA)

Data collection rule associations (DCRAs) are used to associate a DCR with a monitored resource. This is a many-to-many relationship, where a single DCR can be associated with multiple resources, and a single resource can be associated with multiple DCRs. This allows you to develop a strategy for maintaining your monitoring across sets of resources with different requirements.

For example, the following diagram illustrates data collection for Azure Monitor agent (AMA) running on a virtual machine. When the agent is installed, it connects to Azure Monitor to retrieve any DCRs that are associated with it. In this scenario, the DCRs specify events and performance data to collect, which the agent uses to determine what data to collect from the machine and send to Azure Monitor. Once the data is delivered, the cloud pipeline runs any transformation specified in the DCR to filter and modify the data and then sends the data to the specified workspace and table.

### Direct ingestion

With direct ingestion, a particular DCR is specified to process the incoming data. For example, the following diagram illustrates data from a custom application using Logs ingestion API. Each API call specifies the DCR that will process its data. The DCR understands the structure of the incoming data, includes a transformation that ensures that the data is in the format of the target table, and specifies a workspace and table to send the transformed data.

## Transformations

Transformations are KQL queries included in a DCR that run against each record sent to the cloud pipeline. They allow you to modify incoming data before it's stored in Azure Monitor or sent to another destination. You may filter unneeded data to reduce your ingestion costs, remove sensitive data that shouldn't be persisted in the Log Analytics workspace, or format data to ensure that it matches the schema of its destination. Transformations also enable advanced scenarios such as sending data to multiple destinations or enriching data with additional information.

## Edge Pipeline

The edge pipeline extends the Azure Monitor pipeline to your own data center. It enables at-scale collection and routing of telemetry data before it's delivered to the cloud pipeline. Unlike the cloud pipeline, the edge pipeline is optional and requires configuration.

Specific use cases for Azure Monitor edge pipeline are:

1) Scalability. The edge pipeline can handle large volumes of data from monitored resources that may be limited by other collection methods such as Azure Monitor agent.

2) Periodic connectivity. Some environments may have unreliable connectivity to the cloud, or may have long unexpected periods without connection. The edge pipeline can cache data locally and sync with the cloud when connectivity is restored.

3) Layered network. In some environments, the network is segmented and data cannot be sent directly to the cloud. The edge pipeline can be used to collect data from monitored resources without cloud access and manage the connection to Azure Monitor in the cloud.

## DCR regions

Data collection rules are available in all public regions where Log Analytics workspaces and the Azure Government and China clouds are supported. Air-gapped clouds aren't yet supported. A DCR gets created and stored in a particular region and is backed up to the paired-region within the same geography. The service is deployed to all three availability zones within the region. For this reason, it's a zone-redundant service, which further increases availability.

Single region data residency is a preview feature to enable storing customer data in a single region and is currently only available in the Southeast Asia Region (Singapore) of the Asia Pacific Geo and the Brazil South (Sao Paulo State) Region of the Brazil Geo. Single-region residency is enabled by default in these regions.

