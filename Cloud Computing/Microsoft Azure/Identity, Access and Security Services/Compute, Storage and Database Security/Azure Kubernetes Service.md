# Azure Kubernetes Service (AKS)

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You don't need container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

## Overview of Azure Kubernetes Service

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

![image](https://github.com/user-attachments/assets/e22d5e13-9177-40b1-ad52-62b02d54d32f)

AKS is CNCF-certified and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the Microsoft Azure compliance overview.

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution             | Resource type                         |
|--------------------------------|--------------------------------------|
| Azure Kubernetes Service       | Managed Kubernetes                   |
| Azure Red Hat OpenShift        | Managed Kubernetes                   |
| Azure Arc-enabled Kubernetes   | Unmanaged Kubernetes                 |
| Azure Container Instances      | Managed Docker container instance    |
| Azure Container Apps           | Managed Kubernetes                   |

## When to use AKS

The following list describes some of the common use cases for AKS, but by no means is an exhaustive list:

1) Lift and shift to containers with AKS: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.

2) Microservices with AKS: Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.

3) Secure DevOps for AKS: Efficiently balance speed and security by implementing secure DevOps with Kubernetes.

4) Bursting from AKS with ACI: Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.

5) Machine learning model training with AKS: Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.

6) Data streaming with AKS: Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.

7) Using Windows containers on AKS: Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.

## Features of AKS

| Feature                        | Description |
|--------------------------------|-------------|
| **Identity and security management** | • Enforce regulatory compliance controls using Azure Policy with built-in guardrails and internet security benchmarks. <br> • Integrate with Kubernetes RBAC to limit access to cluster resources. <br> • Use Microsoft Entra ID to set up Kubernetes access based on existing identity and group membership. |
| **Logging and monitoring** | • Integrate with Container Insights, a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications. <br> • Set up Network Observability and use BYO Prometheus and Grafana to collect and visualize network traffic data from your clusters. |
| **Streamlined deployments** | • Use prebuilt cluster configurations for Kubernetes with smart defaults. <br> • Autoscale your applications using the Kubernetes Event Driven Autoscaler (KEDA). <br> • Use Draft for AKS to ready source code and prepare your applications for production. |
| **Clusters and nodes** | • Connect storage to nodes and pods, upgrade cluster components, and use GPUs. <br> • Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers. <br> • Configure automatic scaling using the cluster autoscaler and horizontal pod autoscaler. <br> • Deploy clusters with confidential computing nodes to allow containers to run in a hardware-based trusted execution environment. |
| **Storage volume support** | • Mount static or dynamic storage volumes for persistent data. <br> • Use Azure Disks for single pod access and Azure Files for multiple, concurrent pod access. <br> • Use Azure NetApp Files for high-performance, high-throughput, and low-latency file shares. |
| **Networking** | • Leverage Kubenet networking for simple deployments and Azure Container Networking Interface (CNI) networking for advanced scenarios. <br> • Bring your own Container Network Interface (CNI) to use a third-party CNI plugin. <br> • Easily access applications deployed to your clusters using the application routing add-on with nginx. |
| **Development tooling integration** | • Develop on AKS with Helm. <br> • Install the Kubernetes extension for Visual Studio Code to manage your workloads. <br> • Leverage the features of Istio with the Istio-based service mesh add-on. |

# Configure network isolation for Azure Kubernetes Service (AKS)

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. AKS allows flexibility in how you run multitenant clusters and isolate resources. To maximize your investment in Kubernetes, it's important you understand AKS multi-tenancy and isolation features.

## Design clusters for multi-tenancy

Kubernetes lets you logically isolate teams and workloads in the same cluster. The goal is to provide the least number of privileges scoped to the resources each team needs. A Kubernetes Namespace creates a logical isolation boundary. Other Kubernetes features and considerations for isolation and multi-tenancy include the following areas:

1) Best practices for cluster isolation in Azure Kubernetes Service (AKS)

Design clusters for multi-tenancy

Scheduling

Networking

Authentication and authorization

Containers

2) Logically isolated clusters

3) Physically isolated clusters

## Scheduling

Scheduling uses basic features like resource quotas and pod disruption budgets.

More advanced scheduler features include:

1) Taints and tolerations.

2) Node selectors.

3) Node and pod affinity or anti-affinity.

## Networking

Networking uses network policies to control the flow of traffic in and out of pods.

## Authentication and authorization

Authentication and authorization uses:

1) Role-based access control (RBAC).

2) Microsoft Entra integration.

3) Pod identities.

4) Secrets in Azure Key Vault.

## Containers

