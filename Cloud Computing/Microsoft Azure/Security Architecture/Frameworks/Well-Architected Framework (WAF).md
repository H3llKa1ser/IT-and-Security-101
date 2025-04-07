# Azure Well-Architected Framework (WAF)

The Azure Well-Architected Framework is a set of guiding tenets that can be used to improve the quality of a workload. The framework consists of five pillars of architectural excellence:

1) Reliability

2) Security

3) Cost Optimization

4) Operational Excellence

5) Performance Efficiency

Incorporating these pillars helps produce a high quality, stable, and efficient cloud architecture:

| **Pillar**              | **Description**                                                                 |
|-------------------------|---------------------------------------------------------------------------------|
| **Reliability**         | The ability of a system to recover from failures and continue to function.     |
| **Security**            | Protecting applications and data from threats.                                 |
| **Cost Optimization**   | Managing costs to maximize the value delivered.                                |
| **Operational Excellence** | Operations processes that keep a system running in production.               |
| **Performance Efficiency** | The ability of a system to adapt to changes in load.                         |

## Overview

The following diagram gives a high-level overview of the Azure Well-Architected Framework:

![image](https://github.com/user-attachments/assets/f6fd958d-6a75-49f9-b3be-5f8283dd4f9a)

In the center, is the Well-Architected Framework, which includes the five pillars of architectural excellence. Surrounding the Well-Architected Framework are six supporting elements:

1) Azure Well-Architected Review

2) Azure Advisor

3) Documentation

4) Partners, Support, and Services Offers

5) Reference Architectures

6) Design Principles

# The Well-Architected Framework security pillar

Information security has always been a complex subject, and it evolves quickly with the creative ideas and implementations of attackers and security researchers. The origin of security vulnerabilities started with identifying and exploiting common programming errors and unexpected edge cases. However over time, the attack surface that an attacker may explore and exploit has expanded well beyond these common errors and edge cases. Attackers now freely exploit vulnerabilities in system configurations, operational practices, and the social habits of the systems' users. As system complexity, connectedness, and the variety of users increase, attackers have more opportunities to identify unprotected edge cases. Attackers can hack systems into doing things they weren't designed to do.

Security is one of the most important aspects of any architecture. It provides the following assurances against deliberate attacks and abuse of your valuable data and systems:

1) Confidentiality

2) Integrity

3) Availability

Losing these assurances can negatively affect your business operations and revenue, and your organization's reputation. For the security pillar, we'll discuss key architectural considerations and principles for security and how they apply to Azure.

The security of complex systems depends on understanding the business context, social context, and technical context. As you design your system, cover these areas:


![image](https://github.com/user-attachments/assets/5a90f64a-833e-47d0-8bd7-6dec2adcaf89)

Understanding an IT solution as it interacts with its surrounding environment holds the key to preventing unauthorized activity and to identifying anomalous behavior that may represent a security risk.

Another key factor in success: Adopt a mindset of assuming failure of security controls. Assuming failure allows you to design compensating controls that limit risk and damage if a primary control fails.

Assuming failures can be referred to as assume breach or assume compromise. Assume breach is closely related to the Zero Trust approach of continuously validating security assurances. The Zero Trust approach is described in the Security Design Principles section in more detail.

Cloud architectures can help simplify the complex task of securing an enterprise estate through specialization and shared responsibilities:

Specialization: Specialist teams at cloud providers can develop advanced capabilities to operate and secure systems on behalf of organizations. This approach is preferable to numerous organizations individually developing deep expertise on managing and securing common elements, such as:

1) Datacenter physical security

2) Firmware patching

3) Hypervisor configuration

The economies of scale allow cloud provider specialist teams to invest in optimization of management and security that far exceeds the ability of most organizations.

Cloud providers must be compliant with the same IT regulatory requirements as the aggregate of all their customers. Providers must develop expertise to defend against the aggregate set of adversaries who attack their customers. As a consequence, the default security posture of applications deployed to the cloud is frequently much better than that of applications hosted on-premises.

