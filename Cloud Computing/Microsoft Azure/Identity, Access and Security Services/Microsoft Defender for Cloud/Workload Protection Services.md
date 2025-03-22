# Enable workload protection services in Microsoft Defender for Cloud

Defender for Cloud offers security alerts that are powered by Microsoft Threat Intelligence. It also includes a range of advanced, intelligent protections for your workloads. The workload protections are provided through Microsoft Defender plans specific to the types of resources in your subscriptions. For example, you can enable Microsoft Defender for Storage to get alerted about suspicious activities related to your storage resources.

## The Cloud workload dashboard includes the following sections:

1) Microsoft Defender for Cloud coverage - Here you can see the resources types in your subscription that are eligible for protection by Defender for Cloud. Wherever relevant, you can upgrade here as well. If you want to upgrade all possible eligible resources, select Upgrade all.

2) Security alerts - When Defender for Cloud detects a threat in any area of your environment, it generates an alert. These alerts describe details of the affected resources, suggested remediation steps, and in some cases an option to trigger a logic app in response. Selecting anywhere in this graph opens the Security alerts page.

3) Advanced protection - Defender for Cloud includes many advanced threat protection capabilities for virtual machines, Structured Query Language (SQL) databases, containers, web applications, your network, and more. In this advanced protection section, you can see the status of the resources in your selected subscriptions for each of these protections. Select any of them to go directly to the configuration area for that protection type.

4) Insights - This rolling pane of news, suggested reading, and high priority alerts gives Defender for Cloud's insights into pressing security matters that are relevant to you and your subscription. Whether it's a list of high severity Common Vulnerabilities and Exposures (CVEs) discovered on your VMs by a vulnerability analysis tool, or a new blog post by a member of the Defender for Cloud team, you'll find it here in the Insights panel.

## Protect cloud workloads

Proactive security principles require that you implement security practices that protect your workloads from threats. Cloud workload protections (CWP) surface workload-specific recommendations that lead you to the right security controls to protect your workloads.

When your environment is threatened, security alerts right away indicate the nature and severity of the threat so you can plan your response. After you identify a threat in your environment, you need to quickly respond to limit the risk to your resources.

| Capability                          | What Problem Does It Solve? | Get Started | Defender Plan |
|--------------------------------------|-----------------------------|-------------|---------------|
| **Protect cloud servers** | Provides server protections through Microsoft Defender for Endpoint or extended protection with just-in-time network access, file integrity monitoring, vulnerability assessment, and more. | Secure your multicloud and on-premises servers | **Defender for Servers** |
| **Identify threats to your storage resources** | Detects unusual and potentially harmful attempts to access or exploit storage accounts using advanced threat detection capabilities and Microsoft Threat Intelligence data to provide contextual security alerts. | Protect your cloud storage resources | **Defender for Storage** |
| **Protect cloud databases** | Protects databases with attack detection and threat response for popular database types in Azure, addressing database engines and data security risks. | Deploy specialized protections for cloud and on-premises databases | - **Defender for Azure SQL Databases**<br>- **Defender for SQL servers on machines**<br>- **Defender for Open-source relational databases**<br>- **Defender for Azure Cosmos DB** |
| **Protect containers** | Secures containers by improving, monitoring, and maintaining security of clusters, containers, and applications with environment hardening, vulnerability assessments, and run-time protection. | Find security risks in your containers | **Defender for Containers** |
| **Infrastructure service insights** | Diagnoses weaknesses in application infrastructure that can leave environments susceptible to attack. | - Identify attacks targeting applications running over App Service<br>- Detect attempts to exploit Key Vault accounts<br>- Get alerted on suspicious Resource Manager operations<br>- Expose anomalous DNS activities | - **Defender for App Service**<br>- **Defender for Key Vault**<br>- **Defender for Resource Manager**<br>- **Defender for DNS** |
| **Security alerts** | Provides real-time alerts on security threats, categorized by severity to indicate proper responses. | Manage security alerts | **Any workload protection Defender plan** |
| **Security incidents** | Correlates alerts to identify attack patterns and integrates with SIEM, SOAR, and ITSM solutions to respond to threats and limit risks. | Export alerts to SIEM, SOAR, or ITSM systems | **Any workload protection Defender plan** |
