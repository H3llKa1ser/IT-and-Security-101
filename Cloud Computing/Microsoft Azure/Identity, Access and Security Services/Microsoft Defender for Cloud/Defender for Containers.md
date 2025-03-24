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

## Architecture

Defender for Containers is designed differently for each Kubernetes environment whether they're running in:

Azure Kubernetes Service (AKS) - Microsoft's managed service for developing, deploying, and managing containerized applications.

Amazon Elastic Kubernetes Service (EKS) in a connected Amazon Web Services (AWS) account - Amazon's managed service for running Kubernetes on AWS without needing to install, operate, and maintain your own Kubernetes control plane or nodes.

Google Kubernetes Engine (GKE) in a connected Google Cloud Platform (GCP) project - Google’s managed environment for deploying, managing, and scaling applications using GCP infrastructure.

An unmanaged Kubernetes distribution (using Azure Arc-enabled Kubernetes) - Cloud Native Computing Foundation (CNCF) certified Kubernetes clusters hosted on-premises or on IaaS.

To protect your Kubernetes containers, Defender for Containers receives and analyzes:

1) Audit logs and security events from the API server

2) Cluster configuration information from the control plane

3) Workload configuration from Azure Policy

4) Security signals and events from the node level

# Architecture for each Kubernetes environment

## Architecture diagram of Defender for Cloud and AKS clusters

When Defender for Cloud protects a cluster hosted in Azure Kubernetes Service, the collection of audit log data is agentless and collected automatically through Azure infrastructure with no additional cost or configuration considerations. These are the required components in order to receive the full protection offered by Microsoft Defender for Containers:

1) Defender agent: The DaemonSet that is deployed on each node, collects signals from hosts using the *Extended Berkeley Packet Filter (eBPF) technology*, and provides runtime protection. The agent is registered with a Log Analytics workspace, and used as a data pipeline. However, the audit log data isn't stored in the Log Analytics workspace. The Defender agent is deployed as an AKS Security profile.

*eBPF Background and Information*: The Extended Berkeley Packet Filter (eBPF) is a powerful and versatile framework within the Linux kernel for programmatically analyzing and filtering network packets, as well as performing various other system-level tasks. Originally based on the Berkeley Packet Filter (BPF) introduced in the 1990s, eBPF expands upon its capabilities by allowing user-defined programs to run within the kernel, enabling dynamic and efficient packet processing without requiring modifications to the kernel itself.
eBPF programs are written in a restricted subset of C and are loaded into the kernel, where they execute within a secure and sandboxed environment. This allows for a wide range of network-related tasks to be performed directly within the kernel, such as packet filtering, traffic monitoring, security enforcement, and even custom protocol parsing.
One of the key advantages of eBPF is its versatility and performance. By executing within the kernel, eBPF programs can access and manipulate network packets directly, significantly reducing overhead compared to traditional user-space packet processing methods. Additionally, eBPF programs can be dynamically loaded and attached to various hooks within the kernel, allowing for real-time responsiveness and adaptability to changing network conditions.
eBPF has become increasingly popular in modern networking and security applications due to its flexibility and efficiency. It is widely used in tools and frameworks for network monitoring, intrusion detection, traffic analysis, and performance tuning. Moreover, its capabilities extend beyond networking to other areas of system observability and control, making it a fundamental building block for a wide range of Linux-based applications and services.

2) Azure Policy for Kubernetes: A pod that extends the open-source Gatekeeper v3 and registers as a web hook to Kubernetes admission control making it possible to apply at-scale enforcements, and safeguards on your clusters in a centralized, consistent manner. The Azure Policy for Kubernetes pod is deployed as an AKS add-on. It's only installed on one node in the cluster.

