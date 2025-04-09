# Design modern authentication and authorization strategies

This unit addresses a few specific strategies for modern authentication:

1) Conditional access

2) Continuous access evaluation

3) Threat intelligence integration

4) Risk scoring

## Conditional Access

Users can access your organization's resources by using various devices and apps from anywhere. As an IT admin, you want to make sure that these devices meet your standards for security and compliance. Just focusing on who can access a resource isn't sufficient anymore.

To balance security and productivity, you need to think about how a resource is accessed before you can make a decision about access control. With Microsoft Entra Conditional Access, you can address this requirement. With Conditional Access, you can make automated access control decisions based on conditions for accessing your cloud apps.

Best practice: Manage and control access to corporate resources.

Detail: Configure common Microsoft Entra Conditional Access policies based on a group, location, and application sensitivity for SaaS apps and Microsoft Entra ID–connected apps.

Best practice: Block legacy authentication protocols.

Detail: Attackers exploit weaknesses in older protocols every day, particularly for password spray attacks. Configure Conditional Access to block legacy protocols.

## Continuous access evaluation

Token expiration and refresh are a standard mechanism in the industry. When a client application like Outlook connects to a service like Exchange Online, the API requests are authorized using OAuth 2.0 access tokens. By default, access tokens are valid for one hour, when they expire the client is redirected to Microsoft Entra ID to refresh them. That refresh period provides an opportunity to reevaluate policies for user access. For example: we might choose not to refresh the token because of a Conditional Access policy, or because the user has been disabled in the directory.

Customers have expressed concerns about the lag between when conditions change for a user, and when policy changes are enforced. Microsoft Entra ID has experimented with the "blunt object" approach of reduced token lifetimes but found they can degrade user experiences and reliability without eliminating risks.

Timely response to policy violations or security issues really requires a "conversation" between the token issuer (Microsoft Entra ID), and the relying party (enlightened app). This two-way conversation gives us two important capabilities. The relying party can see when properties change, like network location, and tell the token issuer. It also gives the token issuer a way to tell the relying party to stop respecting tokens for a given user because of account compromise, disablement, or other concerns. The mechanism for this conversation is continuous access evaluation (CAE). The goal for critical event evaluation is for response to be near real time, but latency of up to 15 minutes may be observed because of event propagation time; however, IP locations policy enforcement is instant.

The initial implementation of continuous access evaluation focuses on Exchange, Teams, and SharePoint Online.

Continuous access evaluation is available in Azure Government tenants (GCC High and DOD) for Exchange Online.

#### Key Benefits

1) User termination or password change/reset: User session revocation is enforced in near real time.

2) Network location change: Conditional Access location policies are enforced in near real time.

3) Token export to a machine outside of a trusted network can be prevented with Conditional Access location policies.

## Scenarios

There are two scenarios that make up continuous access evaluation, critical event evaluation and Conditional Access policy evaluation.

### Critical event evaluation

Continuous access evaluation is implemented by enabling services, like Exchange Online, SharePoint Online, and Teams, to subscribe to critical Microsoft Entra events. Those events can then be evaluated and enforced near real time. Critical event evaluation doesn't rely on Conditional Access policies so it's available in any tenant. The following events are currently evaluated:

1) User Account is deleted or disabled

2) Password for a user is changed or reset

3) Multifactor Authentication is enabled for the user

4) Administrator explicitly revokes all refresh tokens for a user

5) High user risk detected by Microsoft Entra ID Protection

This process enables the scenario where users lose access to organizational SharePoint Online files, email, calendar, or tasks, and Teams from Microsoft 365 client apps within minutes after a critical event.

### Conditional Access policy evaluation

Exchange Online, SharePoint Online, Teams, and MS Graph can synchronize key Conditional Access policies for evaluation within the service itself.

This process enables the scenario where users lose access to organizational files, email, calendar, or tasks from Microsoft 365 client apps or SharePoint Online immediately after network location changes.

## Microsoft Entra Identity Protection

Identity Protection allows organizations to accomplish three key tasks:

1) Automate the detection and remediation of identity-based risks.

2) Investigate risks using data in the portal.

3) Export risk detection data to other tools.

