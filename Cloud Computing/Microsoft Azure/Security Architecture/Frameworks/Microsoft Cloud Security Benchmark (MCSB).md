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


## Capabilities and controls with MCSB

The Microsoft cloud security benchmark (MCSB) security controls contain many best practices for cybersecurity capabilities and controls, including both technical and non-technical capabilities and controls like processes. The table below lists several relevant security controls:

| **MCSB Control Domain**                | **Security Controls**                                                                                                                                                           |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Data Protection (DP)**              | DP-1: Discover, classify, and label sensitive data  <br>DP-2: Monitor anomalies and threats targeting sensitive data  <br>DP-3: Encrypt sensitive data in transit  <br>DP-4: Enable data at rest encryption by default  <br>DP-5: Use customer-managed key option in data at rest encryption when required  <br>DP-6: Use a secure key management process  <br>DP-7: Use a secure certificate management process  <br>DP-8: Ensure security of key and certificate repository |
| **Asset Management (AM)**            | AM-1: Track asset inventory and their risks  <br>AM-2: Use only approved services  <br>AM-3: Ensure security of asset lifecycle management  <br>AM-4: Limit access to asset management  <br>AM-5: Use only approved applications in virtual machine |
| **Posture and Vulnerability Management (PV)** | PV-1: Define and establish secure configurations  <br>PV-2: Audit and enforce secure configurations  <br>PV-3: Define and establish secure configurations for compute resources  <br>PV-4: Audit and enforce secure configurations for compute resources  <br>PV-5: Perform vulnerability assessments  <br>PV-6: Rapidly and automatically remediate vulnerabilities  <br>PV-7: Conduct regular red team operations |
| **Endpoint Security (ES)**           | ES-1: Use Endpoint Detection and Response (EDR)  <br>ES-2: Use modern anti-malware software  <br>ES-3: Ensure anti-malware software and signatures are updated |
| **Backup and Recovery (BR)**         | BR-1: Ensure regular automated backups  <br>BR-2: Protect backup and recovery data  <br>BR-3: Monitor backups  <br>BR-4: Regularly test backup |
| **DevOps Security (DS)**             | DS-1: Conduct threat modeling  <br>DS-2: Ensure software supply chain security  <br>DS-3: Secure DevOps infrastructure  <br>DS-4: Integrate static application security testing into DevOps pipeline  <br>DS-5: Integrate dynamic application security testing into DevOps pipeline  <br>DS-6: Enforce security of workload throughout DevOps lifecycle  <br>DS-7: Enable logging and monitoring in DevOps |
| **Governance and Strategy (GS)**     | GS-1: Align organization roles, responsibilities and accountabilities  <br>GS-2: Define and implement enterprise segmentation/separation of duties strategy  <br>GS-3: Define and implement data protection strategy  <br>GS-4: Define and implement network security strategy  <br>GS-5: Define and implement security posture management strategy  <br>GS-6: Define and implement identity and privileged access strategy  <br>GS-7: Define and implement logging, threat detection and incident response strategy  <br>GS-8: Define and implement backup and recovery strategy  <br>GS-9: Define and implement endpoint security strategy  <br>GS-10: Define and implement DevOps security strategy |

## Attack protection with MCSB

The Microsoft Cloud Security Benchmark includes many best practices that help protect from insider and external attacks including the security controls listed in the table below focused on security operations:

| **MCSB Control Domain**                | **Security Controls**                                                                                                                                                           |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Incident Response (IR)**            | IR-1: Preparation - update incident response plan and handling process  <br>IR-2: Preparation - setup incident notification  <br>IR-3: Detection and analysis - create incidents based on high-quality alerts  <br>IR-4: Detection and analysis - investigate an incident  <br>IR-5: Detection and analysis - prioritize incidents  <br>IR-6: Containment, eradication, and recovery - automate the incident handling  <br>IR-7: Post-incident activity - conduct lessons learned review and retain evidence |
| **Logging and Threat Detection (LT)** | LT-1: Enable threat detection capabilities  <br>LT-2: Enable threat detection for identity and access management  <br>LT-3: Enable logging for security investigation  <br>LT-4: Enable network logging for security investigation  <br>LT-5: Centralize security log management and analysis  <br>LT-6: Configure log storage retention  <br>LT-7: Use approved time synchronization sources |
