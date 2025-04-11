# Deploying Zero Trust for Microsoft 365

Microsoft 365 is built intentionally with many security and information protection capabilities to help you build Zero Trust into your environment. Many of the capabilities can be extended to protect access to other SaaS apps your organization uses and the data within these apps.

This illustration represents the work of deploying Zero Trust capabilities. This work is broken into units of work that can be configured together, starting from the bottom and working to the top to ensure that prerequisite work is complete.

![image](https://github.com/user-attachments/assets/e6a4e51a-4705-4e8d-843d-3d148e77aa8e)

In this illustration:

1) Zero Trust begins with a foundation of identity and device protection.

2) Threat protection capabilities are built on top of this foundation to provide real-time monitoring and remediation of security threats.

3) Information protection and governance provide sophisticated controls targeted at specific types of data to protect your most valuable information and to help you comply with compliance standards, including protecting personal information.

This article assumes you have already configured cloud identity. If you need guidance for this objective, see Deploy your identity infrastructure for Microsoft 365.

## Step 1: Configure Zero Trust identity and device access protection — starting-point policies

The first step is to build your Zero Trust foundation by configuring identity and device access protection.

![image](https://github.com/user-attachments/assets/d07568fe-6320-474f-b5c6-2d9671310b7b)

Go to Zero Trust identity and device access protection for prescriptive guidance to accomplish this. This series of articles describes a set of identity and device access prerequisite configurations and a set of Microsoft Entra Conditional Access, Microsoft Intune, and other policies to secure access to Microsoft 365 for enterprise cloud apps and services, other SaaS services, and on-premises applications published with Microsoft Entra application proxy.

Device enrollment for policies that require managed devices. See Step 2. Manage endpoints with Intune to enroll devices.

Start by implementing the starting-point tier. These policies do not require enrolling devices into management.

![image](https://github.com/user-attachments/assets/ad79f90b-202f-4205-aaae-5d63757e8330)

## Step 2: Manage endpoints with Intune

Next, enroll your devices into management and begin protecting these with more sophisticated controls.

![image](https://github.com/user-attachments/assets/8d949ba8-cf98-4c65-988a-fd8f7bf4b146)

## Step 3: Add Zero Trust identity and device access protection — Enterprise policies

With devices enrolled into management, you can now implement the full set of recommended Zero Trust identity and device access policies, requiring compliant devices.

![image](https://github.com/user-attachments/assets/628ea455-0542-40b4-a700-7e63ff9b4f16)

Return to Common identity and device access policies and add the policies in the Enterprise tier.

![image](https://github.com/user-attachments/assets/dc5fd2a5-2913-4b7d-9b27-250c11e2fe4e)

## Step 4: Evaluate, pilot, and deploy Microsoft Defender XDR

Microsoft Defender XDR is an extended detection and response (XDR) solution that automatically collects, correlates, and analyzes signal, threat, and alert data from across your Microsoft 365 environment, including endpoint, email, applications, and identities.

![image](https://github.com/user-attachments/assets/bad64540-21ee-4ace-a4ae-8ecc226016be)

## Step 5: Protect and govern sensitive data

Implement Microsoft Purview Information Protection to help you discover, classify, and protect sensitive information wherever it lives or travels.

Microsoft Purview Information Protection capabilities are included with Microsoft Purview and give you the tools to know your data, protect your data, and prevent data loss.

![image](https://github.com/user-attachments/assets/e5ab83f4-9ffd-4253-8cad-e2874168fbc4)

While this work is represented at the top of the deployment stack illustrated earlier in this article, you can begin this work anytime.

Microsoft Purview Information Protection provides a framework, process, and capabilities you can use to accomplish your specific business objectives.

![image](https://github.com/user-attachments/assets/f030003c-e179-4ef0-b703-36a40f29270e)

If you're deploying information protection for data privacy regulations, this solution guide provides a recommended framework for the entire process: Deploy information protection for data privacy regulations with Microsoft 365.

