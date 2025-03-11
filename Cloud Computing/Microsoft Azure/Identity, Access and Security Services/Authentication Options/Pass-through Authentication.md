# Pass-through Authentication

Microsoft Entra pass-through authentication allows your users to sign in to both on-premises and cloud-based applications using the same passwords. This feature provides your users a better experience - one less password to remember, and reduces IT helpdesk costs because your users are less likely to forget how to sign in. When users sign in using Microsoft Entra ID, this feature validates users' passwords directly against your on-premises Active Directory.

This feature is an alternative to Microsoft Entra Password Hash Synchronization, which provides the same benefit of cloud authentication to organizations. However, certain organizations wanting to enforce their on-premises Active Directory security and password policies, can choose to use Pass-through Authentication instead. 

You can combine Pass-through Authentication with the Seamless single sign-on feature. If you have Windows 10 or later machines, use Microsoft Entra hybrid join. This way, when your users are accessing applications on their corporate machines inside your corporate network, they don't need to type in their passwords to sign in.

## Benefits

### Great user experience

1) Users use the same passwords to sign into both on-premises and cloud-based applications.

2) Users spend less time talking to the IT helpdesk resolving password-related issues.

3) Users can complete self-service password management tasks in the cloud.

### Easy to deploy & administer

1) No need for complex on-premises deployments or network configuration.

2) Needs just a lightweight agent to be installed on-premises.

3) No management overhead. The agent automatically receives improvements and bug fixes.

### Secure

1) On-premises passwords are never stored in the cloud in any form.

2) Protects your user accounts by working seamlessly with Microsoft Entra Conditional Access policies, including multifactor authentication (MFA), blocking legacy authentication and by filtering out brute force password attacks.

3) The agent only makes outbound connections from within your network. Therefore, there is no requirement to install the agent in a perimeter network, also known as a DMZ.

4) The communication between an agent and Microsoft Entra ID is secured using certificate-based authentication. These certificates are automatically renewed every few months by Microsoft Entra ID.

### Highly available

1) Additional agents can be installed on multiple on-premises servers to provide high availability of sign-in requests.

## Feature highlights

1) Supports user sign-in into all web browser-based applications and into Microsoft Office client applications that use modern authentication.

2) Sign-in usernames can be either the on-premises default username (userPrincipalName) or another attribute configured in Microsoft Entra Connect (known as Alternate ID).

3) The feature works seamlessly with Conditional Access features such as multifactor authentication (MFA) to help secure your users.

4) Integrated with cloud-based self-service password management, including password writeback to on-premises Active Directory and password protection by banning commonly used passwords.

5) Multi-forest environments are supported if there are forest trusts between your AD forests and if name suffix routing is correctly configured.

6) It is a free feature, and you don't need any paid editions of Microsoft Entra ID to use it.

7) It can be enabled via Microsoft Entra Connect.

8) It uses a lightweight on-premises agent that listens for and responds to password validation requests.

9) Installing multiple agents provides high availability of sign-in requests.

10) It protects your on-premises accounts against brute force password attacks in the cloud.
