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

