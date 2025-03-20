# Configure access control for storage accounts

Requests for a secured resource in the Blob, File, Queue, or Table service must be authorized. Authorization ensures that resources in your storage account are accessible only when you want them to be, and only to those users or applications to whom you grant access.

The following table describes the options that Azure Storage offers for authorizing access to resources:

| Azure Artifact | Shared Key (storage account key) | Shared Access Signature (SAS) | Microsoft Entra ID | On-premises Active Directory Domain Services | Anonymous Public Read Access |
|----------------|---------------------------------|---------------------------------|--------------------|---------------------------------------------|----------------------------|
| **Azure Blobs** | Supported | Supported | Supported | Not supported | Supported |
| **Azure Files (SMB)** | Supported | Not supported | Supported with Microsoft Entra Domain Services or Microsoft Entra Kerberos | Supported, credentials must be synced to Microsoft Entra ID | Not supported |
| **Azure Files (REST)** | Supported | Supported | Supported | Not supported | Not supported |
| **Azure Queues** | Supported | Supported | Supported | Not supported | Not supported |
| **Azure Tables** | Supported | Supported | Supported | Not supported | Not supported |

Each authorization option is briefly described below:

1) Microsoft Entra ID: Microsoft Entra is Microsoft's cloud-based identity and access management service. Microsoft Entra ID integration is available for the Blob, File, Queue and Table services. With Microsoft Entra ID, you can assign fine-grained access to users, groups, or applications via role-based access control (RBAC).

2) Microsoft Entra Domain Services authorization for Azure Files. Azure Files supports identity-based authorization over Server Message Block (SMB) through Microsoft Entra Domain Services. You can use RBAC for fine-grained control over a client's access to Azure Files resources in a storage account.

3) Active Directory (AD) authorization for Azure Files. Azure Files supports identity-based authorization over SMB through AD. Your AD domain service can be hosted on on-premises machines or in Azure VMs. SMB access to Files is supported using AD credentials from domain joined machines, either on-premises or in Azure. You can use RBAC for share level access control and NTFS DACLs for directory and file level permission enforcement.

4) Shared Key: Shared Key authorization relies on your account access keys and other parameters to produce an encrypted signature string that is passed on the request in the Authorization header.

5) Shared access signatures: Shared access signatures (SAS) delegate access to a particular resource in your account with specified permissions and over a specified time interval.

6) Anonymous access to containers and blobs: You can optionally make blob resources public at the container or blob level. A public container or blob is accessible to any user for anonymous read access. Read requests to public containers and blobs do not require authorization.

Authenticating and authorizing access to blob, file, queue and table data with Microsoft Entra ID provides superior security and ease of use over other authorization options. For example, by using Microsoft Entra ID, you avoid having to store your account access key with your code, as you do with Shared Key authorization. While you can continue to use Shared Key authorization with your blob and queue applications, Microsoft recommends moving to Microsoft Entra ID where possible.

Similarly, you can continue to use shared access signatures (SAS) to grant fine-grained access to resources in your storage account, but Microsoft Entra ID offers similar capabilities without the need to manage SAS tokens or worry about revoking a compromised SAS.

# Manage life cycle for storage account access keys

When you create a storage account, Azure generates two 512-bit storage account access keys for that account. These keys can be used to authorize access to data in your storage account via Shared Key authorization, or via SAS tokens that are signed with the shared key.

Microsoft recommends that you use Azure Key Vault to manage your access keys, and that you regularly rotate and regenerate your keys. Using Azure Key Vault makes it easy to rotate your keys without interruption to your applications. You can also manually rotate your keys.

## Protect your access keys

Storage account access keys provide full access to the configuration of a storage account, as well as the data. Always be careful to protect your access keys. Use Azure Key Vault to manage and rotate your keys securely. Access to the shared key grants a user full access to a storage account’s configuration and its data. Access to shared keys should be carefully limited and monitored. Use shared access signature (SAS) tokens with limited scope of access in scenarios where Microsoft Entra ID based authorization can't be used. Avoid hard-coding access keys or saving them anywhere in plain text that is accessible to others. Rotate your keys if you believe they might have been compromised.

Microsoft recommends using Microsoft Entra ID to authorize requests against blob, queue, and table data if possible, rather than using the account keys (Shared Key authorization). Authorization with Microsoft Entra ID provides superior security and ease of use over Shared Key authorization. For Server Message Block (SMB) Azure file shares, Microsoft recommends using on-premises Active Directory Domain Services (AD DS) integration or Microsoft Entra Kerberos authentication.

To prevent users from accessing data in your storage account with Shared Key, you can disallow Shared Key authorization for the storage account. Granular access to data with least privileges necessary is recommended as a security best practice. Microsoft Entra ID based authorization should be used for scenarios that support OAuth. Kerberos or SMTP should be used for Azure Files over SMB. For Azure Files over REST, SAS tokens can be used. Shared key access should be disabled if not required to prevent its inadvertent use.

To protect an Azure Storage account with Microsoft Entra Conditional Access policies, you must disallow Shared Key authorization for the storage account.

If you have disabled shared key access and you are seeing Shared Key authorization reported in the diagnostic logs, this indicates that trusted access is being used to access storage.

