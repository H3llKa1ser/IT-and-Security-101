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

