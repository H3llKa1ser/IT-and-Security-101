# Microsoft Security Graph

Microsoft Graph provides a unified programmability model that you can use to access the data in Microsoft 365, Windows, and Enterprise Mobility + Security. You can use the data in Microsoft Graph to build customized apps for your organization.

The Microsoft Graph API offers a single endpoint, https://graph.microsoft.com (either v1.0 or beta versions). You can use REST APIs or SDKs to access the endpoint and build apps that support Microsoft 365 scenarios. Microsoft Graph also includes a powerful set of services that manage user and device identity, access, compliance, and security and help protect organizations from data leakage or loss.

## What's in Microsoft Graph?

Microsoft Graph exposes REST APIs and client libraries to access data on the following Microsoft cloud services:

1) Microsoft 365 core services: Bookings, Calendar, Delve, Excel, Microsoft Purview eDiscovery, Microsoft Search, OneDrive, OneNote, Outlook/Exchange, People (Outlook contacts), Planner, SharePoint, Teams, To Do, Viva Insights

2) Enterprise Mobility + Security services: Advanced Threat Analytics, Advanced Threat Protection, Microsoft Entra ID, Identity Manager, and Intune

3) Windows services: activities, devices, notifications, Universal Print

4) Dynamics 365 Business Central services

## Microsoft Graph Security API

The Microsoft Graph security API is an intermediary service (or broker) that provides a single programmatic interface to connect multiple Microsoft Graph security providers (also called security providers or providers). Requests to the Microsoft Graph security API are federated to all applicable security providers. The results are aggregated and returned to the requesting application in a common schema, as shown in the following diagram.

![image](https://github.com/user-attachments/assets/d8f6276a-33f7-40cf-99dc-2d2d393c5b43)

Developers can use the Security Graph to build intelligent security services that:

1) Integrate and correlate security alerts from multiple sources.

2) Stream alerts to security information and event management (SIEM) solutions.

3) Automatically send threat indicators to Microsoft security solutions to enable alert, block, or allow actions.

4) Unlock contextual data to inform investigations.

5) Discover opportunities to learn from the data and train your security solutions.

6) Automate SecOps for greater efficiency.

## Use the Microsoft Graph Security API

There are two versions of the Microsoft Graph Security API.

1) Microsoft Graph REST API v1.0

2) Microsoft Graph REST API Beta

The beta version provides new or enhanced APIs that are still in preview status. APIs in preview status are subject to change, and may break existing scenarios without notice.

For Security Operations Analysts, both Microsoft Graph API versions support advanced hunting using the runHuntingQuery method. This method includes a query in Kusto Query Language (KQL).

