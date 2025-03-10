# Federated Authentication

When you choose this authentication method, Microsoft Entra ID hands off the authentication process to a separate trusted authentication system, such as on-premises Active Directory Federation Services (AD FS), to validate the user's password.

The authentication system can provide other advanced authentication requirements, for example, third-party multifactor authentication.

## Key Concepts and considerations

1) Effort. A federated authentication system relies on an external trusted system to authenticate users. Some companies want to reuse their existing federated system investment with their Microsoft Entra hybrid identity solution. The maintenance and management of the federated system falls outside the control of Microsoft Entra ID. It's up to the organization by using the federated system to make sure it's deployed securely and can handle the authentication load.

2) User experience. The user experience of federated authentication depends on the implementation of the features, topology, and configuration of the federation farm. Some organizations need this flexibility to adapt and configure the access to the federation farm to suit their security requirements. For example, it's possible to configure internally connected users and devices to sign in users automatically, without prompting them for credentials. This configuration works because they already signed in to their devices. If necessary, some advanced security features make users' sign-in process more difficult.

3) Advanced scenarios. A federated authentication solution is required when customers have an authentication requirement that Microsoft Entra ID doesn't support natively. See detailed information to help you choose the right sign-in option. Consider the following common requirements:

 - Third-party multifactor providers requiring a federated identity provider.

 - Authentication by using third-party authentication solutions. See the Microsoft Entra federation compatibility list.

 - Sign in that requires a sAMAccountName, for example DOMAIN\username, instead of a User Principal Name (UPN), for example, user@domain.com.

4) Business continuity. Federated systems typically require a load-balanced array of servers, known as a farm. This farm is configured in an internal network and perimeter network topology to ensure high availability for authentication requests. Deploy password hash synchronization along with federated authentication as a backup authentication method when the primary authentication method is no longer available. An example is when the on-premises servers aren't available. Some large enterprise organizations require a federation solution to support multiple Internet ingress points configured with geo-DNS for low-latency authentication requests.

5) Considerations. Federated systems typically require a more significant investment in on-premises infrastructure. Most organizations choose this option if they already have an on-premises federation investment. And if it's a strong business requirement to use a single-identity provider. Federation is more complex to operate and troubleshoot compared to cloud authentication solutions.

For a nonroutable domain that can't be verified in Microsoft Entra ID, you need extra configuration to implement user ID sign in. This requirement is known as Alternate login ID support. See Configuring Alternate Login ID for limitations and requirements. If you choose to use a third-party multifactor authentication provider with federation, ensure the provider supports WS-Trust to allow devices to join Microsoft Entra ID.

#### NOTE: When you deploy your Microsoft Entra hybrid identity solution, you must implement one of the supported topologies of Microsoft Entra Connect. Learn more about supported and unsupported configurations at Topologies for Microsoft Entra Connect.