Containers include:

1) The Azure Policy add-on for AKS to enforce pod security.

2) Pod security admission.

3) Scanning images and runtime for vulnerabilities.

4) Using App Armor or Seccomp (Secure Computing) to restrict container access to the underlying node.

## Logically isolated clusters

Best practice guidance: Separate teams and projects using logical isolation. Minimize the number of physical AKS clusters you deploy to isolate teams or applications.

With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes Namespaces form the logical isolation boundary for workloads and resources.

![image](https://github.com/user-attachments/assets/8785e76b-9910-4445-b85e-521a6e61c91c)

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with the Kubernetes cluster autoscaler, you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

Kubernetes environments aren't entirely safe for hostile multitenant usage. In a multitenant environment, multiple tenants work on a shared infrastructure. If all tenants can't be trusted, you need extra planning to prevent tenants from impacting the security and service of others.

Other security features, like Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multitenant workloads, you should only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster and not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## Physically isolated clusters

Best practice guidance: Minimize the use of physical isolation for each separate team or application deployment and use logical isolation instead.

Physically separating AKS clusters is a common approach to cluster isolation. In this isolation model, teams or workloads are assigned their own AKS cluster. While physical isolation might look like the easiest way to isolate workloads or teams, it adds management and financial overhead. With physically isolated clusters, you must maintain multiple clusters and individually provide access and assign permissions. You're also billed for each individual node.

![image](https://github.com/user-attachments/assets/aea32e66-101b-4ce8-ba0b-2d5321dcc693)

Physically isolated clusters usually have a low pod density. Since each team or workload has their own AKS cluster, the cluster is often over-provisioned with compute resources. Often, a few pods are scheduled on those nodes. Unclaimed node capacity can't be used for applications or services in development by other teams. These excess resources contribute to the extra costs in physically isolated clusters.

# Secure and monitor Azure Kubernetes Service

Microsoft Defender for Containers is a cloud-native solution to improve, monitor, and maintain the security of your containerized assets (Kubernetes clusters, Kubernetes nodes, Kubernetes workloads, container registries, container images and more), and their applications, across multicloud and on-premises environments.

Defender for Containers assists you with four core domains of container security:

1) Security posture management - performs continuous monitoring of cloud APIs, Kubernetes APIs, and Kubernetes workloads to discover cloud resources, provide comprehensive inventory capabilities, detect misconfigurations and provide guidelines to mitigate them, provide contextual risk assessment, and empowers users to perform enhanced risk hunting capabilities through the Defender for Cloud security explorer.

2) Vulnerability assessment - provides agentless vulnerability assessment for Azure, AWS, and GCP with remediation guidelines, zero configuration, daily rescans, coverage for OS and language packages, and exploitability insights.

3) Run-time threat protection - a rich threat detection suite for Kubernetes clusters, nodes, and workloads, powered by Microsoft leading threat intelligence, provides mapping to MITRE ATT&CK framework for easy understanding of risk and relevant context, automated response, and Security Information and Event Management/Extended detection and response integration.

4) Deployment & monitoring- Monitors your Kubernetes clusters for missing agents and provides frictionless at-scale deployment for agent-based capabilities, support for standard Kubernetes monitoring tools, and management of unmonitored resources.

## Security posture management

### Agentless capabilities

1) Agentless discovery for Kubernetes - provides zero footprint, API-based discovery of your Kubernetes clusters, their configurations and deployments.

2) Agentless vulnerability assessment - provides vulnerability assessment for all container images, including recommendations for registry and runtime, quick scans of new images, daily refresh of results, exploitability insights, and more. Vulnerability information is added to the security graph for contextual risk assessment and calculation of attack paths, and hunting capabilities.

3) Comprehensive inventory capabilities - enables you to explore resources, pods, services, repositories, images and configurations through security explorer to easily monitor and manage your assets.

4) Enhanced risk-hunting - enables security admins to actively hunt for posture issues in their containerized assets through queries (built-in and custom) and security insights in the security explorer

5) Control plane hardening - continuously assesses the configurations of your clusters and compares them with the initiatives applied to your subscriptions. When it finds misconfigurations, Defender for Cloud generates security recommendations that are available on Defender for Cloud's Recommendations page. The recommendations let you investigate and remediate issues.

You can use the resource filter to review the outstanding recommendations for your container-related resources, whether in asset inventory or the recommendations page:

