# Microsoft Entra Users

Microsoft Entra ID allows you to create several types of users in your tenant, which provides greater flexibility in how you manage your organization's users.

## Prerequisites

The required role of least privilege varies based on the type of user you're adding and if you need to assign Microsoft Entra roles at the same time. Global Administrator can create users and assign roles, but whenever possible you should use the least privileged role.

| Task                          | Role                          |
|-------------------------------|------------------------------|
| Create a new user             | User Administrator          |
| Invite an external guest      | Guest Inviter               |
| Assign Microsoft Entra roles  | Privileged Role Administrator |


## Types of users

Before you create or invite a new user, take some time to review the types of users, their authentication methods, and their access within the Microsoft Entra tenant. For example, do you need to create an internal guest, an internal user, or an external guest? Does your new user need guest or member privileges?

1) Internal member: These users are most likely full-time employees in your organization.

2) Internal guest: These users have an account in your tenant, but have guest-level privileges. It's possible they were created within your tenant prior to the availability of B2B collaboration.

3) External member: These users authenticate using an external account, but have member access to your tenant. These types of users are common in multitenant organizations.

4) External guest: These users are true guests of your tenant who authenticate using an external method and who have guest-level privileges.

Authentication methods vary based on the type of user you create. Internal guests and members have credentials in your Microsoft Entra tenant that can be managed by administrators. These users can also reset their own password. External members authenticate to their home Microsoft Entra tenant and your Microsoft Entra tenant authenticates the user through a federated sign-in with the external member's Microsoft Entra tenant. If external members forget their password, the administrator in their Microsoft Entra tenant can reset their password. External guests set up their own password using the link they receive in email when their account is created.

# User creation

1) Sign in to the Microsoft Entra admin center as at least a User Administrator.

2) Browse to Identity > Users > All users.

3) Select New user > Create new user.

4) Complete the remaining tabs in the New user page.

## Basics

The Basics tab contains the core fields required to create a new user. Before you begin, review the guidance on user name properties.

1) User principal name: Enter a unique username and select a domain from the menu after the @ symbol. Select Domain not listed if you need to create a new domain. For more information, see Add your custom domain name.

2) Mail nickname: If you need to enter an email nickname that is different from the user principal name you entered, uncheck the Derive from user principal name option, then enter the mail nickname.

3) Display name: Enter the user's name, such as Chris Green or Chris A. Green

4) Password: Provide a password for the user to use during their initial sign-in. Uncheck the Auto-generate password option to enter a different password.

5) Account enabled: This option is checked by default. Uncheck to prevent the new user from being able to sign-in. You can change this setting after the user is created. This setting was called Block sign in in the legacy create user process.

Select Next: Properties to complete the next section.

Either select the Review + create button to create the new user or Next: Properties to complete the next section.

## Properties

There are five categories of user properties you can provide. These properties can be added or updated after the user is created. To manage these details, go to Identity > Users > All users and select a user to update.

1) Identity: Enter the user's first and last name. Set the User type as either Member or Guest.

2) Job information: Add any job-related information, such as the user's job title, department, or manager.

3) Contact information: Add any relevant contact information for the user.

4) Parental controls: For organizations like K-12 school districts, the user's age group may need to be provided. Minors are 12 and under, Not adult are 13-18 years old, and Adults are 18 and over. The combination of age group and consent provided by parent options determine the Legal age group classification. The Legal age group classification may limit the user's access and authority.

5) Settings: Specify the user's global location.

Either select the Review + create button to create the new user or Next: Assignments to complete the next section.

## Assignments

You can assign the user to an administrative unit, group, or Microsoft Entra role when the account is created. You can assign the user to up to 20 groups or roles. You can only assign the user to one administrative unit. Assignments can be added after the user is created.

To assign a group to the new user:

1) Select + Add group.

2) From the menu that appears, choose up to 20 groups from the list and select the Select button.

3) Select the Review + create button.

To assign a role to the new user:

1) Select + Add role.

2) From the menu that appears, choose up to 20 roles from the list and select the Select button.

3) Select the Review + create button.

To add an administrative unit to the new user:

1) Select + Add administrative unit.

2) From the menu that appears, choose one administrative unit from the list and select the Select button.

3) Select the Review + create button.

4) The final tab captures several key details from the user creation process.

