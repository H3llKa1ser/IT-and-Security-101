# Microsoft Entra Identity Protection

Microsoft Entra ID Protection helps organizations detect, investigate, and remediate identity-based risks. These identity-based risks can be further fed into tools like Conditional Access to make access decisions or fed back to a security information and event management (SIEM) tool for further investigation and correlation.

![image](https://github.com/user-attachments/assets/8520084b-9a98-441c-993f-c92e20c10c23)

### Detect risks

Microsoft continually adds and updates detections in our catalog to protect organizations. These detections come from our learnings based on the analysis of trillions of signals each day from Active Directory, Microsoft Accounts, and in gaming with Xbox. This broad range of signals helps Identity Protection detect risky behaviors like:

1) Anonymous IP address usage

2) Password spray attacks

3) Leaked credentials

### Investigate

Any risks detected on an identity are tracked with reporting. Identity Protection provides three key reports for administrators to investigate risks and take action:

1) Risk detections: Each risk detected is reported as a risk detection.

2) Risky sign-ins: A risky sign-in is reported when there are one or more risk detections reported for that sign-in.

3) Risky users: A Risky user is reported when either or both of the following are true:

#### The user has one or more Risky sign-ins.

#### One or more risk detections have been reported.

### Automatic remediation

Risk-based Conditional Access policies can be enabled to require access controls such as providing a strong authentication method, perform multifactor authentication, or perform a secure password reset based on the detected risk level. If the user successfully completes the access control, the risk is automatically remediated.

### Manual remediation

When user remediation isn't enabled, an administrator must manually review them in the reports in the portal, through the API, or in Microsoft 365 Defender. Administrators can perform manual actions to dismiss, confirm safe, or confirm compromise on the risks.

## Making use of the data

Data from Identity Protection can be exported to other tools for archive, further investigation, and correlation. The Microsoft Graph based APIs allow organizations to collect this data for further processing in a tool such as their SIEM.

Organizations might store data for longer periods by changing the diagnostic settings in Microsoft Entra ID. They can choose to send data to a Log Analytics workspace, archive data to a storage account, stream data to Event Hubs, or send data to another solution.

## Required roles

Identity Protection requires users be assigned one or more of the following roles in order to access.

| Role                 | Can do                                                                                           | Can't do                                |
|----------------------|------------------------------------------------------------------------------------------------|-----------------------------------------|
| Security Administrator | Full access to Identity Protection                                                             | Reset password for a user              |
| Security Operator     | View all Identity Protection reports and Overview<br>Dismiss user risk, confirm safe sign-in, confirm compromise<br>Configure alerts | Configure or change policies<br>Reset password for a user |
| Security Reader      | View all Identity Protection reports and Overview                                              | Configure or change policies<br>Reset password for a user<br>Configure alerts<br>Give feedback on detections |
| Global Reader        | Read-only access to Identity Protection                                                         | N/A                                     |
| User Administrator   | Reset user passwords                                                                          | N/A                                     |

Currently, the Security Operator role can't access the Risky sign-ins report.

Conditional Access administrators can create policies that factor in user or sign-in risk as a condition.

## License requirements

Using this feature requires Microsoft Entra ID P2 licenses.

| Capability | Details | Microsoft Entra ID Free / Microsoft 365 Apps | Microsoft Entra ID P1 | Microsoft Entra ID P2 |
|------------|---------|----------------------------------------------|------------------------|------------------------|
| **Risk policies** | Sign-in and user risk policies (via Identity Protection or Conditional Access) | No | No | Yes |
| **Security reports** | Overview | No | No | Yes |
|  | Risky users | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Limited Information. Only users with medium and high risk are shown. No details drawer or risk history. | Full access |
|  | Risky sign-ins | Limited Information. No risk detail or risk level is shown. | Limited Information. No risk detail or risk level is shown. | Full access |
|  | Risk detections | No | Limited Information. No details drawer. | Full access |
| **Notifications** | Users at risk detected alerts | No | No | Yes |
|  | Weekly digest | No | No | Yes |
| **MFA registration policy** |  | No | No | Yes |

