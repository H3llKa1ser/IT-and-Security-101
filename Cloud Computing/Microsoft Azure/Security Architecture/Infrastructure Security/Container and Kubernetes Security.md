# Container and Kubernetes Security

This unit summarizes the Azure security baseline for Azure Kubernetes Service. For areas where there are many controls, we have only included the first five that were mentioned.

Please refer to Introduction to Microsoft Cybersecurity Reference Architecture and cloud security benchmark for more background on Microsoft Cloud Security Benchmark.

In the table below, we have included controls from the full baseline where:

1) Security controls were supported but not enabled by default

2) There was explicit guidance which contained action to be taken on the part of the customer

# Azure Kubernetes Service (AKS) Security Controls

| Area                     | Control | Guidance Summary |
|--------------------------|---------|------------------|
| **Network Security**     | 1.1     | AKS auto-creates and modifies network security groups and route tables to enable appropriate traffic flow. |
|                          | 1.2     | Use Microsoft Defender for Cloud to monitor and secure virtual networks, subnets, and NICs. |
|                          | 1.3     | Use Azure Application Gateway with WAF to protect AKS-hosted web apps from common attacks. |
|                          | 1.4     | Enable Azure DDoS Standard protection for AKS virtual networks. |
|                          | 1.5     | Use Network Watcher packet capture for investigating anomalies. |
| **Logging & Monitoring** | 2.1     | AKS nodes sync time via ntp.ubuntu.com using NTP/UDP port 123. |
|                          | 2.2     | Enable audit logs from kube-apiserver and kube-controller-manager. |
|                          | 2.3     | Use Activity Logs to monitor AKS resource actions and status. |
|                          | 2.4     | Enable Log Analytics agents via Microsoft Defender for Cloud. |
|                          | 2.5     | Use Azure Monitor and set log retention policies per compliance needs. |
| **Identity & Access Control** | 3.1 | Use Microsoft Entra integration to manage access to Kubernetes resources. |
|                          | 3.2     | AKS does not use default passwords; integrate with Microsoft Entra for secure access. |
|                          | 3.3     | Use dedicated admin accounts with Microsoft Entra ID integration. |
|                          | 3.4     | Enable SSO with Microsoft Entra ID for AKS access. |
|                          | 3.5     | Enforce MFA for Entra ID-based AKS access. |
| **Data Protection**      | 4.1     | Tag AKS-related resources to track sensitive data. |
|                          | 4.2     | Logically isolate teams and workloads within AKS clusters. |
|                          | 4.3     | Use perimeter-based third-party tools to monitor/block sensitive data transfers. |
|                          | 4.4     | Use HTTPS ingress with custom or Let's Encrypt TLS certs. |
|                          | 4.5     | Use third-party tools for sensitive data discovery if required. |
| **Vulnerability Management** | 5.1 | Enable Defender for Cloud to scan ACR and AKS for vulnerabilities. |
|                          | 5.2     | AKS auto-patches Linux nodes; Windows nodes need manual updates. |
|                          | 5.3     | Manually manage third-party app updates on AKS nodes. |
|                          | 5.4     | Export scan results periodically and compare to track remediation. |
|                          | 5.5     | Use Defender for Cloud severity ratings to prioritize fixes. |
| **Inventory & Asset Management** | 6.1 | Use Azure Resource Graph to discover all Azure assets. |
|                          | 6.2     | Apply metadata tags for logical resource organization. |
|                          | 6.3     | Use tags, management groups, and subscriptions to track/delete unauthorized resources. |
|                          | 6.4     | Define and maintain a list of approved Azure/compute resources. |
|                          | 6.5     | Use Azure Policy to restrict unapproved resources. |
| **Secure Configuration** | 7.1     | Use Azure Policy (Microsoft.ContainerService) to audit/enforce secure AKS configurations. |
|                          | 7.2     | AKS hosts use security-optimized and hardened OS images. |
|                          | 7.3     | Use Pod Security Policies to restrict pod deployments. |
|                          | 7.4     | AKS nodes use hardened OS images to minimize attack surface. |
|                          | 7.5     | Use Azure Repos and export AKS configs via ARM templates (JSON). |
| **Malware Defense**      | 8.1     | Use DaemonSets to install anti-malware on Linux AKS nodes. |
|                          | 8.2     | Pre-scan uploads using Defender for Cloud if using Azure Storage. |
|                          | 8.3     | Ensure malware tools/signatures on Linux nodes are up-to-date. |
| **Data Recovery**        | 9.1     | Use Velero to back up persistent volumes and AKS resources. |
|                          | 9.2     | Back up customer-managed keys and cluster configurations. |
|                          | 9.3     | Periodically test and validate data restoration from Velero. |
|                          | 9.4     | Secure Velero backups and customer-managed keys. |
| **Incident Response**    | 10.1    | Develop a detailed incident response plan and assign roles. |
|                          | 10.2    | Use Defender for Cloud alert severity to prioritize incidents. |
|                          | 10.3    | Regularly test incident response processes and update plans. |
|                          | 10.4    | Configure alert contact details for MSRC notifications. |
|                          | 10.5    | Use Defender for Cloud’s Continuous Export for alerts. |
| **Penetration Testing**  | 11.1    | Conduct AKS/infra pen tests per Microsoft’s Rules of Engagement and remediate critical issues. |
