# Defender for Servers

The Defender for Servers plan in Microsoft Defender for Cloud reduces security risk and exposure for machines in your organization by providing actionable recommendations to improve and remediate security posture. Defender for Servers also helps to protect machines against real-time security threats and attacks.

#### NOTE: Support for using the Log Analytics agent and Azure Monitoring Agent (AMA) in Defender for Servers has ended. For most plan features, the use of these agents is replaced by agentless machine scanning, or by integration with Microsoft Defender for Endpoint.

## Benefits

Defender for Servers provides a number of security benefits.

1) Protect multicloud and on-premises machines: Defender for Servers protects Windows and Linux machines in multicloud environments (Azure, AWS, GCP), and on-premises.

2) Centralize management and reporting: Defender for Cloud provides a single view of monitored resources, including machines protected by Defender for Servers. You can filter, sort, and cross-reference data to understand, investigate, and analyze machine security.

3) Integrate with Defender services: Defender for Servers integrates natively with security capabilities provided by Defender for Endpoint and Microsoft Defender Vulnerability Management.

4) Improve posture and reduce risk: Defender for Servers assesses the security posture of machines against compliance standards, and provides actionable security recommendations to remediate and improve security posture.

5) Benefit from agentless scanning: Defender for Servers Plan 2 provides agentless machine scanning. Without the need for an agent on endpoints, you can scan software inventory, assess machines for vulnerabilities, scan for machine secrets, and detect malware threats.

6) Protect against threats in near real-time: Defender for Servers identifies and analyzes real-time threats, and issues security alerts as needed.

7) Get intelligent threat detection: Defender for Cloud evaluates events and detects threats using advanced security analytics and machine-learning technologies with multiple threat intelligence sources, including Microsoft Security Response Center (MSRC).

## Defender for Endpoint integration

Defender for Endpoint and Defender for Vulnerability Management integrate natively into Defender for Cloud.

This default integration allows Defender for Servers to take advantage of the endpoint detection and response (EDR) capabilities of Defender for Endpoint, and the vulnerability scanning, software inventory, and premium features provided by Defender for Vulnerability Management.

## Defender for Servers plans

Defender for Servers offers two plans:

1) Defender for Servers Plan 1 is entry-level, and focuses on the EDR capabilities provided by the Defender for Endpoint integration.

2) Defender for Servers Plan 2 provides the same features as Plan 1, and additional capabilities.

## Plan protection features

| Feature                                   | Plan Support           | Details |
|-------------------------------------------|------------------------|---------|
| **Multicloud and hybrid support**         | Plan 1 and 2           | Defender for Servers can protect Azure VMs, AWS/GCP VMs, and on-premises machines connected to Defender for Cloud. |
| **Defender for Endpoint automatic onboarding** | Plan 1 and 2           | Defender for Cloud automatically onboards machines to Defender for Endpoint by installing the Defender for Endpoint extension on connected machines. |
| **Defender for Endpoint EDR**             | Plan 1 and 2           | Supported endpoints receive near real-time threat detection using Defender for Endpoint EDR capabilities. |
| **Threat detection (OS-level)**           | Plan 1 and 2           | Integration with Defender for Endpoint provides OS-level threat detection. |
| **Integrated alerts and incidents**       | Plan 1 and 2           | Defender for Endpoint alerts and incidents for connected machines are displayed in Defender for Cloud, with drill-down in the Defender portal. |
| **Threat detection (Azure network layer)** | Plan 2 only            | Agentless detection detects threats targeting the control plane on the network, including network-based security alerts for Azure VMs. |
| **Software inventory discovery**          | Plan 1 and 2           | Software inventory discovery (provided by Defender Vulnerability Management) is integrated into Defender for Cloud. |
| **Vulnerability scanning (agent-based)**  | Plan 1 and 2           | With the Defender for Endpoint agent, Defender for Servers assesses machines for vulnerabilities using Defender Vulnerability Management. |
| **Vulnerability scanning (agentless)**    | Plan 2 only            | Defender for Cloud provides agentless vulnerability assessment using Defender Vulnerability Management, in addition to agent-based scanning. |
| **OS baseline misconfigurations**         | Plan 2 only            | Defender for Cloud assesses and enforces security configurations using built-in Azure policy initiatives, including Microsoft Cloud Security Benchmark (MCSB). |
| **Regulatory compliance assessment**      | Plan 1 and 2           | Defender for Cloud provides default compliance standards. Additional compliance standards are available with a paid Defender for Servers plan. |
| **OS system updates**                     | Plan 2 only            | Defender for Servers assesses machines to ensure updates and patches are installed, using Azure Update Manager. |
| **Defender for Vulnerability Management premium features** | Plan 2 only | Includes premium features like certificate assessments and OS security baseline assessments, available in the Defender portal. |
| **Malware scanning (agentless)**          | Plan 2 only            | Defender for Servers Plan 2 provides malware scanning as part of its agentless scanning capabilities. |
| **Machine secrets scanning (agentless)**  | Plan 2 only            | Defender for Cloud scans machines for plaintext secrets. Also available in Defender Cloud Security Posture Management (CSPM). |
| **File integrity monitoring**             | Plan 2 only            | Examines files and registries for changes that might indicate an attack. Uses Defender for Endpoint extension for collection. |
| **Just-in-time virtual machine access**   | Plan 2 only            | Locks down machine ports to reduce the attack surface. |
| **Network map**                           | Plan 2 only            | Provides a geographical view of recommendations for hardening network resources. |
| **Free data ingestion (500 MB)**          | Plan 2 only            | Free data ingestion for specific data types in Log Analytics workspaces. |

## Deployment scope

We recommend enabling Defender for Servers at subscription level, but you can enable and disable Defender for Servers at resource level if you need deployment granularity, as follows:

| Scope                        | Plan 1 | Plan 2 |
|------------------------------|--------|--------|
| **Enable for an Azure subscription** | Yes    | Yes    |
| **Enable for a resource**    | Yes    | No     |
| **Disable for a resource**   | Yes    | Yes    |

## After enabling

After a plan is enabled the following applies:

Trial period: 30-day trial period begins. There is no way to stop, pause, or extend this trial period. To enjoy the full 30-day trial, plan ahead to meet your evaluation goals.

Endpoint protection: The Defender for Endpoint extension is automatically installed on all supported machines connected to Defender for Cloud. You can disable automatic provisioning if you need to.

Vulnerability assessment: Defender Vulnerability Management is enabled by default on machines with the Defender for Endpoint extension installed.

Agentless scanning: Agentless scanning is enabled by default when you turn on Defender for Servers Plan 2.

OS configuration assessment: When you enable Defender for Servers Plan 2, Defender for Cloud assesses operation system configuration settings against compute security baselines in Microsoft Cloud Security Benchmark. To use this feature, machines must be running the Azure machine configuration extension. Learn more about setting up the extension.

File integrity monitoring: You set up file integrity monitoring after enabling Defender for Servers Plan 2.
