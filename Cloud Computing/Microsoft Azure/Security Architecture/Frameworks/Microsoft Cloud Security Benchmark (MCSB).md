# Microsoft Cloud Security Benchmark (MCSB)

New services and features are released daily in Azure and other cloud platforms. Developers are rapidly publishing new cloud applications built on these services, and attackers are constantly seeking new ways to exploit misconfigured resources. The cloud moves fast, developers move fast, and attackers also move fast. How do you keep up and make sure that your cloud deployments are secure? How are security practices for cloud systems different from on-premises systems and different between cloud service providers? How do you monitor your workload for consistency across multiple cloud platforms?

Microsoft has found that using security benchmarks can help you quickly secure cloud deployments. A comprehensive security best practice framework from cloud service providers can give you a starting point for selecting specific security configuration settings in your cloud environment, across multiple service providers and allow you to monitor these configurations using a single pane of glass.

## Security controls

A control is a high-level description of a recommended feature or activity that needs to be addressed. Controls aren't specific to a technology or implementation. Security control recommendations are applicable to multiple cloud workloads. Each control is numbered and the control's recommendations identify a list of stakeholders that are typically involved in planning, approval, or implementation of the benchmark.

## MCSB control domains/control families

In the MCSB controls are grouped into "families" or "domains". The following table summarizes the security control domains in MCSB:

| **Control Domain**                  | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Network Security (NS)**          | Covers controls to secure and protect networks, including securing virtual networks, establishing private connections, preventing and mitigating external attacks, and securing DNS.                                                                                                                                                                                                                                                                                                                                  |
| **Identity Management (IM)**       | Covers controls to establish secure identity and access controls using identity and access management systems, including single sign-on, strong authentication, managed identities (and service principals) for applications, conditional access, and account anomaly monitoring.                                                                                                                                                                                                                                    |
| **Privileged Access (PA)**         | Covers controls to protect privileged access to your tenant and resources, including controls to secure the administrative model, administrative accounts, and privileged access workstations against deliberate and inadvertent risks.                                                                                                                                                                                                                                                                                    |
| **Data Protection (DP)**           | Covers data protection at rest, in transit, and through authorized access mechanisms. Includes discovery, classification, protection, and monitoring of sensitive data assets using access control, encryption, key management, and certificate management.                                                                                                                                                                                                                                                              |
| **Asset Management (AM)**          | Covers controls to ensure security visibility and governance over your resources. Includes permissions for security personnel, access to asset inventory, and managing service/resource approvals (inventory, tracking, correction).                                                                                                                                                                                                                                                                                     |
| **Logging and Threat Detection (LT)** | Covers controls for detecting threats in the cloud, enabling and collecting audit logs, generating alerts with native threat detection, centralizing analysis with a SIEM, and managing log retention and time synchronization.                                                                                                                                                                                                                                                                                       |
| **Incident Response (IR)**         | Covers controls across the incident response lifecycle—preparation, detection, containment, and post-incident activities. Includes automation using services like Microsoft Defender for Cloud and Sentinel or other cloud services.                                                                                                                                                                                                                                                                                   |
| **Posture and Vulnerability Management (PV)** | Focuses on controls for assessing and improving cloud security posture, including vulnerability scanning, penetration testing, remediation, and tracking/reporting security configurations.                                                                                                                                                                                                                                                                                                                             |
| **Endpoint Security (ES)**         | Covers controls for endpoint detection and response (EDR), including anti-malware services for endpoints in cloud environments.                                                                                                                                                                                                                                                                                                                                                                                         |
| **Backup and Recovery (BR)**       | Covers controls to ensure data and configuration backups are performed, validated, and protected across different service tiers.                                                                                                                                                                                                                                                                                                                                                                                        |
| **DevOps Security (DS)**           | Covers controls in security engineering and DevOps operations, such as static application security testing, vulnerability management, threat modeling, and software supply chain security. Ensures secure deployment pipelines.                                                                                                                                                                                                                                                                                         |
| **Governance and Strategy (GS)**   | Provides guidance for a coherent security strategy and documented governance, including role/responsibility definition, unified technical strategies, policies, and standards to support long-term assurance.                                                                                                                                                                                                                                                                                                           |

## Service baselines

Security baselines are standardized documents for Azure product offerings, describing the available security capabilities and the optimal security configurations to help you strengthen security through improved tooling, tracking, and security features. We currently have service baselines available for Azure only.

Security baselines for Azure focus on cloud-centric control areas in Azure environments. These controls are consistent with well-known industry standards such as: Center for Internet Security (CIS) or National Institute for Standards in Technology (NIST). Our baselines provide guidance for the control areas listed in the Microsoft cloud security benchmark v1.

Each baseline consists of the following components:

1) How does a service behave?

2) Which security features are available?

3) What configurations are recommended to secure the service?

# Implement Microsoft cloud security benchmark

1) Plan your MCSB implementation by reviewing the documentation for the enterprise controls and service-specific baselines to plan your control framework and how it maps to guidance like Center for Internet Security (CIS) Controls, National Institute of Standards and Technology (NIST), and the Payment Card Industry Data Security Standard (PCI-DSS) framework.

2) Monitor your compliance with MCSB status (and other control sets) using the Microsoft Defender for Cloud – Regulatory Compliance Dashboard for your multicloud environment.

3) Establish guardrails to automate secure configurations and enforce compliance with MCSB (and other requirements in your organization) using features such as Azure Blueprints, Azure Policy, or the equivalent technologies from other cloud platforms.

## Common use cases

Microsoft cloud security benchmark can often be used to address common challenges for customers or service partners who are:

1) New to Azure (and other major cloud platforms, such as AWS) and looking for security best practices to ensure a secure deployment of cloud services and your own application workload.

2) Looking to improve security posture of existing cloud deployments to prioritize top risks and mitigations.

3) Using multicloud environments (such as Azure and AWS) and facing challenges in aligning the security control monitoring and evaluation using a single pane of glass.

4) Evaluating the security features/capabilities of Azure (and other major cloud platforms, such as AWS) before onboarding/approving a service(s) into the cloud service catalog.

5) Having to meet compliance requirements in highly regulated industries, such as government, finance, and healthcare. These customers need to ensure their service configurations of Azure and other clouds to meet the security specification defined in framework such as CIS, NIST, or PCI. MCSB provides an efficient approach with the controls already premapped to these industry benchmarks.

## Terminology

The terms "control" and "baseline" are often used in the Microsoft cloud security benchmark documentation. It's important to understand how MCSB uses these terms.

| **Term**     | **Description**                                                                                                                                                                                                                              | **Example**                                                                                                                                                                               |
|--------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Control**  | A control is a high-level description of a feature or activity that needs to be addressed and isn't specific to a technology or implementation.                                                      | *Data Protection* is one of the security control families. Data Protection contains specific actions that must be addressed to help ensure data is protected.                            |
| **Baseline** | A baseline is the implementation of the control on the individual Azure services. Each organization dictates a benchmark recommendation and corresponding configurations are needed in Azure.<br>**Note:** Service baselines are currently available only for Azure. | The Contoso company looks to enable Azure SQL security features by following the configuration recommended in the Azure SQL security baseline.                                           |
