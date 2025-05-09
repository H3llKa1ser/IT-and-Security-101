# Design solutions for detection and response that includes extended detection and response (XDR) and security information and event management (SIEM).

Microsoft Defender XDR is an eXtended detection and response (XDR) solution that automatically collects, correlates, and analyzes signal, threat, and alert data from across your Microsoft 365 environment, including endpoint, email, applications, and identities. It leverages artificial intelligence (AI) and automation to automatically stop attacks, and remediate affected assets into a safe state.

## Microsoft Defender XDR components secure devices, identity, data, and applications

Microsoft Defender XDR is made up of these security technologies, operating in tandem. You don't need all of these components to benefit from the capabilities of XDR and Microsoft Defender XDR. You will realize gains and efficiencies through using one or two as well.

| **Component**                        | **Description**                                                                                                                                       | **Reference material**                                           |
|--------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| **Microsoft Defender for Identity**  | Microsoft Defender for Identity uses Active Directory signals to identify, detect, and investigate advanced threats, compromised identities, and malicious insider actions directed at your organization. | [What is Microsoft Defender for Identity?](https://www.microsoft.com/en-us/microsoft-defender) |
| **Exchange Online Protection**       | Exchange Online Protection is the native cloud-based SMTP relay and filtering service that helps protect your organization against spam and malware. | [Exchange Online Protection (EOP) overview - Office 365](https://docs.microsoft.com/en-us/exchange/antispam-and-antivirus/antispam) |
| **Microsoft Defender for Office 365**| Microsoft Defender for Collaboration safeguards your organization against malicious threats posed by email messages, links (URLs) and collaboration tools. | [Microsoft Defender for Collaboration - Office 365](https://learn.microsoft.com/en-us/microsoft-365/security/office-365-security/defender-for-office-365?view=o365-worldwide) |
| **Microsoft Defender for Endpoint**  | Microsoft Defender for Endpoint is a unified platform for device protection, post-breach detection, automated investigation, and recommended response. | [Microsoft Defender for Endpoint - Windows security](https://www.microsoft.com/en-us/microsoft-defender) |
| **Microsoft Defender for Cloud Apps**| Microsoft Defender for Cloud Apps is a comprehensive cross-SaaS solution bringing deep visibility, strong data controls, and enhanced threat protection to your cloud apps. | [What is Defender for Cloud Apps?](https://learn.microsoft.com/en-us/microsoft-365/security/defender-cloud-apps/what-is-microsoft-defender-for-cloud-apps?view=o365-worldwide) |
| **Microsoft Entra ID Protection**    | Microsoft Entra ID Protection evaluates risk data from billions of sign-in attempts and uses this data to evaluate the risk of each sign-in to your environment. This data is used by Microsoft Entra ID to allow or prevent account access, depending on how Conditional Access policies are configured. Microsoft Entra ID Protection is licensed separately from Microsoft Defender XDR. It is included with Microsoft Entra ID P2. | [What is Identity Protection?](https://learn.microsoft.com/en-us/azure/active-directory/identity-protection/overview) |

## Microsoft Defender XDR architecture

The diagram below illustrates high-level architecture for key Microsoft Defender XDR components and integrations. Detailed architecture for each Defender component, and use-case scenarios, are given throughout this series of articles.

![image](https://github.com/user-attachments/assets/6129965b-655c-4c8a-8059-71ca4aaadd0e)

In this illustration:

1) Microsoft Defender XDR combines the signals from all of the Defender components to provide extended detection and response (XDR) across domains. This includes a unified incident queue, automated response to stop attacks, self-healing (for compromised devices, user identities, and mailboxes), cross-threat hunting, and threat analytics.

2) Microsoft Defender for Collaboration safeguards your organization against malicious threats posed by email messages, links (URLs), and collaboration tools. It shares signals resulting from these activities with Microsoft Defender XDR. Exchange Online Protection (EOP) is integrated to provide end-to-end protection for incoming email and attachments.

3) Microsoft Defender for Identity gathers signals from servers running Active Directory Federated Services (AD FS) and on-premises Active Directory Domain Services (AD DS). It uses these signals to protect your hybrid identity environment, including protecting against hackers that use compromised accounts to move laterally across workstations in the on-premises environment.

4) Microsoft Defender for Endpoint gathers signals from and protects devices used by your organization.

5) Microsoft Defender for Cloud Apps gathers signals from your organization's use of cloud apps and protects data flowing between your environment and these apps, including both sanctioned and unsanctioned cloud apps.

6) Microsoft Entra ID Protection evaluates risk data from billions of sign-in attempts and uses this data to evaluate the risk of each sign-in to your environment. This data is used by Microsoft Entra ID to allow or prevent account access, depending on how Conditional Access policies are configured. Microsoft Entra ID Protection is licensed separately from Microsoft Defender XDR. It is included with Microsoft Entra ID P2.
