# Azure Storage

The Azure Storage platform is Microsoft's cloud storage solution for modern data storage scenarios. Azure Storage offers highly available, massively scalable, durable, and secure storage for a variety of data objects in the cloud. Azure Storage data objects are accessible from anywhere in the world over HTTP or HTTPS via a REST API. Azure Storage also offers client libraries for developers building applications or services with .NET, Java, Python, JavaScript, C++, and Go. Developers and IT professionals can use Azure PowerShell and Azure CLI to write scripts for data management or configuration tasks. The Azure portal and Azure Storage Explorer provide user-interface tools for interacting with Azure Storage.

## Benefits of Azure Storage

Azure Storage services offer the following benefits for application developers and IT professionals:

1) Durable and highly available. Redundancy ensures that your data is safe in the event of transient hardware failures. You can also opt to replicate data across data centers or geographical regions for additional protection from local catastrophe or natural disaster. Data replicated in this way remains highly available in the event of an unexpected outage.

2) Secure. All data written to an Azure storage account is encrypted by the service. Azure Storage provides you with fine-grained control over who has access to your data.

3) Scalable. Azure Storage is designed to be massively scalable to meet the data storage and performance needs of today's applications.

4) Managed. Azure handles hardware maintenance, updates, and critical issues for you.

5) Accessible. Data in Azure Storage is accessible from anywhere in the world over HTTP or HTTPS. Microsoft provides client libraries for Azure Storage in a variety of languages, including .NET, Java, Node.js, Python, Go, and others, as well as a mature REST API. Azure Storage supports scripting in Azure PowerShell or Azure CLI. And the Azure portal and Azure Storage Explorer offer easy visual solutions for working with your data.

## Azure Storage data services

The Azure Storage platform includes the following data services:

1) Azure Blobs: A massively scalable object store for text and binary data. Also includes support for big data analytics through Data Lake Storage Gen2.

2) Azure Files: Managed file shares for cloud or on-premises deployments.

3) Azure Elastic SAN: A fully integrated solution that simplifies deploying, scaling, managing, and configuring a SAN in Azure.

4) Azure Queues: A messaging store for reliable messaging between application components.

5) Azure Tables: A NoSQL store for schemaless storage of structured data.

6) Azure managed Disks: Block-level storage volumes for Azure VMs.

7) Azure Container Storage (preview): A volume management, deployment, and orchestration service built natively for containers.

Each service is accessed through a storage account with a unique address. To get started, see Create a storage account.

Additionally, Azure provides the following specialized storage:

8) Azure NetApp Files: Enterprise files storage, powered by NetApp: makes it easy for enterprise line-of-business (LOB) and storage professionals to migrate and run complex, file-based applications with no code change. Azure NetApp Files is managed via NetApp accounts and can be accessed via NFS, SMB and dual-protocol volumes.

## Blob Storage

Azure Blob Storage is Microsoft's object storage solution for the cloud. Blob Storage is optimized for storing massive amounts of unstructured data, such as text or binary data.

Blob Storage is ideal for:

1) Serving images or documents directly to a browser.

2) Storing files for distributed access.

3) Streaming video and audio.

4) Storing data for backup and restore, disaster recovery, and archiving.

5) Storing data for analysis by an on-premises or Azure-hosted service.

Objects in Blob Storage can be accessed from anywhere in the world via HTTP or HTTPS. Users or client applications can access blobs via URLs, the Azure Storage REST API, Azure PowerShell, Azure CLI, or an Azure Storage client library. The storage client libraries are available for multiple languages, including .NET, Java, Node.js, and Python.

Clients can also securely connect to Blob Storage by using SSH File Transfer Protocol (SFTP) and mount Blob Storage containers by using the Network File System (NFS) 3.0 protocol.

## Azure Files

Azure Files enables you to set up highly available network file shares that can be accessed by using the industry standard Server Message Block (SMB) protocol, Network File System (NFS) protocol, and Azure Files REST API. That means that multiple VMs can share the same files with both read and write access. You can also read the files using the REST interface or the storage client libraries.

One thing that distinguishes Azure Files from files on a corporate file share is that you can access the files from anywhere in the world using a URL that points to the file and includes a shared access signature (SAS) token. You can generate SAS tokens; they allow specific access to a private asset for a specific amount of time.

File shares can be used for many common scenarios:

1) Many on-premises applications use file shares. This feature makes it easier to migrate those applications that share data to Azure. If you mount the file share to the same drive letter that the on-premises application uses, the part of your application that accesses the file share should work with minimal, if any, changes.

2) Configuration files can be stored on a file share and accessed from multiple VMs. Tools and utilities used by multiple developers in a group can be stored on a file share, ensuring that everybody can find them, and that they use the same version.

3) Resource logs, metrics, and crash dumps are just three examples of data that can be written to a file share and processed or analyzed later.

## Azure Elastic Storage Area Network

Azure Elastic storage area network (SAN) is Microsoft's answer to the problem of workload optimization and integration between your large scale databases and performance-intensive mission-critical applications. Elastic SAN is a fully integrated solution that simplifies deploying, scaling, managing, and configuring a SAN, while also offering built-in cloud capabilities like high availability.

