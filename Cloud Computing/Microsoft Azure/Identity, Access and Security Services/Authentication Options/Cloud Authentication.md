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

# Cloud authentication: Pass-through authentication

1) Effort. For pass-through authentication, you need one or more (we recommend three) lightweight agents installed on existing servers. These agents must have access to your on-premises Active Directory Domain Services, including your on-premises AD domain controllers. They need outbound access to the Internet and access to your domain controllers. For this reason, it's not supported to deploy the agents in a perimeter network. Pass-through Authentication requires unconstrained network access to domain controllers. All network traffic is encrypted and limited to authentication requests. For more information on this process, see the security deep dive on pass-through authentication.

2) User experience. To improve users' sign-in experience, use Microsoft Entra joined devices or Microsoft Entra hybrid joined devices. If you can't join your Windows devices to Microsoft Entra ID, we recommend deploying seamless SSO with password hash synchronization. Seamless SSO eliminates unnecessary prompts when users are signed in.

3) Advanced scenarios. Pass-through Authentication enforces the on-premises account policy at the time of sign-in. For example, access is denied when an on-premises user's account state is disabled, locked out, or their password expires or the logon attempt falls outside the hours when the user is allowed to sign in. Organizations that require multifactor authentication with pass-through authentication must use Microsoft Entra multifactor authentication or Conditional Access custom controls. Those organizations can't use a third-party or on-premises multifactor authentication method that relies on federation. Advanced features require that password hash synchronization is deployed whether or not you choose pass-through authentication. An example is the leaked credentials report of Identity Protection.

4) Business continuity. We recommend that you deploy two extra pass-through authentication agents. These extras are in addition to the first agent on the Microsoft Entra Connect server. This other deployment ensures high availability of authentication requests. When you have three agents deployed, one agent can still fail when another agent is down for maintenance. There's another benefit to deploying password hash synchronization in addition to pass-through authentication. It acts as a backup authentication method when the primary authentication method is no longer available.

5) Considerations. You can use password hash synchronization as a backup authentication method for pass-through authentication, when the agents can't validate a user's credentials due to a significant on-premises failure. Fail over to password hash synchronization doesn't happen automatically and you must use Microsoft Entra Connect to switch the sign-on method manually.

