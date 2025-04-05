# Zero Trust Technology Pillars

For a more comprehensive guide on rolling out Zero Trust, the deployment plans provide in-depth guidance.

Unlike the checklist format of the RaMP, deployment solutions weave together resources across products and services.

Work is broken into units of work that can be configured together, helping you create a good foundation that you can build up from.

## Visibility, automation, and orchestration with Zero Trust

With each of the other technical pillars of Zero Trust generating their own relevant alerts, we need an integrated capability to manage the resulting influx of data to better defend against threats and validate trust in a transaction.

If an investigation results in actionable learnings, you can take remediation steps. For example, if an investigation uncovers gaps in a zero trust deployment, policies can be modified to address these gaps and prevent future unwanted incidents. Whenever possible it is desirable to automate remediation steps, because it reduces the time it takes for a SOC analyst to address the threat and move onto the next incident.

### Visibility, automation, and orchestration Zero Trust deployment objectives

When implementing an end-to-end Zero Trust framework for visibility, automation, and orchestration, we recommend you focus first on these initial deployment objectives:

I. Establish visibility.
II. Enable automation.

After these are completed, focus on these additional deployment objectives:

III. Enable additional protection and detection controls.

## Securing identity with Zero Trust

Before an identity attempts to access a resource, organizations must:

1) Verify the identity with strong authentication.

2) Ensure access is compliant and typical for that identity.

3) Follows least privilege access principles.

Once the identity has been verified, we can control that identity's access to resources based on organization policies, on-going risk analysis, and other tools.

### Identity Zero Trust deployment objectives

When implementing an end-to-end Zero Trust framework for identity, we recommend you focus first on these initial deployment objectives:

I. Cloud identity federates with on-premises identity systems.
II. Conditional Access policies gate access and provide remediation activities.
III. Analytics improve visibility.

After these are completed, focus on these additional deployment objectives:

IV. Identities and access privileges are managed with identity governance.
V. User, device, location, and behavior is analyzed in real time to determine risk and deliver ongoing protection.
VI. Integrate threat signals from other security solutions to improve detection, protection, and response.

## Applications

To get the full benefit of cloud apps and services, organizations must find the right balance of providing access while maintaining control to protect critical data accessed via applications and APIs.

The Zero Trust model helps organizations ensure that apps, and the data they contain, are protected by:

1) Applying controls and technologies to discover Shadow IT.

2) Ensuring appropriate in-app permissions.

3) Limiting access based on real-time analytics.

4) Monitoring for abnormal behavior.

5) Controlling user actions.

6) Validating secure configuration options.

### Applications Zero Trust deployment objectives

Before most organizations start the Zero Trust journey, their on-premises apps are accessed through physical networks or VPN, and some critical cloud apps are accessible to users.

When implementing a Zero Trust approach to managing and monitoring applications, we recommend you focus first on these initial deployment objectives:

I. Gain visibility into the activities and data in your applications by connecting them via APIs.
II. Discover and control the use of shadow IT.
III. Protect sensitive information and activities automatically by implementing policies.

After these are completed, focus on these additional deployment objectives:

IV. Deploy adaptive access and session controls for all apps.
V. Strengthen protection against cyber threats and rogue apps.
VI. Assess the security posture of your cloud environments

## Secure data with Zero Trust

The three core elements of a data protection strategy are:

1) Know your data - If you don't know what sensitive data you have on-premises and in cloud services, you can't adequately protect it. You need to discover data across your entire organization and classify all data by sensitivity level.

2) Protect your data and prevent data loss - Sensitive data needs to be protected by data protection policies that label and encrypt data or block over-sharing. This ensures only authorized users are able to access the data, even when data travels outside of your corporate environment.

3) Monitor and remediate - You should continuously monitor sensitive data to detect policy violations and risky user behavior. This allows you to take appropriate action, such as revoking access, blocking users, and refining your protection policies.

### Data Zero Trust deployment objectives

An information protection strategy needs to encompass your organization's entire digital content. As a baseline, you need to define labels, discover sensitive data, and monitor the use of labels and actions across your environment. Use of sensitivity labels is discussed at the end of this guide.

