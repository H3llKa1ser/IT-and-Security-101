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
