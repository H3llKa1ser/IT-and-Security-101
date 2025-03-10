# Cloud Authentication

When you choose this authentication method, Microsoft Entra ID handles users' sign-in process. Coupled with single sign-on (SSO), users can sign in to cloud apps without having to reenter their credentials. With cloud authentication, you can choose from two options:

1) Microsoft Entra password hash synchronization. The simplest way to enable authentication for on-premises directory objects in Microsoft Entra ID. Users can use the same username and password that they use on-premises without having to deploy any other infrastructure. Some premium features of Microsoft Entra ID, like Identity Protection and Microsoft Entra Domain Services, require password hash synchronization, no matter which authentication method you choose.

2) Microsoft Entra pass-through authentication. Provides a simple password validation for Microsoft Entra authentication services by using a software agent that runs on one or more on-premises servers. The servers validate the users directly with your on-premises Active Directory, which ensures that the password validation doesn't happen in the cloud.

Companies with a security requirement to immediately enforce on-premises user account states, password policies, and sign-in hours might use this authentication method.