When implementing an end-to-end Zero Trust framework for data, we recommend you focus first on these initial deployment objectives:

I. Access decisions are governed by encryption.
II. Data is automatically classified and labeled.

After these are completed, focus on these additional deployment objectives:

III. Classification is augmented by smart machine learning models.
IV. Access decisions are governed by a cloud security policy engine.
V. Prevent data leakage through DLP policies based on a sensitivity label and content inspection.

## Secure endpoints with Zero Trust

Zero Trust adheres to the principle, "Never trust, always verify." In terms of endpoints, that means always verify all endpoints. That includes not only contractor, partner, and guest devices, but also apps and devices used by employees to access work data, regardless of device ownership.

In a Zero Trust approach, the same security policies are applied regardless of whether the device is corporate-owned or personally-owned through bring your own device (BYOD); whether the device is fully managed by IT, or only the apps and data are secured. The policies apply to all endpoints, whether PC, Mac, smartphone, tablet, wearable, or IoT device wherever they are connected, be it the secure corporate network, home broadband, or public internet.

### Endpoint Zero Trust deployment objectives

When implementing an end-to-end Zero Trust framework for securing endpoints, we recommend you focus first on these initial deployment objectives:

I. Endpoints are registered with cloud identity providers. In order to monitor security and risk across multiple endpoints used by any one person, you need visibility in all devices and access points that may be accessing your resources.

II. Access is only granted to cloud-managed and compliant endpoints and apps. Set compliance rules to ensure that devices meet minimum security requirements before access is granted. Also, set remediation rules for noncompliant devices so that people know how to resolve the issue.

III. Data loss prevention (DLP) policies are enforced for corporate devices and BYOD. Control what the user can do with the data after they have access. For instance, restrict file saving to untrusted locations (such as local disk), or restrict copy-and-paste sharing with a consumer communication app or chat app to protect data.

After these are completed, focus on these additional deployment objectives:

IV. Endpoint threat detection is used to monitor device risk. Use a single pane of glass to manage all endpoints in a consistent way, and use a SIEM to route endpoint logs and transactions such that you get fewer, but actionable, alerts.

V. Access control is gated on endpoint risk for both corporate devices and BYOD. Integrate data from Microsoft Defender for Endpoint, or other Mobile Threat Defense (MTD) vendors, as an information source for device compliance policies and device Conditional Access rules. The device risk will then directly influence what resources will be accessible by the user of that device.

## Secure infrastructure with Zero Trust

Azure Blueprints, Azure Policies, Microsoft Defender for Cloud, Microsoft Sentinel, and Azure Sphere can greatly contribute to improving the security of your deployed infrastructure and enable a different approach to defining, designing, provisioning, deploying, and monitoring your infrastructure.

### Infrastructure Zero Trust deployment objectives

When implementing an end-to-end Zero Trust framework for managing and monitoring your infrastructure, we recommend you focus first on these initial deployment objectives:

I. Workloads are monitored and alerted to abnormal behavior.
II. Every workload is assigned an app identity—and configured and deployed consistently.
III. Human access to resources requires Just-In-Time.

After these are completed, focus on these additional deployment objectives:

IV. Unauthorized deployments are blocked, and alert is triggered.
V. Granular visibility and access control are available across workloads.
VI. User and resource access segmented for each workload.

## Secure networks with Zero Trust

Instead of believing everything behind the corporate firewall is safe, an end-to-end Zero Trust strategy assumes breaches are inevitable. That means you must verify each request as if it originates from an uncontrolled network—identity management plays a crucial role in this.

### Network Zero Trust deployment objectives

When implementing an end-to-end Zero Trust framework for securing networks, we recommend you focus first on these initial deployment objectives:

I. Network segmentation: Many ingress/egress cloud micro-perimeters with some micro-segmentation.
II. Threat protection: Cloud native filtering and protection for known threats.
III. Encryption: User-to-app internal traffic is encrypted.

After these are completed, focus on these additional deployment objectives:

IV. Network segmentation: Fully distributed ingress/egress cloud micro-perimeters and deeper micro-segmentation.
V. Threat protection: Machine learning-based threat protection and filtering with context-based signals.
VI. Encryption: All traffic is encrypted.
