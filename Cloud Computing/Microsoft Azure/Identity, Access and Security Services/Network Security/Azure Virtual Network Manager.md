# Azure Virtual Network Manager

Azure Virtual Network Manager is a management service that enables you to group, configure, deploy, and manage virtual networks globally across subscriptions. With Virtual Network Manager, you can define network groups to identify and logically segment your virtual networks. Then you can determine the connectivity and security configurations you want and apply them across all the selected virtual networks in network groups at once.

## How does Azure Virtual Network Manager work?

![image](https://github.com/user-attachments/assets/1ea466c0-4800-4a80-b251-964564733d3d)

During the creation process, you define the scope for what your Azure Virtual Network Manager manages. Your Network Manager only has the delegated access to apply configurations within this scope boundary. Defining a scope can be done directly on a list of subscriptions. However it's recommended to use management groups to define your scope. Management groups provide hierarchical organization to your subscriptions. After defining the scope, you deploy configuration types including Connectivity and the SecurityAdmin rules for your Virtual Network Manager.

After you deploy the Virtual Network Manager instance, you create a network group, which serves as a logical container of networking resources to apply configurations at scale. You can manually select individual virtual networks to be added to your network group, known as static membership. Or you can use Azure Policy to define conditions that govern your group membership dynamically, or dynamic membership. For more information about Azure Policy initiatives, see Azure Virtual Network Manager and Azure Policy.

Next, you create connectivity and/or security configuration(s) applied to those network groups based on your topology and security needs. A connectivity configuration enables you to create a mesh or a hub-and-spoke network topology. A security configuration allows you to define a collection of rules that you can apply to one or more network groups at the global level. Once you've created your desired network groups and configurations, you can deploy the configurations to any region of your choosing.

Azure Virtual Network Manager can be deployed and managed through the Azure portal, Azure CLI, Azure PowerShell, or Terraform.

## Key benefits

1) Centrally manage connectivity and security policies globally across regions and subscriptions.

2) Enable direct connectivity between spokes in a hub-and-spoke configuration without the complexity of managing a mesh network.

3) Highly scalable and highly available service with redundancy and replication across the globe.

4) Ability to create network security rules that override network security group rules.

5) Low latency and high bandwidth between resources in different virtual networks using virtual network peering.

6) Roll out network changes through a specific region sequence and frequency of your choosing.

