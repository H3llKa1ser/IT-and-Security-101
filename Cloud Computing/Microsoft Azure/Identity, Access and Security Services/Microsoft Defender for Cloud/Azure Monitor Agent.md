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