![image](https://github.com/user-attachments/assets/bd22796a-cedf-40fb-b8b1-567cbe4d7a37)

### How does agentless discovery for Kubernetes in Azure work?

The discovery process is based on snapshots taken at intervals:

![image](https://github.com/user-attachments/assets/686cab16-5707-4a9f-978f-a4d7b2584856)

When you enable the agentless discovery for Kubernetes extension, the following process occurs:

Create:

If the extension is enabled from Defender CSPM, Defender for Cloud creates an identity in customer environments called CloudPosture/securityOperator/DefenderCSPMSecurityOperator.
If the extension is enabled from Defender for Containers, Defender for Cloud creates an identity in customer environments called CloudPosture/securityOperator/DefenderForContainersSecurityOperator.
Assign: Defender for Cloud assigns a built-in role called Kubernetes Agentless Operator to that identity on subscription scope. The role contains the following permissions:
AKS read (Microsoft.ContainerService/managedClusters/read)
AKS Trusted Access with the following permissions:
Microsoft.ContainerService/managedClusters/trustedAccessRoleBindings/write
Microsoft.ContainerService/managedClusters/trustedAccessRoleBindings/read
Microsoft.ContainerService/managedClusters/trustedAccessRoleBindings/delete

Discover: Using the system assigned identity, Defender for Cloud performs a discovery of the AKS clusters in your environment using API calls to the API server of AKS.

Bind: Upon discovery of an AKS cluster, Defender for Cloud performs an AKS bind operation by creating a ClusterRoleBinding between the created identity and the Kubernetes ClusterRole aks:trustedaccessrole:defender-containers:microsoft-defender-operator. The ClusterRole is visible via API and gives Defender for Cloud data plane read permission inside the cluster.

### Get secure access for Azure resources in Azure Kubernetes Service by using Trusted Access (preview)

Many Azure services that integrate with Azure Kubernetes Service (AKS) need access to the Kubernetes API server. To avoid granting these services admin access or making your AKS clusters public for network access, you can use the AKS Trusted Access feature.

This feature gives services secure access to AKS and Kubernetes by using the Azure back end without requiring a private endpoint. Instead of relying on identities that have Microsoft Entra permissions, this feature can use your system-assigned managed identity to authenticate with the managed services and applications that you want to use with your AKS clusters.

#### NOTE: AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis.

#### NOTE: The Trusted Access API is generally available. We provide general availability (GA) support for the Azure CLI, but it's still in preview and requires using the aks-preview extension.

#### Trusted Access feature overview

Trusted Access addresses the following scenarios:

If an authorized IP range is set or in a private cluster, Azure services might not be able to access the Kubernetes API server unless you implement a private endpoint access model.

Giving an Azure service admin access to the Kubernetes API doesn't follow the least privilege access best practice and can lead to privilege escalations or risk of credentials leakage. For example, you might have to implement high-privileged service-to-service permissions, and they aren't ideal in an audit review.

#### Prerequisites

An Azure account with an active subscription. Create an account for free.

Resource types that support system-assigned managed identity.

If you're using the Azure CLI, the aks-preview extension version 0.5.74 or later is required.
To learn what roles to use in different scenarios, see these articles:

Azure Machine Learning access to AKS clusters with special configurations
What is Azure Kubernetes Service backup?
Turn on an agentless container posture

## Architecture diagram of Defender for Cloud and Arc-enabled Kubernetes clusters

These components are required in order to receive the full protection offered by Microsoft Defender for Containers:

1) Azure Arc-enabled Kubernetes - Azure Arc-enabled Kubernetes - An agent based solution, installed on one node in the cluster, that connects your clusters to Defender for Cloud. Defender for Cloud is then able to deploy the following two agents as Arc extensions:

2) Defender agent: The DaemonSet that is deployed on each node, collects host signals using eBPF technology and Kubernetes audit logs, to provide runtime protection. The agent is registered with a Log Analytics workspace, and used as a data pipeline. However, the audit log data isn't stored in the Log Analytics workspace. The Defender agent is deployed as an Arc-enabled Kubernetes extension.

3) Azure Policy for Kubernetes: A pod that extends the open-source Gatekeeper v3 and registers as a web hook to Kubernetes admission control making it possible to apply at-scale enforcements, and safeguards on your clusters in a centralized, consistent manner. The Azure Policy for Kubernetes pod is deployed as an Arc-enabled Kubernetes extension. It's only installed on one node in the cluster. For more information, see Protect your Kubernetes workloads and Understand Azure Policy for Kubernetes clusters.