![image](https://github.com/user-attachments/assets/9e18304e-e8d1-4f6f-af59-74ba5473590d)

### Agent-based capabilities

Kubernetes data plane hardening - To protect the workloads of your Kubernetes containers with best practice recommendations, you can install the Azure Policy for Kubernetes.

With the add-on on your Kubernetes cluster, every request to the Kubernetes API server is monitored against the predefined set of best practices before being persisted to the cluster. You can then configure it to enforce the best practices and mandate them for future workloads.

For example, you can mandate that privileged containers shouldn't be created, and any future requests to do so are blocked.

### Vulnerability Assessment

Defender for Containers scans the container images in Azure Container Registry (ACR) and Amazon AWS Elastic Container Registry (ECR) to provide vulnerability reports for your container images, providing details for each vulnerability detected, remediation guidance, real-world exploit insights, and more.

There are two solutions for vulnerability assessment in Azure, one powered by Microsoft Defender Vulnerability Management and one powered by Qualys.

### Run-time protection for Kubernetes nodes and clusters

Defender for Containers provides real-time threat protection for supported containerized environments and generates alerts for suspicious activities. You can use this information to quickly remediate security issues and improve the security of your containers.

Threat protection at the cluster level is provided by the Defender agent and analysis of the Kubernetes audit logs. This means that security alerts are only triggered for actions and deployments that occur after you've enabled Defender for Containers on your subscription.

Examples of security events that Microsoft Defenders for Containers monitors include:

1) Exposed Kubernetes dashboards

2) Creation of high privileged roles

3) Creation of sensitive mounts

You can view security alerts by selecting the Security alerts tile at the top of the Defender for Cloud's overview page, or the link from the sidebar.

![image](https://github.com/user-attachments/assets/36b1618c-5520-47c3-b6a1-19e8cd93f524)

The security alerts page opens:

![image](https://github.com/user-attachments/assets/2dc7b94e-bebf-443b-9eda-3b7301c0b468)

Security alerts for runtime workload in the clusters can be recognized by the K8S.NODE_ prefix of the alert type.

Defender for Containers also includes host-level threat detection with over 60 Kubernetes-aware analytics, AI, and anomaly detections based on your runtime workload.

Defender for Cloud monitors the attack surface of multicloud Kubernetes deployments based on the MITRE ATT&CK matrix for Containers, a framework developed by the Center for Threat-Informed Defense in close partnership with Microsoft.

# Configure authentication for Azure Kubernetes Service

As you deploy and maintain clusters in Azure Kubernetes Service (AKS), you implement ways to manage access to resources and services. Without these controls:

1) Accounts could have access to unnecessary resources and services.

2) Tracking credentials used to make changes can be difficult.

## Use Microsoft Entra ID

Best practice guidance: Deploy AKS clusters with Microsoft Entra integration. Using Microsoft Entra ID centralizes the identity management layer. Any change in user account or group status is automatically updated in access to the AKS cluster. Scope users or groups to the minimum permissions amount using Roles, ClusterRoles, or Bindings.

Your Kubernetes cluster developers and application owners need access to different resources. Kubernetes lacks an identity management solution for you to control the resources with which users can interact. Instead, you can integrate your cluster with an existing identity solution like Microsoft Entra ID, an enterprise-ready identity management solution.

With Microsoft Entra integrated clusters in AKS, you create Roles or ClusterRoles defining access permissions to resources. You then bind the roles to users or groups from Microsoft Entra ID.

Microsoft Entra integration and how you control access to resources can be seen in the following diagram:

![image](https://github.com/user-attachments/assets/d9730e5a-5c81-456b-bcac-4d731bf7dc20)

1) Developer authenticates with Microsoft Entra ID.

2) The Microsoft Entra token issuance endpoint issues the access token.

3) The developer performs an action using the Microsoft Entra token, such as kubectl create pod.

4) Kubernetes validates the token with Microsoft Entra ID and fetches the developer's group memberships.

5) Kubernetes RBAC and cluster policies are applied.

6) The developer's request is successfully based on previous validation of Microsoft Entra group membership and Kubernetes RBAC and policies.

## Use Kubernetes role-based access control (Kubernetes RBAC)

Best practice guidance: Define user or group permissions to cluster resources with Kubernetes RBAC. Create roles and bindings that assign the least amount of permissions required. Integrate with Microsoft Entra ID to automatically update any user status or group membership change and keep access to cluster resources current.

In Kubernetes, you provide granular access control to cluster resources. You define permissions at the cluster level, or to specific namespaces. You determine what resources can be managed and with what permissions. You then apply these roles to users or groups with a binding.

When developer1@contoso.com is authenticated against the AKS cluster, they have full permissions to resources in the finance-app namespace. In this way, you logically separate and control access to resources. Use Kubernetes RBAC with Microsoft Entra ID-integration.

