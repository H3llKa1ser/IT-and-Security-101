# Evaluate solutions that use Microsoft Entra Internet Access

## Evaluate solutions that use Microsoft Entra Internet Access as a secure web gateway

Microsoft Entra Internet Access provides an identity-centric Secure Web Gateway (SWG) solution for Software as a Service (SaaS) applications and other Internet traffic. It protects users, devices, and data from the Internet's wide threat landscape with best-in-class security controls and visibility through Traffic Logs.

### Web content filtering

The key introductory feature for Microsoft Entra Internet Access for all apps is Web content filtering. This feature provides granular access control for web categories and Fully Qualified Domain Names (FQDNs). By explicitly blocking known inappropriate, malicious, or unsafe sites, you protect your users and their devices from any Internet connection whether they're remote or within the corporate network.

Web content filtering is implemented using filtering policies, which are grouped into security profiles, which can be linked to Conditional Access policies. To learn more about Conditional Access, see Microsoft Entra Conditional Access.

### Security profiles

Security profiles are objects you use to group filtering policies and deliver them through user aware Conditional Access policies. For instance, to block all News websites except for msn.com for user angie@contoso.com you create two web filtering policies and add them to a security profile. You then take the security profile and link it to a Conditional Access policy assigned to angie@contoso.com.

    "Security Profile for Angie"       <---- the security profile
    Allow msn.com at priority 100  <---- higher priority filtering policies
    Block News at priority 200     <---- lower priority filtering policy

### Policy processing logic

Within a security profile, policies are enforced according to priority ordering with 100 being the highest priority and 65,000 being the lowest priority (similar to traditional firewall logic). As a best practice, add spacing of about 100 between priorities to allow for policy flexibility in the future.

Once you link a security profile to a Conditional Access (CA) policy, if multiple CA policies match, both security profiles are processed in priority ordering of the matching security profiles.

## Evaluate solutions that use Microsoft Entra Internet Access to access Microsoft 365, including cross-tenant configurations

Solutions in this area rely on Microsoft Entra Internet Access for Microsoft Traffic. This is essentially a traffic forwarding profile that enables Microsoft Entra Internet Access to acquire traffic going to Microsoft services, including Microsoft 365.

The Microsoft profile manages the following policy groups:

1) Exchange Online

2) SharePoint Online and OneDrive

3) Microsoft 365 Common and Office Online (only Microsoft Entra ID and Microsoft Graph)

# Evaluate solutions that use Microsoft Entra Private Access

Microsoft Entra Private Access unlocks the ability to specify the fully qualified domain names (FQDNs) and IP addresses that you consider private or internal, so you can manage how your organization accesses them. With Private Access, you can modernize how your organization's users access private apps and resources. Remote workers don't need to use a VPN to access these resources if they have the Global Secure Access Client installed. The client quietly and seamlessly connects them to the resources they need.

Private Access provides two ways to configure the private resources that you want to tunnel through the service. You can configure Quick Access, which is the primary group of FQDNs and IP addresses that you want to secure. You can also configure a Global Secure Access app for per-app access, which allows you to specify a subset of private resources that you want to secure. The Global Secure Access app provides a granular approach to securing your private resources.

The features of Microsoft Entra Private Access provide a quick and easy way to replace your VPN to allow secure access to your internal resources with an easy-one time configuration, using the secure capabilities of Conditional Access.

## Quick Access and Global Secure Access apps

When you configure the Quick Access and Global Secure Access apps, you create a new enterprise application. The app serves as a container for the private resources that you want to secure. The application has its own Microsoft Entra private network connector to broker the connection between the service and the internal resource. You can assign users and groups to the app, and then use Conditional Access policies to control access to the app.

Quick Access and Per-app Access are similar, but there are a few key concepts to understand so you can decide how to configure each one.

### Quick Access app

Quick Access is the primary group of FQDNs and IP addresses that you want to secure. As you're planning your Global Secure Access deployment, review your list of private resources and determine which resources you always want to tunnel through the service. This primary group of FQDNs, IP addresses, and IP ranges is what you add to Quick Access.

![image](https://github.com/user-attachments/assets/12409f6b-9675-4c94-845f-9dfa7580f1be)

### Global Secure Access app
A Global Secure Access app could be configured if any of the following scenarios sound familiar:

1) I need to apply a different set of Conditional Access policies to a subset of users.

2) I have a few private resources that I want to secure, but they should have a different set of access policies.

3) I have a subset of private resources that I only want to secure for a specific time frame.

![image](https://github.com/user-attachments/assets/4a540f5d-ba2a-4cd7-90a2-a2d4161a2055)

The Global Secure Access app takes a more detailed approach to securing your private resources. You can create multiple per-app access apps to secure different private resources. Paired with Conditional Access policies, you have a powerful yet fine-grained way to secure your private resources.
