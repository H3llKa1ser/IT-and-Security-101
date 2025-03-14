# Microsoft Entra Privileged Identity Management

Privileged Identity Management provides time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions on resources that you care about. Here are some of the key features of Privileged Identity Management:

1) Provide just-in-time privileged access to Microsoft Entra ID and Azure resources.

2) Assign time-bound access to resources using start and end dates.

3) Require approval to activate privileged roles.

4) Enforce multifactor authentication to activate any role.

5) Use justification to understand why users activate.

6) Get notifications when privileged roles are activated.

7) Conduct access reviews to ensure users still need roles.

8) Download audit history for internal or external audit.

9) Prevents removal of the last active Global Administrator and Privileged Role Administrator role assignments.

Once you set up Privileged Identity Management, you'll see Tasks, Manage, and Activity options in the left navigation menu. As an administrator, you can choose between options such as managing Microsoft Entra roles, managing Azure resource roles, or PIM for Groups. When you choose what you want to manage, you see the appropriate set of options for that option.

For Microsoft Entra roles in Privileged Identity Management, only a user who is in the Privileged Role Administrator or Global Administrator role can manage assignments for other administrators. Global Administrators, Security Administrators, Global Readers, and Security Readers can also view assignments to Microsoft Entra roles in Privileged Identity Management.

For Azure resource roles in Privileged Identity Management, only a subscription administrator, a resource Owner, or a resource User Access administrator can manage assignments for other administrators. Users who are Privileged Role Administrators, Security Administrators, or Security Readers don't by default have access to view assignments to Azure resource roles in Privileged Identity Management.

## Terminology

To better understand Privileged Identity Management and its documentation, you should review the following terms.

| Term                        | Definition |
|-----------------------------|------------|
| **action**                  | An activity a security principal can perform on an object type. Sometimes referred to as an operation. |
| **permission**              | A definition that specifies the activity a security principal can perform on an object type. A permission includes one or more actions. |
| **privileged permission**   | In Microsoft Entra ID, permissions that can be used to delegate management of directory resources to other users, modify credentials, authentication or authorization policies, or access restricted data. |
| **privileged role**         | A built-in or custom role that has one or more privileged permissions. |
| **privileged role assignment** | A role assignment that uses a privileged role. |
| **elevation of privilege**  | When a security principal obtains more permissions than their assigned role initially provided by impersonating another role. |
| **protected action**        | Permissions with Conditional Access applied for added security. |

## Role assignment overview

The PIM role assignments give you a secure way to grant access to resources in your organization. This section describes the assignment process. It includes assign roles to members, activate assignments, approve or deny requests, extend and renew assignments.

PIM keeps you informed by sending you and other participants email notifications. These emails might also include links to relevant tasks, such activating, approve or deny a request.

The following screenshot shows an email message sent by PIM. The email informs Administrator-B that Administrator-A updated a role assignment for Member-1.

![image](https://github.com/user-attachments/assets/2032bf1a-dbfd-4f03-841a-f1471fecf828)

## Assign

The assignment process starts by assigning roles to members. To grant access to a resource, the administrator assigns roles to users, groups, service principals, or managed identities. The assignment includes the following data:

1) The members or owners to assign the role.

2) The scope of the assignment. The scope limits the assigned role to a particular set of resources.

3) The type of the assignment

Eligible assignments require the member of the role to perform an action to use the role. Actions might include activation, or requesting approval from designated approvers.
Active assignments don't require the member to perform any action to use the role. Members assigned as active have the privileges assigned to the role.

4) The duration of the assignment, using start and end dates or permanent. For eligible assignments, the members can activate or requesting approval during the start and end dates. For active assignments, the members can use the assign role during this period of time.

The following screenshot shows how administrator assigns a role to members.

