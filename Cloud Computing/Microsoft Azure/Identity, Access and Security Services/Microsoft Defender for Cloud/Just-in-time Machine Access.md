# Just-in-time machine access

Defender for Servers Plan 2 in Microsoft Defender for Cloud provides a just-in-time machine access feature.

Threat actors actively hunt accessible machines with open management ports, like RDP or SSH. All of your machines are potential targets for an attack. When a machine is successfully compromised, it's used as the entry point to attack further resources in the environment.

To reduce attack surfaces, we want fewer open ports, especially management ports. Legitimate users also use these ports, so it's not practical to keep them closed.

To solve this dilemma, Defender for Cloud offers just-in-time machine access so that you can lock down the inbound traffic to your VMs, reducing exposure to attacks while providing easy access to connect to VMs when needed. Just-in-time access is available when Defender for Servers Plan 2 is enabled.

## Just-in-time access and network resources

### Azure

In Azure, you can block inbound traffic on specific ports, by enabling just-in-time access.

1) Defender for Cloud ensures "deny all inbound traffic" rules exist for your selected ports in the network security group (NSG) and Azure Firewall rules.

2) These rules restrict access to your Azure VMs’ management ports and defend them from attack.

3) If other rules already exist for the selected ports, then those existing rules take priority over the new "deny all inbound traffic" rules.

4) If there are no existing rules on the selected ports, then the new rules take top priority in the NSG and Azure Firewall.

### AWS

In AWS, by enabling just-in-time access, the relevant rules in the attached EC2 security groups (for the selected ports) are revoked, blocking inbound traffic on those specific ports.

1) When a user requests access to a VM, Defender for Servers checks that the user has Azure role-based access control (Azure RBAC) permissions for that VM.

2) If the request is approved, Defender for Cloud configures the NSGs and Azure Firewall to allow inbound traffic to the selected ports from the relevant IP address (or range), for the amount of time that was specified.

3) In AWS, Defender for Cloud creates a new EC2 security group that allows inbound traffic to the specified ports.

4) After the time has expired, Defender for Cloud restores the NSGs to their previous states

5) Connections that are already established aren't interrupted.

#### NOTE: Just-in-time access doesn't support VMs protected by Azure Firewalls controlled by Azure Firewall Manager. The Azure Firewall must be configured with Rules (Classic) and can't use Firewall policies.

## Identify VMs for just-in-time access

The following diagram shows the logic that Defender for Servers applies when deciding how to categorize your supported VMs:

![image](https://github.com/user-attachments/assets/1931f25e-4068-4794-8cb1-7a8b50fa6feb)

When Defender for Cloud finds a machine that can benefit from just-in-time access, it adds that machine to the recommendation's Unhealthy resources tab.

# Enable just-in-time access

Defender for Servers in Microsoft Defender for Cloud provides a just-in-time machine access feature.

You can use Microsoft Defender for Cloud's just-in-time access to protect your Azure VMs from unauthorized network access. Many times firewalls contain allow rules that leave your VMs vulnerable to attack. JIT lets you allow access to your VMs only when the access is needed, on the ports needed, and for the period of time needed.

## Prerequisites

Microsoft Defender for Servers Plan 2 must be enabled on the subscription.

Supported VMs: VMs deployed through Azure Resource Manager, VMs protected by Azure Firewalls on the same VNET as the VM, AWS EC2 instances (Preview)

Unsupported VMs: VMs deployed with classic deployment models, VMs protected by Azure Firewalls controlled by Azure Firewall Manager

To set up just-in-time access on your AWS VMs, you need to connect your AWS account to Microsoft Defender for Cloud.

To JIT policy, the policy name, together with the targeted VM name, must not exceed a total of 56 characters.

You need Reader and SecurityReader permissions, or a custom role can view the JIT status and parameters.

For a custom role, assign the permissions summarized in the table. To create a least-privileged role for users that only need to request JIT access to a VM, use the Set-JitLeastPrivilegedRole script. 

Link: https://github.com/Azure/Microsoft-Defender-for-Cloud/tree/main/Powershell%20scripts/JIT%20Scripts/JIT%20Custom%20Role

| **User Action**                          | **Permissions to Set** |
|-------------------------------------------|------------------------|
| **Configure or edit a JIT policy for a VM** | Assign these actions to the role: <br> On the scope of a subscription (or resource group when using API or PowerShell only) that is associated with the VM: <br> - `Microsoft.Security/locations/jitNetworkAccessPolicies/write` <br> On the scope of a subscription (or resource group when using API or PowerShell only) of VM: <br> - `Microsoft.Compute/virtualMachines/write` |
| **Request JIT access to a VM**           | Assign these actions to the user: <br> - `Microsoft.Security/locations/jitNetworkAccessPolicies/initiate/action` <br> - `Microsoft.Security/locations/jitNetworkAccessPolicies/*/read` <br> - `Microsoft.Compute/virtualMachines/read` <br> - `Microsoft.Network/networkInterfaces/*/read` <br> - `Microsoft.Network/publicIPAddresses/read` |
| **Read JIT policies**                     | Assign these actions to the user: <br> - `Microsoft.Security/locations/jitNetworkAccessPolicies/read` <br> - `Microsoft.Security/locations/jitNetworkAccessPolicies/initiate/action` <br> - `Microsoft.Security/policies/read` <br> - `Microsoft.Security/pricings/read` <br> - `Microsoft.Compute/virtualMachines/read` <br> - `Microsoft.Network/*/read` |

#### NOTE: Only the Microsoft.Security permissions are relevant for AWS. To create a least-privileged role for users that only need to request JIT access to a VM, use the Set-JitLeastPrivilegedRole script.

