# Design and evaluate threat detection coverage by using MITRE ATT&CK matrices, including Cloud, Enterprise, Mobile, and ICS

MITRE ATT&CK is a publicly accessible knowledge base of tactics and techniques that are commonly used by attackers, and is created and maintained by observing real-world observations. Many organizations use the MITRE ATT&CK knowledge base to develop specific threat models and methodologies that are used to verify security status in their environments.

## ATT&CK matrices

MITRE ATT&CK includes three matrices in its attack framework. Each matrix is a threat model with multiple tactics or goals along with techniques for achieving those goals in a specific type of environment:

1) Enterprise - a threat model that describes what an attacker might do in a corporate network.

2) Mobile - a threat model that describes what an attacker might do to infiltrate mobile devices.

3) ICS - a threat model that describes potential attacks on an Industrial Control System (ICS).

## MITRE ATT&CK and Microsoft Sentinel

Microsoft Sentinel analyzes ingested data, not only to detect threats and help you investigate, but also to visualize the nature and coverage of your organization's security status.

This article describes how to use the MITRE page in Microsoft Sentinel to view the detections already active in your workspace, and those available for you to configure, to understand your organization's security coverage, based on the tactics and techniques from the MITRE ATT&CK® framework.

![image](https://github.com/user-attachments/assets/ca770515-c7a0-441f-a11b-b58e37a01eae)

Microsoft Sentinel is currently aligned to The MITRE ATT&CK framework, version 13.

## View current MITRE coverage

In Microsoft Sentinel, in the Threat management menu on the left, select MITRE. By default, both currently active scheduled query and near real-time (NRT) rules are indicated in the coverage matrix.

1) Use the legend at the top-right to understand how many detections are currently active in your workspace for specific technique.

2) Use the search bar at the top-left to search for a specific technique in the matrix, using the technique name or ID, to view your organization's security status for the selected technique.

3) Select a specific technique in the matrix to view more details on the right. There, use the links to jump to any of the following locations:

Select View technique details for more information about the selected technique in the MITRE ATT&CK framework knowledge base.

Select links to any of the active items to jump to the relevant area in Microsoft Sentinel.

## Simulate possible coverage with available detections

In the MITRE coverage matrix, simulated coverage refers to detections that are available, but not currently configured, in your Microsoft Sentinel workspace. View your simulated coverage to understand your organization's possible security status, were you to configure all detections available to you.

In Microsoft Sentinel, in the General menu on the left, select MITRE.

Select items in the Simulate menu to simulate your organization's possible security status.

1) Use the legend at the top-right to understand how many detections, including analytics rule templates or hunting queries, are available for you to configure.

2) Use the search bar at the top-left to search for a specific technique in the matrix, using the technique name or ID, to view your organization's simulated security status for the selected technique.

3) Select a specific technique in the matrix to view more details on the right. There, use the links to jump to any of the following locations:

Select View technique details for more information about the selected technique in the MITRE ATT&CK framework knowledge base.

Select links to any of the simulation items to jump to the relevant area in Microsoft Sentinel.

For example, select Hunting queries to jump to the Hunting page. There, you'll see a filtered list of the hunting queries that are associated with the selected technique, and available for you to configure in your workspace.

## Use the MITRE ATT&CK framework in analytics rules and incidents

Having a scheduled rule with MITRE techniques applied running regularly in your Microsoft Sentinel workspace enhances the security status shown for your organization in the MITRE coverage matrix.

1) Analytics rules:

When configuring analytics rules, select specific MITRE techniques to apply to your rule.

When searching for analytics rules, filter the rules displayed by technique to find your rules quicker.

2) Incidents:

When incidents are created for alerts that are surfaced by rules with MITRE techniques configured, the techniques are also added to the incidents.

3) Threat hunting:

When creating a new hunting query, select the specific tactics and techniques to apply to your query.

When searching for active hunting queries, filter the queries displayed by tactics by selecting an item from the list above the grid. Select a query to see tactic and technique details on the right.

When creating bookmarks, either use the technique mapping inherited from the hunting query, or create your own mapping.