![image](https://github.com/user-attachments/assets/0ff5a47c-7f24-49c4-9ec3-7d622f3724c4)

## Activate

If users have been made eligible for a role, then they must activate the role assignment before using the role. To activate the role, users select specific activation duration within the maximum (configured by administrators), and the reason for the activation request.

The following screenshot shows how members activate their role to a limited time.

![image](https://github.com/user-attachments/assets/eeac7a8c-5505-4d8a-a7ff-5920ef3fab9b)

If the role requires approval to activate, a notification appears in the upper right corner of the user's browser informing them the request is pending approval. If an approval isn't required, the member can start using the role.

## Approve or deny

Delegated approvers receive email notifications when a role request is pending their approval. Approvers can view, approve or deny these pending requests in PIM. After the request has been approved, the member can start using the role. For example, if a user or a group was assigned with Contribution role to a resource group, they are able to manage that particular resource group.

## Extend and renew assignments

After administrators set up time-bound owner or member assignments, the first question you might ask is what happens if an assignment expires? In this new version, we provide two options for this scenario:

1) Extend – When a role assignment nears expiration, the user can use Privileged Identity Management to request an extension for the role assignment.

2) Renew – When a role assignment has already expired, the user can use Privileged Identity Management to request a renewal for the role assignment.

Both user-initiated actions require an approval from a Global Administrator or Privileged Role Administrator. Admins don't need to be in the business of managing assignment expirations. You can just wait for the extension or renewal requests to arrive for simple approval or denial.

## Scenarios

Privileged Identity Management supports the following scenarios:

### Privileged Role Administrator permissions

1) Enable approval for specific roles.

2) Specify approver users or groups to approve requests.

3) View request and approval history for all privileged roles.

### Approver permissions

1) View pending approvals (requests).

2) Approve or reject requests for role elevation (single and bulk).

3) Provide justification for my approval or rejection.

### Eligible role user permissions

1) Request activation of a role that requires approval.

2) View the status of your request to activate.

3) Complete your task in Microsoft Entra ID if activation was approved.

## Microsoft Graph APIs

You can use Privileged Identity Management programmatically through the following Microsoft Graph APIs:

1) PIM for Microsoft Entra roles APIs.

2) PIM for groups APIs.

## Reasons to use

Organizations want to minimize the number of people who have access to secure information or resources, because that reduces the chance of

1) A malicious actor getting access.

2) An authorized user inadvertently impacting a sensitive resource.

However, users still need to carry out privileged operations in Microsoft Entra ID, Azure, Microsoft 365, or SaaS apps. Organizations can give users just-in-time privileged access to Azure and Microsoft Entra resources and can oversee what those users are doing with their privileged access.

Privileged Identity Management (PIM) provides a time-based and approval-based role activation to mitigate the risks of excessive, unnecessary, or misused access permissions to important resources. These resources include resources in Microsoft Entra ID, Azure, and other Microsoft Online Services such as Microsoft 365 or Microsoft Intune.

## Understand PIM

The PIM concepts in this section will help you understand your organization’s privileged identity requirements.

Today, you can use PIM with:

1) Microsoft Entra roles – Sometimes referred to as directory roles, Microsoft Entra roles include built-in and custom roles to manage Microsoft Entra ID and other Microsoft 365 online services.

2) Azure roles – The role-based access control (RBAC) roles in Azure that grants access to management groups, subscriptions, resource groups, and resources.

3) PIM for Groups – To set up just-in-time access to member and owner role of a Microsoft Entra security group. PIM for Groups not only gives you an alternative way to set up PIM for Microsoft Entra roles and Azure roles, but also allows you to set up PIM for other permissions across Microsoft online services like Intune, Azure Key Vaults, and Azure Information Protection. If the group is configured for app provisioning, activation of group membership triggers provisioning of group membership (and the user account, if it wasn’t provisioned) to the application using the System for Cross-Domain Identity Management (SCIM) protocol.

You can assign the following to these roles or groups:

1) Users- To get just-in-time access to Microsoft Entra roles, Azure roles, and PIM for Groups.

2) Groups- Anyone in a group to get just-in-time access to Microsoft Entra roles and Azure roles. For Microsoft Entra roles, the group must be a newly created cloud group that’s marked as assignable to a role while for Azure roles, the group can be any Microsoft Entra security group. We don't recommend assigning/nesting a group to a PIM for Groups.

#### NOTE: You cannot assign service principals as eligible to Microsoft Entra roles, Azure roles, and PIM for Groups but you can grant a time limited active assignment to all three.