Elastic SAN is designed for large scale Input/Output-intensive workloads and top tier databases such as SQL, MariaDB, and support hosting the workloads on virtual machines, or containers such as Azure Kubernetes Service. Elastic SAN volumes are compatible with a wide variety of compute resources through theInternet Small Computer Systems Interface (iSCSI) protocol. Some other benefits of Elastic SAN include a simplified deployment and management interface. Since you can manage storage for multiple compute resources from a single interface, and cost optimization.

## Azure Container Storage (preview)

Azure Container Storage integrates with Kubernetes and utilizes existing Azure Storage offerings for actual data storage, offering a volume orchestration and management solution purposely built for containers. You can choose any of the supported backing storage options to create a storage pool for your persistent volumes.

Azure Container Storage offers substantial benefits:

1) Rapid scale out of stateful pods

2) Improved performance for stateful workloads

3) Kubernetes-native volume orchestration

## Queue Storage

The Azure Queue service is used to store and retrieve messages. Queue messages can be up to 64 KB in size, and a queue can contain millions of messages. Queues are generally used to store lists of messages to be processed asynchronously.

For example, say you want your customers to be able to upload pictures, and you want to create thumbnails for each picture. You could have your customer wait for you to create the thumbnails while uploading the pictures. An alternative would be to use a queue. When the customer finishes their upload, write a message to the queue. Then have an Azure Function retrieve the message from the queue and create the thumbnails. Each of the parts of this processing can be scaled separately, giving you more control when tuning it for your usage.

## Table Storage

Azure Table Storage is now part of Azure Cosmos DB. In addition to the existing Azure Table Storage service, there's a new Azure Cosmos DB for Table offering that provides throughput-optimized tables, global distribution, and automatic secondary indexes.

## Disk Storage

An Azure managed disk is a virtual hard disk (VHD). You can think of it like a physical disk in an on-premises server but, virtualized. Azure-managed disks are stored as page blobs, which are a random Input/Output storage object in Azure. We call a managed disk 'managed' because it's an abstraction over page blobs, blob containers, and Azure storage accounts. With managed disks, all you have to do is provision the disk, and Azure takes care of the rest.

## Azure NetApp Files

Azure NetApp Files is an enterprise-class, high-performance, metered file storage service. Azure NetApp Files supports any workload type and is highly available by default. You can select service and performance levels, create NetApp accounts, capacity pools, volumes, and manage data protection.

# Secure access to storage accounts

Every request to Azure Storage must be authorized. Azure Storage supports the following authorization methods:

1) Microsoft Entra integration for blob, file, queue, and table data. Azure Storage supports authentication and authorization with Microsoft Entra ID for the Blob, File, Table, and Queue services via Azure role-based access control (Azure RBAC). Authorizing requests with Microsoft Entra ID is recommended for superior security and ease of use.

2) Identity-based authentication over SMB for Azure Files. Azure Files supports identity-based authorization over SMB (Server Message Block) through either on-premises Microsoft Entra Domain Services, or Microsoft Entra Kerberos (hybrid user accounts only).

3) Authorization with Shared Key. The Azure Storage Blob, Files, Queue, and Table services support authorization with Shared Key. A client using Shared Key authorization passes a header with every request that is signed using the storage account access key. pended to the URI for a storage resource. The security token encapsulates constraints such as permissions and the interval of access.

4) Microsoft Entra Domain Services with Azure NetApp Files. Azure NetApp Files features such as SMB volumes, dual-protocol volumes, and NFSv4.1 Kerberos volumes are designed to be used with Microsoft Entra Domain Services.

# Encryption

There are two basic kinds of encryption available for Azure Storage: encryption at rest and client-side encryption.

1. Encryption at rest

Azure Storage encryption protects and safeguards your data to meet your organizational security and compliance commitments. Azure Storage automatically encrypts all data prior to persisting to the storage account and decrypts it prior to retrieval. The encryption, decryption, and key management processes are transparent to users. Customers can also choose to manage their own keys using Azure Key Vault.

2. Client-side encryption

The Azure Storage client libraries provide methods for encrypting data from the client library before sending it across the wire and decrypting the response. Data encrypted via client-side encryption is also encrypted at rest by Azure Storage.

Azure NetApp Files data traffic is inherently secure by design, as it doesn't provide a public endpoint and data traffic stays within customer-owned VNet. Data-in-flight isn't encrypted by default. However, data traffic from an Azure VM (running an Network File System or Server Message Block client) to Azure NetApp Files is as secure as any other Azure-VM-to-VM traffic. NFSv4.1 and SMB3 data-in-flight encryption can optionally be enabled.

# Redundancy

To ensure that your data is durable, Azure Storage stores multiple copies of your data. When you set up your storage account, you select a redundancy option.

Azure NetApp Files provides locally redundant storage with 99.99% availability.

## Transfer data to and from Azure Storage

You have several options for moving data into or out of Azure Storage. Which option you choose depends on the size of your dataset and your network bandwidth.

Azure NetApp Files provides NFS and SMB volumes. You can use any file-based copy tool to migrate data to the service.
