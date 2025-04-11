# Design monitoring to support hybrid and multicloud environments

Hybrid, multicloud, and edge deployment approaches often lead to increases in operating costs. The unexpected increase in cost is the result of duplicated or disparate operations, with one set of operating practices per cloud provider. Unified operations is the intentional approach of maintaining one set of tools and processes to consistently manage each cloud provider through a common set of governance and operations management practices.

## Understand and minimize costs through unified operations

In hybrid and multicloud strategies, the first increase in overhead costs might be duplicated cloud platform utilities: network, identity, governance, security, and operations tooling. In the longer term, business challenges could emerge, such as staffing core functions or teams with the required skills to manage diverse environments.

Hybrid and multicloud strategies lead many decision makers to incorrectly conclude that the cloud is more expensive than on-premises technologies. A recent Forrester Consulting study, commissioned by Microsoft, found that a hybrid and multicloud strategy can provide significant three-year return on investment, and substantial avoided on-premises infrastructure and staff costs for organizations. An Accenture and WSP environment and energy study further concluded that cloud solutions add increased energy efficiencies for large deployments. Organizations using cloud solutions reduce energy use and carbon emissions by more than 30 percent against business applications installed on-premises. For small deployments, cloud solutions reach over 90 percent reductions with a shared cloud service.

Organizations can modernize and optimize overall operations using a simple approach to overcoming risks, overhead cost increases, or challenges related to staffing core functions. The Unified operations approach provides hybrid, multicloud, and edge cloud strategies that reduce short-term duplication and long-term strain on your technology staff. This article describes the provider-neutral approach of using unified operations to extend a single enterprise control plane across distributed assets in hybrid, multicloud, and edge environments.

More articles will follow that outline the Azure approach to unified operations: delivering governance and operations management across heterogeneous hybrid, multicloud, and edge environments. The overall goal in an Azure-specific approach to unified operations is to inventory, organize, and govern IT assets anywhere, on any infrastructure. This centralized enterprise control plane provides a consistent cloud operations management experience across on-premises, multicloud, and edge environments.

## Primary cloud platform

Successful hybrid, multicloud, and edge strategies begin with a primary cloud platform.

Whether located in a public or private cloud, your primary cloud platform hosts your operational processes, along with a set of defined cloud facilities. In Azure, those facilities are Azure regions, whereas on-premises, they could be datacenters. These facilities host the cloud services necessary to manage core operations, and to support other workloads hosted on the platform. Your primary cloud platform also includes a series of controls designed to support operations within that cloud.

## Define unified operations

The concept behind how the unified operations approach works is: implement an extension, or gateway, in order to apply the controls in your primary cloud provider across your hybrid, multicloud, or edge deployments. Manage and govern your operations consistently across heterogeneous on-premises, multicloud, and edge environments.

When you implement unified operations, a single enterprise control plane extends across your organization's distributed assets. The single enterprise control plane provides consistent management, application development, and cloud services to any infrastructure, anywhere, at scale. When you enable consistent management and governance for organizations, a gateway with such cloud controls extends consistent operations management and data services across disparate on-premises, multicloud, and edge environments.

When identifying your primary cloud platform, it's important to ensure that cloud has the necessary toolsets to manage all the clouds in your portfolio. Many cloud platforms were designed and built before operations required hybrid, multicloud, or edge deployment options. Insufficient capabilities in current operation tools can require operations teams to replicate processes-using different cloud controls to manage cloud services across each cloud platform. If your cloud strategy calls for hybrid, multicloud, or edge deployment options and your primary cloud platform doesn't support them, consider a platform that can deploy the requisite functionalities for unified operations.

## Unified operations

A single cloud management and operations experience across your portfolio of distributed, scaled assets supports an integrated hybrid and multicloud strategy. This implementation increases your organization's future innovation, agility, and business growth. Adding a gateway for cloud controls that extend management and data services to on-premises, multicloud, and the edge, enables consistent management and governance for organizations. An integral hybrid and multicloud strategy can increase your organization's future innovation, agility, and business growth, anywhere. Implement an extension (or gateway) in order to apply the controls in your primary cloud provider across your hybrid, multicloud, or edge deployments.

![image](https://github.com/user-attachments/assets/d551bc93-a129-4fd7-8dcd-6f07f80fae0f)

If you use an inconsistent approach to implementing unified operations, it can multiply cost inefficiencies for your organization-with increased operating costs (from duplicated cloud platform utilities, or operations tooling). It can also have negative business impacts (staffing teams without the necessary cloud skilling in place).

If your current primary cloud provider doesn't offer the required capabilities for unified operations, consider optimizing your operations and processes using a modern cloud provider.

## Unified operations decomposed

The following image shows the individual components required for unified operations, and how they interact with each other. The following sections provide details on each unified operations component.

![image](https://github.com/user-attachments/assets/aa0ecfa2-8bef-4f2d-800b-17751aa7f03c)

### Customer processes

The primary objective of unified operations is to create as much process consistency as possible across deployments. No cloud service provider can reach 100% feature parity across all hybrid, multicloud, and edge deployments. But the provider should be able to deliver baseline feature sets common across all deployments, so that your governance and operations management processes remain consistent.

![image](https://github.com/user-attachments/assets/4d4a6611-8cda-4660-a504-0d0940350e9c)

Most commonly, customers require the ability to deliver consistency within their defined governance and operations management processes. To meet long-term requirements, your unified operations solution needs to scale to meet these common processes, specified in the following section.

#### Common governance processes tasks

1) Cost management: View, manage, or optimize costs, and identify and provide mitigation guidance for cloud-related IT spend risk.

2) Security baseline: Audit, apply, or automate requirements from recommended security controls, and identify and provide mitigation guidance for security-related business risks.

3) Resource consistency: Onboard, organize, and configure resources and services, and identify and provide risk mitigation guidance for potential business risks.