![image](https://github.com/user-attachments/assets/c8d29eae-15e9-474d-8b38-b4f324c2bb28)

## Architecture diagram of Defender for Cloud and EKS clusters

When Defender for Cloud protects a cluster hosted in Elastic Kubernetes Service, the collection of audit log data is agentless. These are the required components in order to receive the full protection offered by Microsoft Defender for Containers:

1) Kubernetes audit logs – AWS account’s CloudWatch enables, and collects audit log data through an agentless collector, and sends the collected information to the Microsoft Defender for Cloud backend for further analysis.

2) Azure Arc-enabled Kubernetes - Azure Arc-enabled Kubernetes - An agent based solution, installed on one node in the cluster, that connects your clusters to Defender for Cloud. Defender for Cloud is then able to deploy the following two agents as Arc extensions:

3) Defender agent: The DaemonSet that is deployed on each node, collects signals from hosts using eBPF technology, and provides runtime protection. The agent is registered with a Log Analytics workspace, and used as a data pipeline. However, the audit log data isn't stored in the Log Analytics workspace. The Defender agent is deployed as an Arc-enabled Kubernetes extension.

4) Azure Policy for Kubernetes: A pod that extends the open-source Gatekeeper v3 and registers as a web hook to Kubernetes admission control making it possible to apply at-scale enforcements, and safeguards on your clusters in a centralized, consistent manner. The Azure Policy for Kubernetes pod is deployed as an Arc-enabled Kubernetes extension. It's only installed on one node in the cluster.

![image](https://github.com/user-attachments/assets/21ec0d27-6d17-4351-9dca-0f88f56ab85e)

How does agentless discovery for Kubernetes in AWS work?

The discovery process is based on snapshots taken at intervals:

When you enable the agentless discovery for Kubernetes extension, the following process occurs:

1) Create:

The Defender for Cloud role MDCContainersAgentlessDiscoveryK8sRole must be added to the aws-auth ConfigMap of the EKS clusters. The name can be customized.

2) Assign: Defender for Cloud assigns the MDCContainersAgentlessDiscoveryK8sRole role the following permissions:

eks:UpdateClusterConfig
eks:DescribeCluster

3) Discover: Using the system assigned identity, Defender for Cloud performs a discovery of the EKS clusters in your environment using API calls to the API server of EKS.

## Architecture diagram of Defender for Cloud and GKE clusters

When Defender for Cloud protects a cluster hosted in Google Kubernetes Engine, the collection of audit log data is agentless. These are the required components in order to receive the full protection offered by Microsoft Defender for Containers:

1) Kubernetes audit logs – GCP Cloud Logging enables, and collects audit log data through an agentless collector, and sends the collected information to the Microsoft Defender for Cloud backend for further analysis.

2) Azure Arc-enabled Kubernetes - Azure Arc-enabled Kubernetes - An agent based solution, installed on one node in the cluster, that connects your clusters to Defender for Cloud. Defender for Cloud is then able to deploy the following two agents as Arc extensions:

3) Defender agent: The DaemonSet that is deployed on each node, collects signals from hosts using eBPF technology, and provides runtime protection. The agent is registered with a Log Analytics workspace, and used as a data pipeline. However, the audit log data isn't stored in the Log Analytics workspace. The Defender agent is deployed as an Arc-enabled Kubernetes extension.

4) Azure Policy for Kubernetes: A pod that extends the open-source Gatekeeper v3 and registers as a web hook to Kubernetes admission control making it possible to apply at-scale enforcements, and safeguards on your clusters in a centralized, consistent manner. The Azure Policy for Kubernetes pod is deployed as an Arc-enabled Kubernetes extension. It only needs to be installed on one node in the cluster.

![image](https://github.com/user-attachments/assets/d96eaabb-8028-4e8f-8da2-fd4bac06a704)

How does agentless discovery for Kubernetes in GCP work?
The discovery process is based on snapshots taken at intervals:

When you enable the agentless discovery for Kubernetes extension, the following process occurs:

Create:

The service account mdc-containers-k8s-operator is created. The name can be customized.

Assign: Defender for Cloud attaches the following roles to the service account mdc-containers-k8s-operator:

The custom role MDCGkeClusterWriteRole, which has the container.clusters.update permission
The built-in role container.viewer

Discover: Using the system assigned identity, Defender for Cloud performs a discovery of the GKE clusters in your environment using API calls to the API server of GKE.

