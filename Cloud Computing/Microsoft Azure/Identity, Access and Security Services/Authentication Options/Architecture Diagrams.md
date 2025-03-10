# Architecture Diagrams

The following diagrams outline the high-level architecture components required for each authentication method you can use with your Microsoft Entra hybrid identity solution. They provide an overview to help you compare the differences between the solutions.

1) Simplicity of a password hash synchronization solution:

![image](https://github.com/user-attachments/assets/03d24cb6-6382-4e42-a7ed-affb3876dbf8)

2) Agent requirements of pass-through authentication, using two agents for redundancy:

![image](https://github.com/user-attachments/assets/4df45beb-0655-4f79-88b4-4031638d5124)

3) Components required for federation in your perimeter and internal network of your organization:

![image](https://github.com/user-attachments/assets/8b547083-39c1-42c2-b6e5-b9e242a25b7f)

# Comparing Methods

| **Consideration** | **Password Hash Synchronization** | **Pass-through Authentication** | **Federation with AD FS** |
|-------------------|--------------------------------|---------------------------|-----------------------|
| **Where does authentication happen?** | In the cloud | In the cloud, after a secure password verification exchange with the on-premises authentication agent | On-premises |
| **On-premises server requirements beyond Microsoft Entra Connect** | None | One server for each additional authentication agent | Two or more AD FS servers<br>Two or more WAP servers in the perimeter/DMZ network |
| **Requirements for on-premises Internet and networking** | None | Outbound Internet access from the servers running authentication agents | Inbound Internet access to WAP servers in the perimeter<br>Inbound network access to AD FS servers from WAP servers in the perimeter<br>Network load balancing |
| **TLS/SSL certificate requirement?** | No | No | Yes |
| **Health monitoring solution?** | Not required | Agent status provided by the Microsoft Entra admin center | Microsoft Entra Connect Health |
| **SSO to cloud resources from domain-joined devices within the company network?** | Yes with Microsoft Entra joined devices, Microsoft Entra hybrid joined devices, the Microsoft Enterprise SSO plug-in for Apple devices, or Seamless SSO | Yes with Microsoft Entra joined devices, Microsoft Entra hybrid joined devices, the Microsoft Enterprise SSO plug-in for Apple devices, or Seamless SSO | Yes |
| **Supported sign-in types** | UserPrincipalName + password<br>Windows-Integrated Authentication by using Seamless SSO<br>Alternate login ID<br>Microsoft Entra joined Devices<br>Microsoft Entra hybrid joined devices<br>Certificate and smart card authentication | UserPrincipalName + password<br>Windows-Integrated Authentication by using Seamless SSO<br>Alternate login ID<br>Microsoft Entra joined Devices<br>Microsoft Entra hybrid joined devices<br>Certificate and smart card authentication | UserPrincipalName + password<br>sAMAccountName + password<br>Windows-Integrated Authentication<br>Certificate and smart card authentication<br>Alternate login ID |
| **Windows Hello for Business support?** | Key trust model<br>Hybrid Cloud Trust | Key trust model<br>Hybrid Cloud Trust<br>Both require Windows Server 2016 Domain functional level | Key trust model<br>Hybrid Cloud Trust<br>Certificate trust model |
| **Multifactor authentication options** | Microsoft Entra multifactor authentication<br>Custom Controls with Conditional Access | Microsoft Entra multifactor authentication<br>Custom Controls with Conditional Access | Microsoft Entra multifactor authentication<br>Third-party MFA<br>Custom Controls with Conditional Access |
| **Supported user account states** | Disabled accounts (up to 30-minute delay) | Disabled accounts<br>Account locked out<br>Account expired<br>Password expired<br>Sign-in hours | Disabled accounts<br>Account locked out<br>Account expired<br>Password expired<br>Sign-in hours |
| **Conditional Access options** | Microsoft Entra Conditional Access, with Microsoft Entra ID P1 or P2 | Microsoft Entra Conditional Access, with Microsoft Entra ID P1 or P2 | Microsoft Entra Conditional Access, with Microsoft Entra ID P1 or P2<br>AD FS claim rules |
| **Blocking legacy protocols supported?** | Yes | Yes | Yes |
| **Customizable sign-in pages?** | Yes, with Microsoft Entra ID P1 or P2 | Yes, with Microsoft Entra ID P1 or P2 | Yes |
| **Advanced scenarios supported** | Smart password lockout<br>Leaked credentials reports, with Microsoft Entra ID P2 | Smart password lockout | Multisite low-latency authentication system<br>AD FS extranet lockout<br>Integration with third-party identity systems |

