# Multi-Factor Authentication (MFA) Implementation 

Multifactor authentication is a process in which a user is prompted for additional forms of identification during a sign-in event. For example, the prompt could be to enter a code on their cellphone or to provide a fingerprint scan. When you require a second form of identification, security is increased because this additional factor isn't easy for an attacker to obtain or duplicate.

Microsoft Entra multifactor authentication and Conditional Access policies give you the flexibility to require MFA from users for specific sign-in events.

## Prerequisites

A working Microsoft Entra tenant with Microsoft Entra ID P1 or trial licenses enabled.

If you need to, create one for free.
An account with at least the Conditional Access Administrator role. Some MFA settings can also be managed by an Authentication Policy Administrator.

A non-administrator account with a password that you know. For this tutorial, we created an account, named testuser. In the tutorial, you test the end-user experience of configuring and using Microsoft Entra multifactor authentication.

If you need information about creating a user account, see Add or delete users using Microsoft Entra ID.
A group that the non-administrator user is a member. For the tutorial, we created a group, named MFA-Test-Group. In the tutorial, you enable Microsoft Entra multifactor authentication for this group.

If you need more information about creating a group, see Create a basic group and add members using Microsoft Entra ID.

### Create a Conditional Access policy

#### TIP: Steps in the example might vary slightly based on the portal you start from.

The recommended way to enable and use Microsoft Entra multifactor authentication is with Conditional Access policies. Conditional Access lets you create and define policies that react to sign-in events and that request additional actions before a user is granted access to an application or service.

Conditional Access policies can be applied to specific users, groups, and apps. The goal is to protect your organization while also providing the right levels of access to the users who need it.

In this tutorial, we create a basic Conditional Access policy to prompt for MFA when a user signs in.

First, create a Conditional Access policy and assign your test group of users as follows:

Sign in to the Microsoft Entra admin center as at least a Conditional Access Administrator.

Browse to Protection > Conditional Access, select + New policy, and then select Create new policy.

