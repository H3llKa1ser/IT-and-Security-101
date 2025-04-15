# Integrate hybrid and multicloud environments with Azure Arc

Today, companies struggle to control and govern increasingly complex environments that extend across data centers, multiple clouds, and edge. Each environment and cloud possesses its own set of management tools, and new DevOps and ITOps operational models can be hard to implement across resources.

Azure Arc simplifies governance and management by delivering a consistent multicloud and on-premises management platform.

Azure Arc provides a centralized, unified way to:

1) Manage your entire environment together by projecting your existing non-Azure and/or on-premises resources into Azure Resource Manager.

2) Manage virtual machines, Kubernetes clusters, and databases as if they are running in Azure.

3) Use familiar Azure services and management capabilities, regardless of where they live.

4) Continue using traditional ITOps while introducing DevOps practices to support new cloud native patterns in your environment.

5) Configure custom locations as an abstraction layer on top of Azure Arc-enabled Kubernetes clusters and cluster extensions.

![image](https://github.com/user-attachments/assets/c351f787-e3aa-4c49-8f63-8522d722345d)

Currently, Azure Arc allows you to manage the following resource types hosted outside of Azure:

1) Servers: Manage Windows and Linux physical servers and virtual machines hosted outside of Azure.

2) Kubernetes clusters: Attach and configure Kubernetes clusters running anywhere, with multiple supported distributions.

3) Azure data services: Run Azure data services on-premises, at the edge, and in public clouds using Kubernetes and the infrastructure of your choice. SQL Managed Instance and PostgreSQL (preview) services are currently available.

4) SQL Server: Extend Azure services to SQL Server instances hosted outside of Azure.

5) Virtual machines (preview): Provision, resize, delete and manage virtual machines based on VMware vSphere or Azure Stack HCI and enable VM self-service through role-based access.

## Key features and benefits

Some of the key scenarios that Azure Arc supports are:

1) Implement consistent inventory, management, governance, and security for servers across your environment.

2) Configure Azure VM extensions to use Azure management services to monitor, secure, and update your servers.

3) Manage and govern Kubernetes clusters at scale.

4) Use GitOps to deploy configuration across one or more clusters from Git repositories.

5) Zero-touch compliance and configuration for Kubernetes clusters using Azure Policy.

6) Run Azure data services on any Kubernetes environment as if it runs in Azure (specifically Azure SQL Managed Instance and Azure Database for PostgreSQL server, with benefits such as upgrades, updates, security, and monitoring). Use elastic scale and apply updates without any application downtime, even without continuous connection to Azure.

7) Create custom locations on top of your Azure Arc-enabled Kubernetes clusters, using them as target locations for deploying Azure services instances. Deploy your Azure service cluster extensions for Azure Arc-enabled data services, App services on Azure Arc (including web, function, and logic apps) and Event Grid on Kubernetes.

8) Perform virtual machine lifecycle and management operations for VMware vSphere and Azure Stack HCI environments.

9) A unified experience viewing your Azure Arc-enabled resources, whether you are using the Azure portal, the Azure CLI, Azure PowerShell, or Azure REST API.

# Introduction to Azure Arc landing zone accelerator for hybrid and multicloud

Enterprises are currently building and running applications across various ecosystems on-premises, in multiple public clouds, and on the edge. When you're working in these distributed environments, it's critical that you find a way to ensure compliance and manage servers, applications, and data at scale while still maintaining agility.

Azure landing zones provides: A specific architectural approach. Reference architecture. Set of reference implementations that help you prepare your landing zones for mission-critical technology platforms and supported workloads.

![image](https://github.com/user-attachments/assets/2dc0afc7-41ce-44c2-b6d4-7fbb9b1a8fca)

Azure landing zones were designed with hybrid and multicloud in mind. To support hybrid and multicloud, the reference architecture requires two additions:

1) Hybrid and multicloud connectivity: Understand key network design considerations and recommendations for working with Azure Arc.

2) Unified operations: Include Azure Arc-enabled resources to extend your governance and operations support with consistent tooling.

## Why hybrid?

As organizations adopt modern cloud services and the associated benefits, periods of running services parallel alongside the legacy on-premises infrastructure are inevitable. As your organization further evaluates cloud services or as business requirements dictate, your team might choose to run more than one public cloud service. Operating a distributed heterogeneous estate requires simplified, consolidated management and governance to reduce operational impact.

Use landing zone concepts introduced as part of the Cloud Adoption Framework guidance to establish patterns for building hybrid architectures and introducing standards for connectivity, governance, and monitoring. This work helps when your strategic intent is to simplify and combine the infrastructure and services following migration projects. Setting standards for management processes and tools removes the need to retrofit workloads after you move them into Azure.

## Prerequisites

It's beneficial to have familiarity with the Azure landing zones. For more information, see the Azure landing zones overview and Azure landing zones implementation guidance.

![image](https://github.com/user-attachments/assets/518ac30e-e9d3-4baa-9a2f-c5d6722c4385)

Azure provides various management tools to help you monitor and govern infrastructure and applications at scale. When implementing a hybrid landing zone, be sure to extend the Azure tools to control infrastructure and applications outside of Azure. This approach creates a single management plane and a single view of your entire hybrid estate, which makes monitoring and management at scale as straightforward as possible.

