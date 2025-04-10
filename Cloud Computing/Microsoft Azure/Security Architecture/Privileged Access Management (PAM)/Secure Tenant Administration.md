# Secure Tenant Administration

This unit will look at the following perspectives on secure tenant administration:

1) Azure tenant administration with Azure Lighthouse

2) Principles for Microsoft 365 tenant administration

# Azure tenant management with Azure Lighthouse

Azure Lighthouse enables multi-tenant management with scalability, higher automation, and enhanced governance across resources.

With Azure Lighthouse, service providers can deliver managed services using comprehensive and robust tooling built into the Azure platform. Customers maintain control over who has access to their tenant, which resources they can access, and what actions can be taken. Enterprise organizations managing resources across multiple tenants can use Azure Lighthouse to streamline management tasks.

Cross-tenant management experiences let you work more efficiently with Azure services such as Azure Policy, Microsoft Sentinel, Azure Arc, and many more. Users can see what changes were made and by whom in the activity log, which is stored in the customer's tenant and can be viewed by users in the managing tenant.

![image](https://github.com/user-attachments/assets/5465ac6f-5402-4112-9b8b-4680037abb5e)

### Benefits

Azure Lighthouse helps service providers efficiently build and deliver managed services. Benefits include:

1) Management at scale: Customer engagement and life-cycle operations to manage customer resources are easier and more scalable. Existing APIs, management tools, and workflows can be used with delegated resources, including machines hosted outside of Azure, regardless of the regions in which they're located.

2) Greater visibility and control for customers: Customers have precise control over the scopes they delegate and the permissions that are allowed. They can audit service provider actions and remove access completely at any time.

3) Comprehensive and unified platform tooling: Azure Lighthouse works with existing tools and APIs, Azure managed applications, and partner programs like the Cloud Solution Provider program (CSP). This flexibility supports key service provider scenarios, including multiple licensing models such as EA, CSP and pay-as-you-go. You can integrate Azure Lighthouse into your existing workflows and applications, and track your impact on customer engagements by linking your partner ID.

### Capabilities

Azure Lighthouse includes multiple ways to help streamline engagement and management:

1) Azure delegated resource management: Manage your customers' Azure resources securely from within your own tenant, without having to switch context and control planes. Customer subscriptions and resource groups can be delegated to specified users and roles in the managing tenant, with the ability to remove access as needed.

2) New Azure portal experiences: View cross-tenant information in the My customers page in the Azure portal. A corresponding Service providers page lets customers view and manage their service provider access.

3) Azure Resource Manager templates: Use ARM templates to onboard delegated customer resources and perform cross-tenant management tasks.

4) Managed Service offers in Azure Marketplace: Offer your services to customers through private or public offers, and automatically onboard them to Azure Lighthouse.

# Microsoft 365 tenant management

A Microsoft 365 tenant is a dedicated instance of the services of Microsoft 365 and your organization data stored within a specific default location, such as Europe or North America. This location is specified when you create the tenant for your organization. Each Microsoft 365 tenant is distinct, unique, and separate from all other Microsoft 365 tenants. You create a Microsoft 365 tenant when you purchase one or more products from Microsoft, such as Microsoft 365 E3 or E5, and a set of licenses for each.

Your Microsoft 365 tenant also includes a Microsoft Entra tenant, which is a dedicated instance of Microsoft Entra ID for user accounts, groups, and other objects. Each Microsoft Entra tenant is distinct, unique, and separate from all other Microsoft Entra tenants. While your organization can have multiple Microsoft Entra tenants that you can set up with Azure subscriptions, Microsoft 365 tenants can only use a single Microsoft Entra tenant, the one that was created when you created the tenant.

Here is an example:

![image](https://github.com/user-attachments/assets/ed64dfc4-f680-4253-bd72-5162028740a5)

Tenant management is the planning, deployment, and ongoing operation of your Microsoft 365 tenants.

## Attributes of a well-designed and operating tenant

Beyond the correct name and location for your tenant, there are additional elements to plan, deploy, and manage to ensure that your user experiences with cloud productivity apps—such as Microsoft Teams and Exchange Online—are effective, secure, and performant.

Here are the elements:

1) You have the correct set of products (subscriptions) and licenses.

 - The set of products match your business, IT, and security needs.

 - There is an adequate number of licenses for your workers and anticipated changes in staffing.

2) For networking:

 - You have configured the correct DNS domain names.

 - For enterprise networks, you have optimized network traffic to the Microsoft network for onsite workers.

 - You have optimized network traffic for remote workers who are using a VPN client.

3) You have synchronized your Active Directory Domain Services (AD DS) accounts, groups, and other objects.

 - Your Microsoft Entra tenant accounts are mapped to Exchange Online mailboxes with the correct DNS domains for email addresses.

 - Your user accounts have been assigned the correct licenses from the correct purchased products (such as Microsoft 365 E3 or E5).

4) You have configured strong identity and access management.

 - You are requiring secure user sign-in with passwordless or multi-factor authentication (MFA).

 - You have Conditional Access policies that enforce sign-in requirements and restrictions for higher levels of security.

5) On-premises Office servers and their data have been migrated to cloud apps or are being used in a hybrid configuration.

6) You are doing device management with Intune or Basic Mobility and Security built into Microsoft 365.

 - Your organization-owned devices are enrolled and managed.

 - The apps for personal devices are managed.

Here is an example of a Microsoft 365 tenant with all these elements in place.

![image](https://github.com/user-attachments/assets/76b1e41c-8ca5-47c8-9da5-07ce958d9663)

In this illustration, the Microsoft 365 tenant includes:

1) Products and licenses for Microsoft 365 E3 and E5.

2) Microsoft 365 productivity apps.

3) Intune with enrolled devices and device and application policies.

4) A Microsoft Entra tenant that has synchronized user account (groups and other directory objects are not shown), domains, and Conditional Access policies.
