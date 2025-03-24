# Microsoft Defender for Containers

Microsoft Defender for Containers is a cloud-native solution to improve, monitor, and maintain the security of your containerized assets (Kubernetes clusters, Kubernetes nodes, Kubernetes workloads, container registries, container images and more), and their applications, across multicloud and on-premises environments.

Defender for Containers assists you with four core domains of container security:

1) Security posture management - performs continuous monitoring of cloud APIs, Kubernetes APIs, and Kubernetes workloads to discover cloud resources, provide comprehensive inventory capabilities, detect misconfigurations and provide guidelines to mitigate them, provide contextual risk assessment, and empowers users to perform enhanced risk hunting capabilities through the Defender for Cloud security explorer.

2) Vulnerability assessment - provides agentless vulnerability assessment for Azure, AWS, and GCP with remediation guidelines, zero configuration, daily rescans, coverage for OS and language packages, and exploitability insights.

3) Run-time threat protection - a rich threat detection suite for Kubernetes clusters, nodes, and workloads, powered by Microsoft leading threat intelligence, provides mapping to MITRE ATT&CK framework for easy understanding of risk and relevant context, automated response, and Security Information and Event Management (SIEM)/Extended Detection and Response (XDR) integration.

4) Deployment & monitoring- Monitors your Kubernetes clusters for missing agents and provides frictionless at-scale deployment for agent-based capabilities, support for standard Kubernetes monitoring tools, and management of unmonitored resources.

## Microsoft Defender for Containers plan availability

| **Aspect**                 | **Details** |
|----------------------------|------------|
| **Release State**          | General availability (GA). <br> Certain features are in preview. For a full list, see the [Containers support matrix in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction#containers-support-matrix). |
| **Feature Availability**   | Refer to the [Containers support matrix in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction#containers-support-matrix) for additional information on feature release state and availability. |
| **Pricing**                | Microsoft Defender for Containers is billed as shown on the [pricing page](https://azure.microsoft.com/en-us/pricing/details/defender-for-cloud/). |
| **Required Roles & Permissions** | - To deploy the required components, see the permissions for each of the components. <br> - Security admin can dismiss alerts. <br> - Security reader can view vulnerability assessment findings. <br> See also [Roles for remediation](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction#roles-for-remediation) and [Azure Container Registry roles and permissions](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-roles). |
| **Clouds**                 | View the [Containers support matrix in Defender for Cloud](https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-containers-introduction#containers-support-matrix) to see cloud availability. |

## Security Posture Management

### Agentless capabilities

1) Agentless discovery for Kubernetes - provides zero footprint, API-based discovery of your Kubernetes clusters, their configurations and deployments.

2) Agentless vulnerability assessment - provides vulnerability assessment for all container images, including recommendations for registry and runtime, quick scans of new images, daily refresh of results, exploitability insights, and more. Vulnerability information is added to the security graph for contextual risk assessment and calculation of attack paths, and hunting capabilities.

3) Comprehensive inventory capabilities - enables you to explore resources, pods, services, repositories, images and configurations through security explorer to easily monitor and manage your assets.

4) Enhanced risk-hunting - enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and security insights in the security explorer

5) Control plane hardening - continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues.

You can use the resource filter to review the outstanding recommendations for your container-related resources, whether in asset inventory or the recommendations page:

![image](https://github.com/user-attachments/assets/191428be-b96f-4c12-a3de-7ad8978c1434)

#### NOTE: For details included with this capability, check out the containers section of the recommendations reference table, and look for recommendations with type "Control plane"

### Agent-based capabilities

Kubernetes data plane hardening - To protect the workloads of your Kubernetes containers with best practice recommendations, you can install the Azure Policy for Kubernetes. Learn more about monitoring components for Defender for Cloud.

With the add-on on your Kubernetes cluster, every request to the Kubernetes API server is monitored against the predefined set of best practices before being persisted to the cluster. You can then configure it to enforce the best practices and mandate them for future workloads.

For example, you can mandate that privileged containers shouldn't be created, and any future requests to do so are blocked.

### Vulnerability assessment

Defender for Containers scans the container images in Azure Container Registry (ACR), Amazon AWS Elastic Container Registry (ECR), Google Artifact Registry (GAR), and Google Container Registry (GCR) to provide agentless vulnerability assessment for your container images, including registry and runtime recommendations, remediation guidance, quick scans of new images, real-world exploit insights, exploitability insights, and more.

Vulnerability information powered by Microsoft Defender Vulnerability Management is added to the cloud security graph for contextual risk, calculation of attack paths, and hunting capabilities.

There are two solutions for vulnerability assessment in Azure, one powered by Microsoft Defender Vulnerability Management and one powered by Qualys.

## Run-time protection for Kubernetes nodes and clusters

Defender for Containers provides real-time threat protection for supported containerized environments and generates alerts for suspicious activities. You can use this information to quickly remediate security issues and improve the security of your containers.

Threat protection is provided for Kubernetes at cluster level, node level, and workload level and includes both agent based coverage that requires the Defender agent and agentless coverage that is based on analysis of the Kubernetes audit logs. Security alerts are only triggered for actions and deployments that occur after you enabled Defender for Containers on your subscription.

Examples of security events that Microsoft Defenders for Containers monitors include:

1) Exposed Kubernetes dashboards

2) Creation of high privileged roles

3) Creation of sensitive mounts

You can view security alerts by selecting the Security alerts tile at the top of the Defender for Cloud's overview page, or the link from the sidebar.

![image](https://github.com/user-attachments/assets/51a7d3d7-5bd5-41a2-b365-634ebb49832c)

The security alerts page opens:

![image](https://github.com/user-attachments/assets/4dcb0b01-957e-4863-8000-50ada4519774)

Security alerts for runtime workload in the clusters can be recognized by the Kubernetes K8S.NODE_ prefix of the alert type.

Defender for Containers also includes host-level threat detection with over 60 Kubernetes-aware analytics, AI, and anomaly detections based on your runtime workload.