![image](https://github.com/user-attachments/assets/f638be13-a247-4157-8eaf-81385859b0da)

Enter a name for the policy, such as MFA Pilot.

Under Assignments, select the current value under Users or workload identities.

![image](https://github.com/user-attachments/assets/abbf803f-f80b-4f83-9f16-347961b4939c)

Under What does this policy apply to?, verify that Users and groups is selected.

Under Include, choose Select users and groups, and then select Users and groups.

![image](https://github.com/user-attachments/assets/12f4784c-df39-4bb2-bfe3-232bdfed0e87)

#### NOTE: Since no one is assigned yet, the list of users and groups (shown in the next step) opens automatically.

Browse for and select your Microsoft Entra group, such as MFA-Test-Group, then choose Select.

![image](https://github.com/user-attachments/assets/6f8963ca-fd4e-4389-b09e-a15983a3e2bf)

#### NOTE: We've selected the group to apply the policy to. In the next section, we configure the conditions under which to apply the policy.

### Configure the conditions for multifactor authentication

Now that the Conditional Access policy is created and a test group of users is assigned, define the cloud apps or actions that trigger the policy. These cloud apps or actions are the scenarios that you decide require additional processing, such as prompting for multifactor authentication. For example, you could decide that access to a financial application or use of management tools require an additional prompt for authentication.

### Configure which apps require multifactor authentication

For this tutorial, configure the Conditional Access policy to require multifactor authentication when a user signs in.

Select the current value under Cloud apps or actions, and then under Select what this policy applies to, verify that Cloud apps is selected.

Under Include, choose Select apps.

#### NOTE: Since no apps are yet selected, the list of apps (shown in the next step) opens automatically.

#### TIP: You can choose to apply the Conditional Access policy to All cloud apps or Select apps. To provide flexibility, you can also exclude certain apps from the policy.

Browse the list of available sign-in events that can be used. For this example, select Windows Azure Service Management API so that the policy applies to sign-in events. Then choose Select.

![image](https://github.com/user-attachments/assets/0ab48e21-d167-47d9-a15f-533ec35056f6)

### Configure multifactor authentication for access

Next, we configure access controls. Access controls let you define the requirements for a user to be granted access. They might be required to use an approved client app or a device that's hybrid joined to Microsoft Entra ID.

In this tutorial, configure the access controls to require multifactor authentication during a sign-in event.

Under Access controls, select the current value under Grant, and then select Grant access.

![image](https://github.com/user-attachments/assets/04d39ecf-8774-4cee-8fd3-85856859764e)

Select Require multifactor authentication, and then choose Select.

![image](https://github.com/user-attachments/assets/57854e5d-9549-4bc0-a6f9-dd5a81bd8366)

### Activate the policy

Conditional Access policies can be set to Report-only if you want to see how the configuration would affect users, or Off if you don't want to the use policy right now. Because a test group of users is targeted for this tutorial, let's enable the policy, and then test Microsoft Entra multifactor authentication.

Under Enable policy, select On.

![image](https://github.com/user-attachments/assets/a2f01ffa-5523-48a7-a174-0640bcf43270)

To apply the Conditional Access policy, select Create.

## Test Microsoft Entra multifactor authentication

First, sign in to a resource that doesn't require MFA:

1) Open a new browser window in InPrivate or incognito mode and browse to https://account.activedirectory.windowsazure.com. Using a private mode for your browser prevents any existing credentials from affecting this sign-in event.

2) Sign in with your non-administrator test user, such as testuser. Be sure to include @ and the domain name for the user account. If this is the first instance of signing in with this account, you're prompted to change the password. However, there's no prompt for you to configure or use multifactor authentication.

3) Close the browser window.

You configured the Conditional Access policy to require additional authentication for sign in. Because of that configuration, you're prompted to use Microsoft Entra multifactor authentication or to configure a method if you haven't yet done so.

Test this new requirement by signing in to the Microsoft Entra admin center:

1) Open a new browser window in InPrivate or incognito mode and sign in to the Microsoft Entra admin center.

2) Sign in with your non-administrator test user, such as testuser. Be sure to include @ and the domain name for the user account. You're required to register for and use Microsoft Entra multifactor authentication.

![image](https://github.com/user-attachments/assets/c97d136a-6e3b-4305-a8e9-2fef5d0fcde9)

3) Select Next to begin the process.

You can choose to configure an authentication phone, an office phone, or a mobile app for authentication. Authentication phone supports text messages and phone calls, office phone supports calls to numbers that have an extension, and mobile app supports using a mobile app to receive notifications for authentication or to generate authentication codes.

4) Complete the instructions on the screen to configure the method of multifactor authentication that you've selected.

5) Close the browser window, and sign in to the Microsoft Entra admin center again to test the authentication method that you configured. For example, if you configured a mobile app for authentication, you should see a prompt like the following.

![image](https://github.com/user-attachments/assets/1392422a-b6ac-4d1a-b189-4006c1d3d426)

6) Close the browser window

## Configure Microsoft Entra multifactor authentication settings

To customize the end-user experience for Microsoft Entra multifactor authentication, you can configure options for settings like account lockout thresholds or fraud alerts and notifications.

The following Microsoft Entra multifactor authentication settings are available in the Azure portal:

| Feature                            | Description |
|------------------------------------|-------------|
| **Account lockout (MFA Server only)** | Temporarily lock accounts from using Microsoft Entra multifactor authentication if there are too many denied authentication attempts in a row. This feature applies only to users who use MFA Server to enter a PIN to authenticate. |
| **Block/unblock users**            | Block specific users from being able to receive Microsoft Entra multifactor authentication requests. Any authentication attempts for blocked users are automatically denied. Users remain blocked for 90 days from the time that they're blocked or until they're manually unblocked. |
| **Fraud alert**                     | Configure settings that allow users to report fraudulent verification requests. |
| **Report suspicious activity**      | Configure settings that allow users to report fraudulent verification requests. |
| **Notifications**                    | Enable notifications of events from MFA Server. |
| **OATH tokens**                      | Used in cloud-based Microsoft Entra multifactor authentication environments to manage OATH tokens for users. |
| **Phone call settings**              | Configure settings related to phone calls and greetings for cloud and on-premises environments. |
| **Providers**                        | This will show any existing authentication providers that you've associated with your account. Adding new providers is disabled as of September 1, 2018. |
