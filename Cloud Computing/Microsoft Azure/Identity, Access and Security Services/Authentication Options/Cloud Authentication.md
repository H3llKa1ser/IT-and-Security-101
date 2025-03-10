# Cloud Authentication

When you choose this authentication method, Microsoft Entra ID handles users' sign-in process. Coupled with single sign-on (SSO), users can sign in to cloud apps without having to reenter their credentials. With cloud authentication, you can choose from two options:

1) Microsoft Entra password hash synchronization. The simplest way to enable authentication for on-premises directory objects in Microsoft Entra ID. Users can use the same username and password that they use on-premises without having to deploy any other infrastructure. Some premium features of Microsoft Entra ID, like Identity Protection and Microsoft Entra Domain Services, require password hash synchronization, no matter which authentication method you choose.

2) Microsoft Entra pass-through authentication. Provides a simple password validation for Microsoft Entra authentication services by using a software agent that runs on one or more on-premises servers. The servers validate the users directly with your on-premises Active Directory, which ensures that the password validation doesn't happen in the cloud.

Companies with a security requirement to immediately enforce on-premises user account states, password policies, and sign-in hours might use this authentication method.

# Cloud authentication: Password hash synchronization

1) Effort. Password hash synchronization requires the least effort regarding deployment, maintenance, and infrastructure. This level of effort typically applies to organizations that only need their users to sign in to Microsoft 365, SaaS apps, and other Microsoft Entra ID-based resources. When turned on, password hash synchronization is part of the Microsoft Entra Connect Sync process and runs every two minutes.

2) User experience. To improve users' sign-in experience, use Microsoft Entra joined devices or Microsoft Entra hybrid joined devices. If you can't join your Windows devices to Microsoft Entra ID, we recommend deploying seamless SSO with password hash synchronization. Seamless SSO eliminates unnecessary prompts when users are signed in.

3) Advanced scenarios. If organizations choose to, it's possible to use insights from identities with Microsoft Entra ID Protection reports with Microsoft Entra ID P2. An example is the leaked credentials report. Windows Hello for Business has specific requirements when you use password hash synchronization. Microsoft Entra Domain Services requires password hash synchronization to provision users with their corporate credentials in the managed domain.

Organizations that require multifactor authentication with password hash synchronization must use Microsoft Entra multifactor authentication or Conditional Access custom controls. Those organizations can't use third-party or on-premises multifactor authentication methods that rely on federation.

#### NOTE: Microsoft Entra Conditional Access require Microsoft Entra ID P1 licenses.

4) Business continuity. Using password hash synchronization with cloud authentication is highly available as a cloud service that scales to all Microsoft datacenters. To make sure password hash synchronization doesn't go down for extended periods, deploy a second Microsoft Entra Connect server in staging mode in a standby configuration.

5) Considerations. Currently, password hash synchronization doesn't immediately enforce changes in on-premises account states. In this situation, a user has access to cloud apps until the user account state is synchronized to Microsoft Entra ID. Organizations might want to overcome this limitation by running a new synchronization cycle after administrators do bulk updates to on-premises user account states. An example is disabling accounts.

