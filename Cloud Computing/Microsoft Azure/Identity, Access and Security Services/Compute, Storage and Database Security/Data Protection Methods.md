# Select and configure appropriate methods for protecting against data security threats, including soft delete, backups, versioning, and immutable storage

Azure Storage provides data protection for Blob Storage and Azure Data Lake Storage Gen2 to help you to prepare for scenarios where you need to recover data that has been deleted or overwritten. It's important to think about how to best protect your data before an incident occurs that could compromise it.

## Recommendations for basic data protection

If you're looking for basic data protection coverage for your storage account and the data that it contains, then Microsoft recommends taking the following steps to begin with:

1) Configure an Azure Resource Manager lock on the storage account to protect the account from deletion or configuration changes.

2) Enable container soft delete for the storage account to recover a deleted container and its contents.

3) Save the state of a blob at regular intervals:

For Blob Storage workloads, enable blob versioning to automatically save the state of your data each time a blob is overwritten.

For Azure Data Lake Storage workloads, take manual snapshots to save the state of your data at a particular point in time.

## Overview of data protection options

The following table summarizes the options available in Azure Storage for common data protection scenarios. Choose the scenarios that are applicable to your situation to learn more about the options available to you. Not all features are available at this time for storage accounts with a hierarchical namespace enabled.

| Scenario | Data Protection Option | Recommendations | Protection Benefit | Available for Data Lake Storage |
|----------|------------------------|-----------------|--------------------|--------------------------------|
| Prevent a storage account from being deleted or modified. | Azure Resource Manager lock | Lock all of your storage accounts with an Azure Resource Manager lock to prevent deletion of the storage account. | Protects the storage account against deletion or configuration changes. Doesn't protect containers or blobs in the account from being deleted or overwritten. | Yes |
| Prevent a blob version from being deleted for an interval that you control. | Immutability policy on a blob version | Set an immutability policy on an individual blob version to protect business-critical documents, for example, in order to meet legal or regulatory compliance requirements. | Protects a blob version from being deleted and its metadata from being overwritten. An overwrite operation creates a new version. If at least one container has version-level immutability enabled, the storage account is also protected from deletion. Container deletion fails if at least one blob exists in the container. | No |
| Prevent a container and its blobs from being deleted or modified for an interval that you control. | Immutability policy on a container | Set an immutability policy on a container to protect business-critical documents, for example, in order to meet legal or regulatory compliance requirements. | Protects a container and its blobs from all deletes and overwrites. When a legal hold or a locked time-based retention policy is in effect, the storage account is also protected from deletion. Containers for which no immutability policy has been set aren't protected from deletion. | Yes |
| Restore a deleted container within a specified interval. | Container soft delete | Enable container soft delete for all storage accounts, with a minimum retention interval of seven days. Enable blob versioning and blob soft delete together with container soft delete to protect individual blobs in a container. Store containers that require different retention periods in separate storage accounts. | A deleted container and its contents may be restored within the retention period. Only container-level operations (for example, Delete Container) can be restored. Container soft delete doesn't enable you to restore an individual blob in the container if that blob is deleted. | Yes |
| Automatically save the state of a blob in a previous version when it's overwritten. | Blob versioning | Enable blob versioning, together with container soft delete and blob soft delete, for storage accounts where you need optimal protection for blob data. Store blob data that doesn't require versioning in a separate account to limit costs. | Every blob write operation creates a new version. The current version of a blob may be restored from a previous version if the current version is deleted or overwritten. | No |
| Restore a deleted blob or blob version within a specified interval. | Blob soft delete | Enable blob soft delete for all storage accounts, with a minimum retention interval of seven days. Enable blob versioning and container soft delete together with blob soft delete for optimal protection of blob data. Store blobs that require different retention periods in separate storage accounts. | A deleted blob or blob version may be restored within the retention period. | Yes |
| Restore a set of block blobs to a previous point in time. | Point-in-time restore | To use point-in-time restore to revert to an earlier state, design your application to delete individual block blobs rather than deleting containers. | A set of block blobs may be reverted to their state at a specific point in the past. Only operations performed on block blobs are reverted. Any operations performed on containers, page blobs, or append blobs aren't reverted. | No |
| Manually save the state of a blob at a given point in time. | Blob snapshot | Recommended as an alternative to blob versioning when versioning isn't appropriate for your scenario, due to cost or other considerations, or when the storage account has a hierarchical namespace enabled. | A blob may be restored from a snapshot if the blob is overwritten. If the blob is deleted, snapshots are also deleted. | Yes, in preview |
| A blob can be deleted or overwritten, but the data is regularly copied to a second storage account. | Roll-your-own solution for copying data to a second account by using Azure Storage object replication or a tool like AzCopy or Azure Data Factory. | Recommended for peace-of-mind protection against unexpected intentional actions or unpredictable scenarios. Create the second storage account in the same region as the primary account to avoid incurring egress charges. | Data can be restored from the second storage account if the primary account is compromised in any way. | AzCopy and Azure Data Factory are supported. Object replication isn't supported. |


## Data protection by resource type

The following table summarizes the Azure Storage data protection options according to the resources they protect.

