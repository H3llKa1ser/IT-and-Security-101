# Align conditional access and Zero Trust

We'll start out with some design principles.

## Conditional Access as a Zero Trust policy engine

The Microsoft approach to Zero Trust includes Conditional Access as the main policy engine. Here's an overview of that approach:

![image](https://github.com/user-attachments/assets/1e57e33f-d07a-4e34-9b74-793ca914c43a)

Conditional Access is used as the policy engine for a Zero Trust architecture that covers both policy definition and policy enforcement. Based on various signals or conditions, Conditional Access can block or give limited access to resources, as shown here:

![image](https://github.com/user-attachments/assets/cab41806-ee97-4302-a6eb-634a7a076892)

Here's a more detailed view of the elements of Conditional Access and what it covers:

![image](https://github.com/user-attachments/assets/554ae0bb-fbd5-4f36-bd5b-3017c66e4c02)

This diagram shows Conditional Access and related elements that can help protect user access to resources, as opposed to non-interactive or non-human access. The following diagram describes both types of identities:

![image](https://github.com/user-attachments/assets/0fdaa5e8-61e1-4d4e-b340-5f4e645788c0)

Non-human access to resources must also be protected. Currently, you can't use Conditional Access to protect non-human access to cloud resources. You need to use another method, like grant controls for OAuth-based access.

## Principles of Conditional Access vs Principles of Zero Trust

Based on the preceding information, here's a summary of suggested principles. Microsoft recommends that you create an access model based on Conditional Access that's aligned with the three main Microsoft Zero Trust principles:

| **Zero Trust Principle**        | **Conditional Access Principle**                                                                                                                                                                                                                 |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Verify explicitly**          | - Move the control plane to the cloud. <br> - Integrate apps with Microsoft Entra ID and protect them using Conditional Access. <br> - Consider all clients to be external.                                                                       |
| **Use least privileged access**| - Evaluate access based on compliance and risk (user, sign-in, device risk). <br> - Use these access priorities: <br> &nbsp;&nbsp;• Direct access with Conditional Access protection <br> &nbsp;&nbsp;• Microsoft Entra app proxy <br> &nbsp;&nbsp;• Conditional Access–based VPN with app/DNS restriction. |
| **Assume breach**              | - Segment network infrastructure. <br> - Minimize use of enterprise PKI. <br> - Migrate SSO from AD FS to PHS. <br> - Reduce dependency on DCs via Kerberos KDC in Entra ID. <br> - Manage devices with Microsoft Endpoint Manager; move management to the cloud. |

Here are some more detailed principles and recommended practices for Conditional Access:

Apply Zero Trust principles to Conditional Access.

Use report-only mode before putting a policy into production.

Test both positive and negative scenarios.

Use change and revision control on Conditional Access policies.

Automate the management of Conditional Access policies by using tools like Azure DevOps / GitHub or Azure Logic Apps.

Use block mode for general access only if and where you need to.

Ensure that all applications and your platform are protected. Conditional Access has no implicit "deny all."

Protect privileged users in all Microsoft 365 role-based access control (RBAC) systems.

Require password change and multi-factor authentication for high-risk users and sign-ins (enforced by sign-in frequency).

Restrict access from high-risk devices. Use an Intune compliance policy with a compliance check in Conditional Access.

Protect privileged systems, like access to the administrator portals for Office 365, Azure, AWS, and Google Cloud.

Prevent persistent browser sessions for admins and on untrusted devices.

Block legacy authentication.

Restrict access from unknown or unsupported device platforms.

Require compliant device for access to resources, when possible.

Restrict strong credential registration.

Consider using default session policy that allows sessions to continue if there's an outage, if the appropriate conditions were satisfied before the outage.

