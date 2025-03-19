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
