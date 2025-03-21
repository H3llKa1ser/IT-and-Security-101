# Entitlement Management

Entitlement management is an identity governance feature that enables organizations to manage identity and access lifecycle at scale, by automating access request workflows, access assignments, reviews, and expiration.

People in organizations need access to various groups, applications, and SharePoint Online sites to perform their job. Managing this access is challenging, as requirements change. New applications are added or users need more access rights. This scenario gets more complicated when you collaborate with outside organizations. You may not know who in the other organization needs access to your organization's resources, and they won't know what applications, groups, or sites your organization is using.

Entitlement management can help you more efficiently manage access to groups, applications, and SharePoint Online sites for internal users, and also for users outside your organization who need access to those resources.

## Why use entitlement management>

Enterprise organizations often face challenges when managing workforce access to resources such as:

1) Users may not know what access they should have, and even if they do, they may have difficulty locating the right individuals to approve their access.

2) Once users find and receive access to a resource, they may hold on to access longer than is required for business purposes.

These problems are compounded for users who need access from another organization, such as external users that are from supply chain organizations or other business partners. For example:

1) No one person may know all of the specific individuals in other organization's directories to be able to invite them.

2) Even if they were able to invite these users, no one in that organization may remember to manage all of the users' access consistently.

Entitlement management can help address these challenges. To learn more about how customers have been using entitlement management, you can read the Mississippi Division of Medicaid, Store brand and Avanade case studies.

## What can I do with entitlement management?

Here are some of capabilities of entitlement management:

1) Control who can get access to applications, groups, Teams and SharePoint sites, with multi-stage approval, and ensure users don't retain access indefinitely through time-limited assignments and recurring access reviews.

2) Give users access automatically to those resources, based on the user's properties like department or cost center, and remove a user's access when those properties change.

3) Delegate to non-administrators the ability to create access packages. These access packages contain resources that users can request, and the delegated access package managers can define policies with rules for which users can request, who must approve their access, and when access expires.

4) Select connected organizations whose users can request access. When a user who isn't yet in your directory requests access, and is approved, they're automatically invited into your directory and assigned access. When their access expires, if they have no other access package assignments, their B2B account in your directory can be automatically removed.

## What are access packages and what resources can I manage with them?

Entitlement management introduces the concept of an access package. An access package is a bundle of all the resources with the access a user needs to work on a project or perform their task. Access packages can be used to govern access for your employees, and also for users who originate outside your organization.

Here are the types of resources you can manage user's access to, with entitlement management:

1) Membership of Microsoft Entra security groups.

2) Membership of Microsoft 365 Groups and Teams.

3) Assignment to Microsoft Entra enterprise applications, including SaaS applications and custom-integrated applications that support federation/single sign-on and/or provisioning.

4) Membership of SharePoint Online sites.

You can also control access to other resources that rely upon Microsoft Entra security groups or Microsoft 365 Groups. For example:

1) You can give users licenses for Microsoft 365 by using a Microsoft Entra security group in an access package and configuring group-based licensing for that group.

2) You can give users access to manage Azure resources by using a Microsoft Entra security group in an access package and creating an Azure role assignment for that group.

3) You can give users access to manage Microsoft Entra roles by using groups assignable to Microsoft Entra roles in an access package and assigning a Microsoft Entra role to that group.

## How do I control who gets access?

With an access package, an administrator or delegated access package manager lists the resources (groups, apps, and sites), and the roles the users need for those resources.

Access packages also include one or more policies. A policy defines the rules or guardrails for assignment to access package. Each policy can be used to ensure that only the appropriate users are able to have access assignments, and the access is time-limited and will expire if not renewed.

You can have policies for users to request access. In these kinds of policies, an administrator or access package manager defines

1) Either the already-existing users (typically employees or already-invited guests), or the partner organizations of external users that are eligible to request access.

2) The approval process and the users that can approve or deny access.

3) The duration of a user's access assignment, once approved, before the assignment expires.

You can also have policies for users to be assigned access, either by an administrator, automatically based on rules, or through lifecycle workflows.

![image](https://github.com/user-attachments/assets/55b1cf0d-3fa5-4af7-a523-dcd1272f5bb3)

## When should I use access packages?

Access packages don't replace other mechanisms for access assignment. They're most appropriate in situations such as:

1) Migrating access policy definitions from a third party enterprise role management to Microsoft Entra ID.

2) Users need time-limited access for a particular task. For example, you might use group-based licensing and a dynamic group to ensure all employees have an Exchange Online mailbox, and then use access packages for situations in which employees need more access rights. For example, rights to read departmental resources from another department.

3) Access that requires the approval of a person's manager or other designated individuals.

4) Access that should be assigned automatically to people in a particular part of an organization during their time in that job role, but also available for people elsewhere in the organization, or in a business partner organization, to request.