| Data protection option                                 | Protects an account from deletion | Protects a container from deletion | Protects an object from deletion | Protects an object from overwrites |
|--------------------------------------------------------|----------------------------------|----------------------------------|--------------------------------|--------------------------------|
| Azure Resource Manager lock                            | Yes                              | No                               | No                             | No                             |
| Immutability policy on a blob version                 | Yes                              | Yes                              | Yes                            | Yes                            |
| Immutability policy on a container                    | Yes                              | Yes                              | Yes                            | Yes                            |
| Container soft delete                                  | No                               | Yes                              | No                             | No                             |
| Blob versioning                                       | No                               | No                               | Yes                            | Yes                            |
| Blob soft delete                                      | No                               | No                               | Yes                            | Yes                            |
| Point-in-time restore                                 | No                               | No                               | Yes                            | Yes                            |
| Blob snapshot                                         | No                               | No                               | No                             | Yes                            |
| Roll-your-own solution for copying data to a second account | No                               | Yes                              | Yes                            | Yes                            |

Understanding the nuances of data protection in Azure Storage reveals several operational insights and restrictions:

An Azure Resource Manager lock doesn't protect a container from deletion.

Storage account deletion fails if there is at least one container with version-level immutable storage enabled.

Container deletion fails if at least one blob exists in the container, regardless of whether policy is locked or unlocked.

Overwriting the contents of the current version of the blob creates a new version. An immutability policy protects a version's metadata from being overwritten.

While a legal hold or a locked time-based retention policy is in effect at container scope, the storage account is also protected from deletion.

Not currently supported for Data Lake Storage workloads.

AzCopy and Azure Data Factory are options that are supported for both Blob Storage and Data Lake Storage workloads. Object replication is supported for Blob Storage workloads only.

## Recover deleted or overwritten data

If you should need to recover data that has been overwritten or deleted, how you proceed depends on which data protection options you've enabled and which resource was affected. The following table describes the actions that you can take to recover data.

| Deleted or Overwritten Resource | Possible Recovery Actions | Requirements for Recovery |
|--------------------------------|---------------------------|--------------------------|
| Storage account | Attempt to recover the deleted storage account | The storage account was originally created with the Azure Resource Manager deployment model and was deleted within the past 14 days. A new storage account with the same name hasn't been created since the original account was deleted. |
| Container | Recover the soft-deleted container and its contents | Container soft delete is enabled and the container soft delete retention period hasn't yet expired. |
| Containers and blobs | Restore data from a second storage account | All container and blob operations have been effectively replicated to a second storage account. |
| Blob (any type) | Restore a blob from a previous version | Blob versioning is enabled and the blob has one or more previous versions. |
| Blob (any type) | Recover a soft-deleted blob | Blob soft delete is enabled and the soft delete retention interval hasn't expired. |
| Blob (any type) | Restore a blob from a snapshot | The blob has one or more snapshots. |
| Set of block blobs | Recover a set of block blobs to their state at an earlier point in time | Point-in-time restore is enabled and the restore point is within the retention interval. The storage account hasn't been compromised or corrupted. |
| Blob version | Recover a soft-deleted version | Blob soft delete is enabled. |

## Summary of cost considerations

| Data Protection Option | Cost Considerations |
|------------------------|----------------------|
| **Azure Resource Manager lock for a storage account** | No charge to configure a lock on a storage account. |
| **Immutability policy on a blob version** | No charge to enable version-level immutability on a container. Creating, modifying, or deleting a time-based retention policy or legal hold on a blob version results in a write transaction charge. |
| **Immutability policy on a container** | No charge to configure an immutability policy on a container. |
| **Container soft delete** | No charge to enable container soft delete for a storage account. Data in a soft-deleted container is billed at the same rate as active data until the soft-deleted container is permanently deleted. |
| **Blob versioning** | No charge to enable blob versioning for a storage account. After enabling, every write or delete operation on a blob creates a new version, potentially increasing capacity costs.<br><br>A blob version is billed based on unique blocks or pages. Costs increase as the base blob diverges from a version. Changing a blob or version's tier may have a billing impact. See [Pricing and billing](https://azure.microsoft.com/en-us/pricing/).<br><br>Use lifecycle management to delete older versions as needed to control costs. See [Optimize costs by automating Azure Blob Storage access tiers](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-lifecycle-management-concepts). |
| **Blob soft delete** | No charge to enable blob soft delete for a storage account. Data in a soft-deleted blob is billed at the same rate as active data until permanently deleted. |
| **Point-in-time restore** | No charge to enable point-in-time restore for a storage account; however, enabling it also enables blob versioning, soft delete, and change feed, which may incur other charges.<br><br>You're billed for point-in-time restore when performing a restore operation. The cost depends on the amount of data restored. See [Pricing and billing](https://azure.microsoft.com/en-us/pricing/). |
| **Blob snapshots** | Data in a snapshot is billed based on unique blocks or pages. Costs increase as the base blob diverges from the snapshot. Changing a blob or snapshot's tier may have a billing impact. See [Pricing and billing](https://azure.microsoft.com/en-us/pricing/).<br><br>Use lifecycle management to delete older snapshots as needed to control costs. See [Optimize costs by automating Azure Blob Storage access tiers](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-lifecycle-management-concepts). |
| **Copy data to a second storage account** | Maintaining data in a second storage account incurs capacity and transaction costs. If the second account is in a different region, copying data incurs egress charges. |

## Disaster Recovery

Azure Storage always maintains multiple copies of your data so that it's protected from planned and unplanned events, including transient hardware failures, network or power outages, and massive natural disasters. Redundancy ensures that your storage account meets its availability and durability targets even in the face of failures.

If a failure occurs in a data center, if your storage account is redundant across two geographical regions (geo-redundant), then you have the option to fail over your account from the primary region to the secondary region.

Customer-managed failover isn't currently supported for storage accounts with a hierarchical namespace enabled.