## Use Azure RBAC

Best practice guidance: Use Azure RBAC to define the minimum required user and group permissions to AKS resources in one or more subscriptions.

There are two levels of access needed to fully operate an AKS cluster:

1) Access the AKS resource on your Azure subscription.

2) This access level allows you to:

Control scaling or upgrading your cluster using the AKS APIs

Pull your kubeconfig.

3) Access to the Kubernetes API.

This access level is controlled either by:

Kubernetes RBAC (traditionally) or

By integrating Azure RBAC with AKS for kubernetes authorization.

## Use pod-managed identities

Don't use fixed credentials within pods or container images, as they are at risk of exposure or abuse. Instead, use pod identities to automatically request access using Microsoft Entra ID.

To access other Azure resources, like Azure Cosmos DB, Key Vault, or Blob storage, the pod needs authentication credentials. You could define authentication credentials with the container image or inject them as a Kubernetes secret. Either way, you would need to manually create and assign them. Usually, these credentials are reused across pods and aren't regularly rotated.

With pod-managed identities (preview) for Azure resources, you automatically request access to services through Microsoft Entra ID. Pod-managed identities are currently in preview for AKS.

Microsoft Entra pod-managed identity (preview) supports two modes of operation:

1) Standard mode: In this mode, the following 2 components are deployed to the AKS cluster:
Managed Identity Controller(MIC): A Kubernetes controller that watches for changes to pods, AzureIdentity and AzureIdentityBinding through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes AzureAssignedIdentity as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying virtual machine scale set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the virtual machine scale set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.
Node Managed Identity (NMI): is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the Azure Instance Metadata Service on each node. It redirects requests to itself and validates if the pod has access to the identity it's requesting a token for, and fetch the token from the Microsoft Entra tenant on behalf of the application.

2) Managed mode: In this mode, there's only NMI. The identity needs to be manually assigned and managed by the user. In this mode, when you use the az aks pod-identity add command to add a pod identity to an Azure Kubernetes Service (AKS) cluster, it creates the AzureIdentity and AzureIdentityBinding in the namespace specified by the --namespace parameter, while the AKS resource provider assigns the managed identity specified by the --identity-resource-id parameter to virtual machine scale set of each node pool in the AKS cluster.

#### NOTE: If you instead decide to install the Microsoft Entra pod-managed identity using the AKS cluster add-on, setup uses the managed mode.

The managed mode provides the following advantages over the standard:

1) Identity assignment on the virtual machine scale set of a node pool can take up 40-60 seconds. With cronjobs or applications that require access to the identity and can't tolerate the assignment delay, it's best to use managed mode as the identity is pre-assigned to the virtual machine scale set of the node pool. Either manually or using the az aks pod-identity add command.

2) In standard mode, MIC requires write permissions on the virtual machine scale set used by the AKS cluster and Managed Identity Operator permission on the user-assigned managed identities. When running in managed mode, since there's no MIC, the role assignments aren't required.

Instead of manually defining credentials for pods, pod-managed identities request an access token in real time, using it to access only their assigned resources. In AKS, there are two components that handle the operations to allow pods to use managed identities:

1) The Node Management Identity (NMI) server is a pod that runs as a DaemonSet on each node in the AKS cluster. The NMI server listens for pod requests to Azure services.

2) The Azure Resource Provider queries the Kubernetes API server and checks for an Azure identity mapping that corresponds to a pod.

When pods request a security token from Microsoft Entra ID to access to an Azure resource, network rules redirect the traffic to the NMI server.

1) The NMI server:

Identifies pods requesting access to Azure resources based on their remote address.
Queries the Azure Resource Provider.

2) The Azure Resource Provider checks for Azure identity mappings in the AKS cluster.

3) The NMI server requests an access token from Microsoft Entra ID based on the pod's identity mapping.

4) Microsoft Entra ID provides access to the NMI server, which is returned to the pod.

This access token can be used by the pod to then request access to resources in Azure.

In the following example, a developer creates a pod that uses a managed identity to request access to Azure SQL Database:

![image](https://github.com/user-attachments/assets/8dc5a898-7b87-46de-ab24-ae7bf315f6dd)

1) Cluster operator creates a service account to map identities when pods request access to resources.

2) The NMI server is deployed to relay any pod requests, along with the Azure Resource Provider, for access tokens to Microsoft Entra ID.

3) A developer deploys a pod with a managed identity that requests an access token through the NMI server.

4) The token is returned to the pod and used to access Azure SQL Database