5) Departments wish to manage their own access policies for their resources without IT involvement.

6) Two or more organizations are collaborating on a project, and as a result, multiple users from one organization will need to be brought in via Microsoft Entra B2B to access another organization's resources.

## How do I delegate access?

Access packages are defined in containers called catalogs. You can have a single catalog for all your access packages, or you can designate individuals to create and own their own catalogs. An administrator can add resources to any catalog, but a non-administrator can only add to a catalog the resources that they own. A catalog owner can add other users as catalog co-owners, or as access package managers. These scenarios are described further in the article delegation and roles in entitlement management.

## Terminology

| Term | Description |
|------|------------|
| **access package** | A bundle of resources that a team or project needs and is governed with policies. An access package is always contained in a catalog. You would create a new access package for a scenario in which users need to request access. |
| **access request** | A request to access the resources in an access package. A request typically goes through an approval workflow. If approved, the requesting user receives an access package assignment. |
| **assignment** | An assignment of an access package to a user ensures the user has all the resource roles of that access package. Access package assignments typically have a time limit before they expire. |
| **catalog** | A container of related resources and access packages. Catalogs are used for delegation, so that non-administrators can create their own access packages. Catalog owners can add resources they own to a catalog. |
| **catalog creator** | A collection of users who are authorized to create new catalogs. When a non-administrator user who is authorized to be a catalog creator creates a new catalog, they automatically become the owner of that catalog. |
| **connected organization** | An external Microsoft Entra directory or domain that you have a relationship with. The users from a connected organization can be specified in a policy as being allowed to request access. |
| **policy** | A set of rules that defines the access lifecycle, such as how users get access, who can approve, and how long users have access through an assignment. A policy is linked to an access package. For example, an access package could have two policies - one for employees to request access and a second for external users to request access. |
| **resource** | An asset, such as an Office group, a security group, an application, or a SharePoint Online site, with a role that a user can be granted permissions to. |
| **resource directory** | A directory that has one or more resources to share. |
| **resource role** | A collection of permissions associated with and defined by a resource. A group has two roles - member and owner. SharePoint sites typically have three roles but may have other custom roles. Applications can have custom roles. |

## License requirements

Using this feature requires Microsoft Entra ID Governance subscriptions for your organization's users. Some capabilities within this feature may operate with a Microsoft Entra ID P2 subscription, see the articles of each capability for more details.

## Delegation and roles in entitlement management

In Microsoft Entra ID, you can use role models to manage access at scale through identity governance.

1) You can use access packages to represent organizational roles in your organization, such as "sales representative". An access package representing that organizational role would include all the access rights that a sales representative might typically need, across multiple resources.

2) Applications can define their own roles. For example, if you had a sales application, and that application included the app role "salesperson" in its manifest, you could then include that role from the app manifest in an access package. Applications can also use security groups in scenarios where a user could have multiple application-specific roles simultaneously.

3) You can use roles for delegating administrative access. If you have a catalog for all the access packages needed by sales, you could assign someone to be responsible for that catalog, by assigning them a catalog-specific role.

This unit discusses how to use roles to manage aspects within Microsoft Entra entitlement management, for controlling access to the entitlement management resources.

By default, users in the Global Administrator role or the Identity Governance Administrator role can create and manage all aspects of entitlement management. However, the users in these roles may not know all the situations where access packages are required. Typically it's users within the respective departments, teams, or projects who know who they're collaborating with, using what resources, and for how long. Instead of granting unrestricted permissions to non-administrators, you can grant users the least permissions they need to do their job and avoid creating conflicting or inappropriate access rights.

## Delegated management of guest user lifecycle

ypically, a user in a role with Guest Inviter privileges can invite individual external users to an organization, and this setting can be changed using the external collaboration settings.

For managing external collaboration, where the individual external users for a collaboration project may not be known in advance, assigning users who are working with external organizations into entitlement management roles can allow them to configure catalogs, access packages and policies for their external collaboration. These configurations allow the external users they're collaborating with to request and be added to your organization's directory and access packages.

1) To allow users in external directories from connected organizations to be able to request access packages in a catalog, the catalog setting of Enabled for external users needs to be set to Yes. Changing this setting can be done by an administrator or a catalog owner of the catalog.

2) The access package must also have a policy set for users not in your directory. This policy can be created by an administrator, catalog owner or access package manager of the catalog.

3) An access package with that policy will allow users in scope to be able to request access, including users not already in your directory. If their request is approved, or doesn't require approval, then the user will be automatically added to your directory.

4) If the policy setting was for All users, and the user wasn't part of an existing connected organization, then a new proposed connected organization is automatically created. You can view the list of connected organizations and remove organizations that are no longer needed.

You can also configure what happens when an external user brought in by entitlement management loses their last assignment to any access packages. You can block them from signing in to this directory, or have their guest account removed, in the settings to manage the lifecycle of external users.