4) Identity baseline: Enforce authentication and authorization across user identity and access, and identify and provide risk-mitigation guidance for potential identity-related business risks.

5) Deployment acceleration: Drive consistency using templates, automation, and pipelines (for deployments, configuration alignment, and reusable assets). Establish policies to ensure compliant, consistent, and repeatable resource deployment and configuration.

#### Common operations management processes tasks

1) Inventory and visibility: Account for, and ensure reporting for all assets, and collect and monitor your inventory's run state in enterprise-grade environments.

2) Optimized operations: Track, patch, and optimize supported resources and minimize business interruption risks from configuration drift or vulnerabilities from inconsistent patch management.

3) Protection and recovery: Backup, business continuity, and disaster recovery best practices reduce the duration and impact of unpreventable outages.

4) Platform operations: Specialized operations for common technology platforms such as SQL databases, virtual desktops, and SAP (for medium to high criticality workloads).

5) Workload operations: Specialized operations (for high priority/mission-critical workloads) with greater operations requirements.

Platform and workload operations both run an equivalent iterative process to improve system design, automate remediation, scale changes with a service catalog, and continuously improve system design, automation, and scale.

Your primary cloud platform should be able to provide the required technical capabilities and tooling to automate processes, and reach the goals described in the previous section for governance and operations management. Your unified operations solution should enable you to extend these processes across all hybrid, multicloud, and edge deployments.

### Primary cloud controls

Your primary cloud platform should include important features to facilitate or automate the customer processes typically required in the cloud.

![image](https://github.com/user-attachments/assets/18acc193-a1e9-4139-be22-a623d546fd3b)

#### Basic features

All these basic features are required in order to deliver a cloud adoption plan, at scale:

1) Search, index, group, and tag all deployed assets, extending basic visibility and management.

2) Templatize, automate, and extend tooling for consistent deployments.

3) Create access and security boundaries to protect deployed assets.

#### Enhanced features

You'll likely need most, if not all, of the following enhanced features to operate a hybrid and multicloud environment at scale:

1) Performance and inventory reporting

2) Security and compliance auditing and automation

3) Tracking and reporting on applications and dependencies

#### Automated controls

Automate your environment with tools to modernize your operations and optimize operational costs:

1) Environment and in-guest policy

2) Configuration and updates

3) Protection and recovery

These features are likely already included in the control sets you're currently using to operate your primary cloud provider. There are likely many other features and automated processes available in that set of controls. Those features are the primary control functionalities that should be available across hybrid, multicloud, and edge in your unified operations solution.

It's because they're implemented as primary controls that the features above are the ones that commonly lead to fractured or duplicated operations. As mentioned before, an inconsistent approach to implementing unified operations can:

1) Increase operating costs (for example, duplicated cloud platform utilities, operations tooling)

2) Multiply cost inefficiencies for your organization

3) Incur significant capital expenditures in the early phase of the cloud adoption journey

### Hybrid, multicloud gateway, and enterprise control plane

To extend your primary cloud controls, configure an extension or gateway. This type of extension lets your controls see and interact with resources that are deployed outside the cloud platform and creates one control plane and greater visibility across disparate, heterogeneous environments.

In Microsoft's cloud platforms, Azure Arc is the extension. Azure Arc extends the same controls and processes you use to govern your Azure cloud to other public and private clouds and the edge. It's these cloud controls that enable a unified operations approach to consistent governance and operations management processes across heterogeneous on-premises, multicloud, and edge environments.

Unified operations extends the reach of Azure Resource Manager (ARM), the operating system of Azure. ARM reaches outside Azure to bring scattered resources inside Azure and represent them. By bringing Azure services and management to any kind of infrastructure, the unified operations approach extends Azure's reach, and enables new hybrid and multicloud solutions.

When you use a unified operations approach, you can organize, govern, and secure any environment anywhere, with centralized visibility, operations, and compliance. Build cloud applications, anywhere, at scale, with standardized application services, from deployment to monitoring. Deploy Azure services anywhere, faster, consistently, and at scale with always-up-to-date Azure Arc enabled services.

Building, operating, and managing across traditional, cloud-native, and distributed edge applications with consistent controls and processes extends cloud innovations to scattered assets. You can unlock new hybrid and multicloud scenarios to support:

1) Simplified management

2) Faster application development

3) Consistent Azure services

These scenarios extend to all resource environments, on any infrastructure, across your entire IT estate.

A central Azure control plane that focuses on standardization, interoperability, and compliance provides the following benefits across your hybrid and multicloud infrastructures:

1) Enables consistent visibility and uniform governance and operations management

2) Increases productivity

3) Reduces risks

4) Accelerates cloud adoption and migration practices and technologies for organizations