Shared Responsibility Model: As computing environments move from customer-controlled datacenters to the cloud, the responsibility of security also shifts. Security of the operational environment is now a concern shared by both cloud providers and customers. Organizations can reduce focus on activities that aren't core business competencies by shifting these responsibilities to a cloud service like Azure. Depending on the specific technology choices, some security protections will be built into the particular service, while addressing others will remain the customer's responsibility. To ensure that proper security controls are provided, organizations must carefully evaluate the services and technology choices.


![image](https://github.com/user-attachments/assets/bc811efb-e078-488d-afc7-57e8a5a23f90)

Shared Responsibility and Key Strategies:

After reading this document, you'll be equipped with key insights about how to improve the security posture of your architecture.

As part of your architecture design, you should consider all relevant areas that affect the success of your application. While this article is concerned primarily with security principles, you should also prioritize other requirements of a well-designed system, such as:

1) Availability

2) Scalability

3) Costs

4) Operational characteristics (trading off one over the other as necessary)

Consistently sacrificing security for gains in other areas isn't advisable because security risks tend to increase dynamically over time.

Increasing security risks result in three key strategies:

1) Establish a modern perimeter: For the elements that your organization controls to ensure you have a consistent set of controls (a perimeter) between those assets and the threats to them. Perimeters should be designed based on intercepting authentication requests for the resources (identity controls) versus intercepting network traffic on enterprise networks. This traditional approach isn't feasible for enterprise assets outside the network.

2) Modernize infrastructure security: For operating systems and middleware elements that legacy applications require, take advantage of cloud technology to reduce security risk to the organization. For example, knowing whether all servers in a physical datacenter are updated with security patches has always been challenging because of discoverability. Software-defined datacenters allow easy and rapid discovery of all resources. This rapid discovery enables technology like Microsoft Defender for Cloud to measure quickly and accurately the patch state of all servers and remediate them.

3) "Trust but verify" each cloud provider: For the elements, which are under the control of the cloud provider. You should ensure the security practices and regulatory compliance of each cloud provider (large and small) meet your requirements.

We cover the following areas in the security pillar of the Microsoft Azure Well-Architected Framework:

| **Security Topic**                   | **Description**                                                                                                                                                                                                                                                                                                                                                                                                                 |
|-------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Security design principles**      | These principles describe a securely architected system hosted on cloud or on-premises datacenters, or a combination of both.                                                                                                                                                                                                                                                                                                 |
| **Governance, risk, and compliance**| How is the organization's security going to be monitored, audited, and reported? What types of risks does the organization face while trying to protect identifiable information, Intellectual Property (IP), financial information? Are there specific industry, government, or regulatory requirements that dictate or provide recommendations on criteria that your organization's security controls must meet? |
| **Regulatory compliance**           | Governments and other organizations frequently publish standards to help define good security practices (due diligence) so that organizations can avoid being negligent in security.                                                                                                                                                                                                                                            |
| **Administration**                  | Administration is the practice of monitoring, maintaining, and operating Information Technology (IT) systems to meet service levels that the business requires. Administration introduces some of the highest impact security risks because performing these tasks requires privileged access to a broad set of these systems and applications.                                                                            |
| **Applications and services**       | Applications and the data associated with them ultimately act as the primary store of business value on a cloud platform.                                                                                                                                                                                                                                                                                                       |
| **Identity and access management**  | Identity provides the basis of a large percentage of security assurances.                                                                                                                                                                                                                                                                                                                                                       |
| **Information protection and storage** | Protecting data at rest is required to maintain confidentiality, integrity, and availability assurances across all workloads.                                                                                                                                                                                                                                                                                                  |
| **Network security and containment**| Network security has been the traditional linchpin of enterprise security efforts. However, cloud computing has increased the requirement for network perimeters to be more porous and many attackers have mastered the art of attacks on identity system elements (which nearly always bypass network controls).                                                                       |
| **Security Operations**             | Security operations maintain and restore the security assurances of the system as live adversaries attack it. The tasks of security operations are described well by the NIST Cybersecurity Framework functions of Detect, Respond, and Recover.                                                                                                                                        |