![image](https://github.com/user-attachments/assets/e7ce4a24-3ca0-49b3-8403-18bbd6652416)

Identity Protection uses the learnings Microsoft has acquired from their position in organizations with Microsoft Entra ID, the consumer space with Microsoft Accounts, and in gaming with Xbox to protect your users. Microsoft analyses trillions of signals per day to identify and protect customers from threats.

The signals generated by and fed to Identity Protection, can be further fed into tools like Conditional Access to make access decisions, or fed back to a security information and event management (SIEM) tool for further investigation.

### Detect risk

Identity Protection detects risks of many types, including:

Anonymous IP address use

Atypical travel

Malware linked IP address

Unfamiliar sign-in properties

Leaked credentials

Password spray

and more...

The risk signals can trigger remediation efforts such as requiring: perform multifactor authentication, reset their password using self-service password reset, or block access until an administrator takes action.

### Investigate risk
Administrators can review detections and take manual action on them if needed. There are three key reports that administrators use for investigations in Identity Protection:

Risky users

Risky sign-ins

Risk detections

#### Risk levels

Identity Protection categorizes risk into tiers: low, medium, and high.

Microsoft doesn't provide specific details about how risk is calculated. Each level of risk brings higher confidence that the user or sign-in is compromised. For example, something like one instance of unfamiliar sign-in properties for a user might not be as threatening as leaked credentials for another user.

##### NOTE: Risk-based policies can be created in Identity protection as well, but it is recommended to do so with Conditional Access policies.

## Risk-based conditional access policies

Access control policies can be applied to protect organizations when a sign-in or user is detected to be at risk. Such policies are called risk-based policies.

Microsoft Entra Conditional Access offers two risk conditions: Sign-in risk and User risk. Organizations can create risk-based Conditional Access policies by configuring these two risk conditions and choosing an access control method. During each sign-in, Identity Protection sends the detected risk levels to Conditional Access, and the risk-based policies apply if the policy conditions are satisfied.

![image](https://github.com/user-attachments/assets/afaeca1f-89bb-4484-97e7-69e1b6f66a7a)

The following diagram shows an example of enforcing a policy that requires multifactor authentication when the sign-in risk level is medium or high.

![image](https://github.com/user-attachments/assets/517ef050-eaf9-42cb-ae0a-f5c85624732e)

The example above also demonstrates a main benefit of a risk-based policy: automatic risk remediation. When a user successfully completes the required access control, like a secure password change, their risk is remediated. That sign-in session and user account isn't at risk, and no action is needed from the administrator.

Allowing users to self-remediate using this process reduces the risk investigation and remediation burden on the administrators while protecting your organizations from security compromises. More information about risk remediation can be found in the article, Remediate risks and unblock users.

### Sign-in risk-based Conditional Access policy

During each sign-in, Identity Protection analyzes hundreds of signals in real-time and calculates a sign-in risk level that represents the probability that the given authentication request isn't authorized. This risk level then gets sent to Conditional Access, where the organization's configured policies are evaluated. Administrators can configure sign-in risk-based Conditional Access policies to enforce access controls based on sign-in risk, including requirements such as:

1) Block access

2) Allow access

3) Require multifactor authentication

### User risk-based Conditional Access policy

Identity Protection analyzes signals about user accounts and calculates a risk score based on the probability that the user has been compromised. If a user has risky sign-in behavior, or their credentials have been leaked, Identity Protection uses these signals to calculate the user risk level. Administrators can configure user risk-based Conditional Access policies to enforce access controls based on user risk, including requirements such as:

1) Block access

2) Allow access but require a secure password change.

A secure password change remediates the user risk and close the risky user event to prevent unnecessary noise for administrators.

## Protected actions

Protected actions in Microsoft Entra ID are permissions that have been assigned Conditional Access policies. When a user attempts to perform a protected action, they must first satisfy the Conditional Access policies assigned to the required permissions. For example, to allow administrators to update Conditional Access policies, you can require that they first satisfy the Phishing-resistant MFA policy.

### Why use protected actions?

You use protected actions when you want to add an additional layer of protection. Protected actions can be applied to permissions that require strong Conditional Access policy protection, independent of the role being used or how the user was given the permission. Because the policy enforcement occurs at the time the user attempts to perform the protected action and not during user sign-in or rule activation, users are prompted only when needed.

### What policies are typically used with protected actions?

We recommend using multifactor authentication on all accounts, especially accounts with privileged roles. Protected actions can be used to require additional security. Here are some common stronger Conditional Access policies.

1) Stronger MFA authentication strengths, such as Passwordless MFA or Phishing-resistant MFA,

2) Privileged access workstations, by using Conditional Access policy device filters.

3) Shorter session timeouts, by using Conditional Access sign-in frequency session controls.

### What permissions can be used with protected actions?

Conditional Access policies can be applied to limited set of permissions. You can use protected actions in the following areas:

1) Conditional Access policy management

2) Cross-tenant access settings management

3) Custom rules that define network locations

4) Protected action management
