# Microsoft Entra ID Access Reviews

Access reviews in Microsoft Entra ID, part of Microsoft Entra, enable organizations to efficiently manage group memberships, access to enterprise applications, and role assignments. User's access can be reviewed regularly to make sure only the right people have continued access.

## Why are access reviews important?

Microsoft Entra ID enables you to collaborate with users from inside your organization and with external users. Users can join groups, invite guests, connect to cloud apps, and work remotely from their work or personal devices. The convenience of using self-service has led to a need for better access management capabilities.

1) As new employees join, how do you ensure they have the access they need to be productive?

2) As people move teams or leave the company, how do you make sure that their old access is removed?

3) Excessive access rights can lead to compromises.

4) Excessive access right may also lead audit findings as they indicate a lack of control over access.

5) You have to proactively engage with resource owners to ensure they regularly review who has access to their resources.

## When should you use access reviews?

1) Too many users in privileged roles: It's a good idea to check how many users have administrative access, how many of them are Global Administrators, and if there are any invited guests or partners that haven't been removed after being assigned to do an administrative task. You can recertify the role assignment users in Microsoft Entra roles such as Global Administrators, or Azure resources roles such as User Access Administrator in the Microsoft Entra Privileged Identity Management (PIM) experience.

2) When automation is not possible: You can create rules for dynamic membership on security groups or Microsoft 365 Groups, but what if the HR data isn't in Microsoft Entra ID or if users still need access after leaving the group to train their replacement? You can then create a review on that group to ensure those who still need access should have continued access.

3) When a group is used for a new purpose: If you have a group that is going to be synced to Microsoft Entra ID, or if you plan to enable the application Salesforce for everyone in the Sales team group, it would be useful to ask the group owner to review the group membership prior to the group being used in a different risk content.

4) Business critical data access: for certain resources, such as business critical applications, it might be required as part of compliance processes to ask people to regularly reconfirm and give a justification on why they need continued access.

5) To maintain a policy's exception list: In an ideal world, all users would follow the access policies to secure access to your organization's resources. However, sometimes there are business cases that require you to make exceptions. As the IT admin, you can manage this task, avoid oversight of policy exceptions, and provide auditors with proof that these exceptions are reviewed regularly.

6) Ask group owners to confirm they still need guests in their groups: Employee access might be automated with other identity and access management features such lifecycle workflows based on data from an HR source, but not invited guests. If a group gives guests access to business sensitive content, then it's the group owner's responsibility to confirm the guests still have a legitimate business need for access.

7) Have reviews recur periodically: You can set up recurring access reviews of users at set frequencies such as weekly, monthly, quarterly or annually, and the reviewers are notified at the start of each review. Reviewers can approve or deny access with a friendly interface and with the help of smart recommendations.

## Where do you create reviews?

Depending on what you want to review, you'll either create your access review in access reviews, Microsoft Entra enterprise apps, PIM, or entitlement management.

| Access Rights of Users                | Reviewers Can Be               | Review Created In                      | Reviewer Experience                        |
|----------------------------------------|--------------------------------|----------------------------------------|--------------------------------------------|
| Security group members                 | Specified reviewers, Group owners, Self-review | Access reviews                 | Microsoft Entra groups, Access panel      |
| Office group members                   | Specified reviewers, Group owners, Self-review | Access reviews                 | Microsoft Entra groups, Access panel      |
| Assigned to a connected app            | Specified reviewers, Self-review | Access reviews                        | Microsoft Entra enterprise apps, Access panel |
| Microsoft Entra enterprise apps        | Specified reviewers, Self-review | Privileged Identity Management        | Microsoft Entra Admin Center              |
| Microsoft Entra role                   | Specified reviewers, Self-review | Privileged Identity Management        | Microsoft Entra Admin Center              |
| Azure resource role                    | Specified reviewers, Self-review | Privileged Identity Management        | Microsoft Entra Admin Center              |
| Access package assignments             | Specified reviewers, Group members, Self-review | Entitlement management | Access panel                              |
