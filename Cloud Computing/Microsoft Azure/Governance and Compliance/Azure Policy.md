# Azure Policy

How do you ensure that your resources stay compliant? Can you be alerted if a resource's configuration has changed?

Azure Policy is a service in Azure that enables you to create, assign, and manage policies that control or audit your resources. These policies enforce different rules across your resource configurations so that those configurations stay compliant with corporate standards.

## How does Azure Policy define policies?

Azure Policy enables you to define both individual policies and groups of related policies, known as initiatives. Azure Policy evaluates your resources and highlights resources that aren't compliant with the policies you've created. Azure Policy can also prevent noncompliant resources from being created.

Azure Policies can be set at each level, enabling you to set policies on a specific resource, resource group, subscription, and so on. Additionally, Azure Policies are inherited, so if you set a policy at a high level, it will automatically be applied to all of the groupings that fall within the parent. For example, if you set an Azure Policy on a resource group, all resources created within that resource group will automatically receive the same policy.

Azure Policy comes with built-in policy and initiative definitions for Storage, Networking, Compute, Security Center, and Monitoring. For example, if you define a policy that allows only a certain size for the virtual machines (VMs) to be used in your environment, that policy is invoked when you create a new VM and whenever you resize existing VMs. Azure Policy also evaluates and monitors all current VMs in your environment, including VMs that were created before the policy was created.

In some cases, Azure Policy can automatically remediate noncompliant resources and configurations to ensure the integrity of the state of the resources. For example, if all resources in a certain resource group should be tagged with AppName tag and a value of "SpecialOrders," Azure Policy will automatically apply that tag if it is missing. However, you still retain full control of your environment. If you have a specific resource that you don’t want Azure Policy to automatically fix, you can flag that resource as an exception – and the policy won’t automatically fix that resource.

Azure Policy also integrates with Azure DevOps by applying any continuous integration and delivery pipeline policies that pertain to the pre-deployment and post-deployment phases of your applications.

## What are Azure Policy initiatives?

An Azure Policy initiative is a way of grouping related policies together. The initiative definition contains all of the policy definitions to help track your compliance state for a larger goal.

For example, Azure Policy includes an initiative named Enable Monitoring in Azure Security Center. Its goal is to monitor all available security recommendations for all Azure resource types in Azure Security Center.

Under this initiative, the following policy definitions are included:

1) Monitor unencrypted SQL Database in Security Center This policy monitors for unencrypted SQL databases and servers.

2) Monitor OS vulnerabilities in Security Center This policy monitors servers that don't satisfy the configured OS vulnerability baseline.

3) Monitor missing Endpoint Protection in Security Center This policy monitors for servers that don't have an installed endpoint protection agent.

In fact, the Enable Monitoring in Azure Security Center initiative contains over 100 separate policy definitions.

# Overview

When it comes to securing your Azure environment, you’ll encounter two essential tools: Azure Security Policies and Azure Security Initiatives. Both play critical roles in maintaining compliance, but they serve different purposes. Let’s break down their features and use cases.

## Azure Security Policies

Definition: Azure Policy is like a diligent guardian that ensures your resources adhere to specific rules. It allows you to define and enforce policies across your Azure environment.

Components:

1) Policy Definition: Specifies the conditions you want to control (e.g., resource types allowed, mandatory tags).

2) Policy Assignment: Determines where the policy takes effect (individual resources, resource groups, management groups).

3) Policy Parameters: Customizes policy behavior (e.g., Virtual Machine Stock Keeping Units, location).

Use Cases:

1) Enforcing specific rules consistently.

2) Ensuring uniform tagging.

3) Controlling resource types.

## Azure Security Initiatives

Definition: Think of Azure Initiatives as policy bundles. They group related Azure policy definitions together for a specific purpose.

Components:

1) Definitions (Policies): A collection of policies bundled into a single item.

2) Assignment: Initiatives are applied to a scope (e.g., subscription, resource group).

3) Parameters: Customize initiative behavior.

Use Cases:

1) Achieving broader compliance goals (e.g., Payment Card Industry Data Security Standard, Health Insurance Portability and Accountability Act).

2) Managing related policies cohesively.

## When to use which

Azure Policy:

1) Use it for individual policies when specific rules need enforcement.

2) Sometimes a single policy suffices.

Azure Initiatives:

1) Recommended even for a single policy because it simplifies management.

2) Initiatives allow you to manage multiple policies as a cohesive unit.

 - Example: Instead of handling 20 separate policies for PCI-DSS compliance, use an initiative that evaluates them all simultaneously.

Azure Security Policies focus on granular control, while Azure Security Initiatives provide a consolidated approach. Choose wisely based on your organization’s needs and compliance complexity. Both are essential tools in your Azure security toolbox.

