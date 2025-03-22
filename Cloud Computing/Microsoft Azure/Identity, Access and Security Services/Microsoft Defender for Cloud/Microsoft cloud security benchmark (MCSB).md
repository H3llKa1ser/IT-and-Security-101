# Microsoft cloud security benchmark (MCSB)

The Microsoft cloud security benchmark (MCSB) provides prescriptive best practices and recommendations to help improve the security of workloads, data, and services on Azure and your multicloud environment, focusing on cloud-centric control areas with input from a set of holistic Microsoft and industry security guidance that includes:

1) Cloud Adoption Framework: Guidance on security, including strategy, roles and responsibilities, Azure Top 10 Security Best Practices, and reference implementation.

2) Azure Well-Architected Framework: Guidance on securing your workloads on Azure.

3) The Chief Information Security Officer (CISO) Workshop: Program guidance and reference strategies to accelerate security modernization using Zero Trust principles.

4) Other industry and cloud service provider's security best practice standards and framework: Examples include the Amazon Web Services (AWS) Well-Architected Framework, Center for Internet Security (CIS) Controls, National Institute of Standards and Technology (NIST), and Payment Card Industry Data Security Standard (PCI-DSS).

## Microsoft cloud security benchmark features

Comprehensive multicloud security framework: Organizations often have to build an internal security standard to reconcile security controls across multiple cloud platforms to meet security and compliance requirements on each of them. This often requires security teams to repeat the same implementation, monitoring, and assessment across the different cloud environments (often for different compliance standards). This creates unnecessary overhead, cost, and effort. To address this concern, we enhanced the Azure Security Benchmark (ASB) to the Microsoft cloud security benchmark (MCSB) to help you quickly work with different clouds by:

1) Providing a single control framework to easily meet the security controls across clouds

2) Providing consistent user experience for monitoring and enforcing the multicloud security benchmark in Defender for Cloud

3) Staying aligned with Industry Standards (e.g., Center for Internet Security, National Institute of Standards and Technology, Payment Card Industry)

Automated control monitoring for AWS in Microsoft Defender for Cloud: You can use Microsoft Defender for Cloud Regulatory Compliance Dashboard to monitor your AWS environment against Microsoft cloud security benchmark (MCSB), just like how you monitor your Azure environment. We developed approximately 180 AWS checks for the new AWS security guidance in MCSB, allowing you to monitor your AWS environment and resources in Microsoft Defender for Cloud.

Azure guidance and security principles: Azure security guidance, security principles, features, and capabilities.

## Controls

| Control Domains                     | Description |
|--------------------------------------|-------------|
| **Network Security (NS)**            | Covers controls to secure and protect networks, including securing virtual networks, establishing private connections, preventing and mitigating external attacks, and securing Domain Name System (DNS). |
| **Identity Management (IM)**         | Covers controls to establish secure identity and access controls using IAM systems, including single sign-on, strong authentication, managed identities, conditional access, and account anomalies monitoring. |
| **Privileged Access (PA)**           | Covers controls to protect privileged access to tenant and resources, including protecting administrative models, accounts, and privileged access workstations. |
| **Data Protection (DP)**             | Covers data protection at rest, in transit, and via authorized access mechanisms, including discovery, classification, protection, and monitoring of sensitive data. |
| **Asset Management (AM)**            | Covers security visibility and governance over resources, including permissions for security personnel, security access to asset inventory, and managing service/resource approvals. |
| **Logging and Threat Detection (LT)** | Covers detecting threats and collecting/storing audit logs, including using cloud monitoring, SIEM integration, time synchronization, and log retention. |
| **Incident Response (IR)**           | Covers incident response lifecycle (preparation, detection, containment, post-incident activities) using Azure services like Defender for Cloud and Sentinel. |
| **Posture and Vulnerability Management (PV)** | Covers cloud security posture management, including vulnerability scanning, penetration testing, security configuration tracking, and remediation. |
| **Endpoint Security (ES)**           | Covers endpoint detection and response (EDR), including anti-malware services for cloud environments. |
| **Backup and Recovery (BR)**         | Covers ensuring data and configuration backups are performed, validated, and protected across different service tiers. |
| **DevOps Security (DS)**             | Covers security in DevOps processes, including SAST, vulnerability management, threat modeling, and software supply chain security. |
| **Governance and Strategy (GS)**     | Covers establishing a coherent security strategy and governance approach, including roles, responsibilities, unified technical strategy, and supporting policies. |
