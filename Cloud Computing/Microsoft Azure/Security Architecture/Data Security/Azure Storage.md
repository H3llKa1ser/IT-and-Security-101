# Data protection in Azure Storage

| **Scenario** | **Data protection option** | **Recommendations** | **Protection benefit** | **Available for Data Lake Storage** |
|--------------|-----------------------------|----------------------|-------------------------|--------------------------------------|
| Prevent a storage account from being deleted or modified. | Azure Resource Manager lock | Lock all of your storage accounts with an Azure Resource Manager lock to prevent deletion of the storage account. | Protects the storage account against deletion or configuration changes. Doesn't protect containers or blobs in the account from being deleted or overwritten. | Yes |
| Prevent a blob version from being deleted for an interval that you control. | Immutability policy on a blob version | Set an immutability policy on an individual blob version to protect business-critical documents, for example, in order to meet legal or regulatory compliance requirements. | Protects a blob version from being deleted and its metadata from being overwritten. An overwrite operation creates a new version. If at least one container has version-level immutability enabled, the storage account is also protected from deletion. Container deletion fails if at least one blob exists in the container. | No |
| Prevent a container and its blobs from being deleted or modified for an interval that you control. | Immutability policy on a container | Set an immutability policy on a container to protect business-critical documents, for example, in order to meet legal or regulatory compliance requirements. | Protects a container and its blobs from all deletes and overwrites. When a legal hold or a locked time-based retention policy is in effect, the storage account is also protected from deletion. | Yes |
| Restore a deleted container within a specified interval. | Container soft delete | Enable container soft delete for all storage accounts, with a minimum retention interval of seven days. Enable blob versioning and blob soft delete together with container soft delete to protect individual blobs in a container. | A deleted container and its contents may be restored within the retention period. Only container-level operations (e.g., Delete Container) can be restored. | Yes |
| Automatically save the state of a blob in a previous version when it's overwritten. | Blob versioning | Enable blob versioning, together with container soft delete and blob soft delete, for storage accounts where you need optimal protection for blob data. | Every blob write operation creates a new version. The current version of a blob may be restored from a previous version if the current version is deleted or overwritten. | No |
| Restore a deleted blob or blob version within a specified interval. | Blob soft delete | Enable blob soft delete for all storage accounts, with a minimum retention interval of seven days. Enable blob versioning and container soft delete together with blob soft delete. | A deleted blob or blob version may be restored within the retention period. | Yes |
| Restore a set of block blobs to a previous point in time. | Point-in-time restore | To use point-in-time restore to revert to an earlier state, design your application to delete individual block blobs rather than deleting containers. | A set of block blobs may be reverted to their state at a specific point in the past. Only operations on block blobs are reverted. | No |
| Manually save the state of a blob at a given point in time. | Blob snapshot | Recommended as an alternative to blob versioning when versioning isn't appropriate, or when the storage account has a hierarchical namespace enabled. | A blob may be restored from a snapshot if the blob is overwritten. If the blob is deleted, snapshots are also deleted. | Yes, in preview |
| A blob can be deleted or overwritten, but the data is regularly copied to a second storage account. | Roll-your-own solution for copying data to a second account by using Azure Storage object replication or a tool like AzCopy or Azure Data Factory. | Recommended for peace-of-mind protection against unexpected intentional actions or unpredictable scenarios. Create the second storage account in the same region as the primary to avoid egress charges. | Data can be restored from the second storage account if the primary account is compromised in any way. AzCopy and Azure Data Factory are supported. Object replication isn't supported. | |

# Data encryption in Azure Storage
Azure Storage encryption is enabled for all storage accounts, including both Resource Manager and classic storage accounts. Azure Storage encryption cannot be disabled. Because your data is secured by default, you don't need to modify your code or applications to take advantage of Azure Storage encryption.

Data in a storage account is encrypted regardless of performance tier (standard or premium), access tier (hot or cool), or deployment model (Azure Resource Manager or classic). All new and existing block blobs, append blobs, and page blobs are encrypted, including blobs in the archive tier. All Azure Storage redundancy options support encryption, and all data in both the primary and secondary regions is encrypted when geo-replication is enabled. All Azure Storage resources are encrypted, including blobs, disks, files, queues, and tables. All object metadata is also encrypted.

There is no additional cost for Azure Storage encryption.

## About encryption key management

Data in a new storage account is encrypted with Microsoft-managed keys by default. You can continue to rely on Microsoft-managed keys for the encryption of your data, or you can manage encryption with your own keys. If you choose to manage encryption with your own keys, you have two options. You can use either type of key management, or both:

1) You can specify a customer-managed key to use for encrypting and decrypting data in Blob Storage and in Azure Files.1,2 Customer-managed keys must be stored in Azure Key Vault or Azure Key Vault Managed Hardware Security Model (HSM).

2) You can specify a customer-provided key on Blob Storage operations. A client making a read or write request against Blob Storage can include an encryption key on the request for granular control over how blob data is encrypted and decrypted.

By default, a storage account is encrypted with a key that is scoped to the entire storage account. Encryption scopes enable you to manage encryption with a key that is scoped to a container or an individual blob. You can use encryption scopes to create secure boundaries between data that resides in the same storage account but belongs to different customers. Encryption scopes can use either Microsoft-managed keys or customer-managed keys.

The following table compares key management options for Azure Storage encryption.

| **Key management parameter**      | **Microsoft-managed keys** | **Customer-managed keys**             | **Customer-provided keys**      |
|----------------------------------|-----------------------------|----------------------------------------|----------------------------------|
| Encryption/decryption operations | Azure                       | Azure                                  | Azure                            |
| Azure Storage services supported | All                         | Blob Storage, Azure Files¹ ²          | Blob Storage                     |
| Key storage                      | Microsoft key store         | Azure Key Vault or Key Vault HSM       | Customer's own key store         |
| Key rotation responsibility      | Microsoft                   | Customer                                | Customer                         |
| Key control                      | Microsoft                   | Customer                                | Customer                         |
| Key scope                        | Account (default), container, or blob | Account (default), container, or blob | N/A                              |
