# Enable double encryption at the Azure Storage infrastructure level

Azure Storage automatically encrypts all data in a storage account at the service level using 256-bit AES encryption, which is one of the strongest block ciphers available, and is FIPS 140-2 compliant. Customers who require higher levels of assurance that their data is secure can also enable 256-bit AES encryption at the Azure Storage infrastructure level for double encryption. Double encryption of Azure Storage data protects against a scenario where one of the encryption algorithms or keys may be compromised. In this scenario, the additional layer of encryption continues to protect your data.

Infrastructure encryption can be enabled for the entire storage account, or for an encryption scope within an account. When infrastructure encryption is enabled for a storage account or an encryption scope, data is encrypted twice — once at the service level and once at the infrastructure level — with two different encryption algorithms and two different keys.

Service-level encryption supports the use of either Microsoft-managed keys or customer-managed keys with Azure Key Vault or Key Vault Managed Hardware Security Model (HSM). Infrastructure-level encryption relies on Microsoft-managed keys and always uses a separate key.

To doubly encrypt your data, you must first create a storage account or an encryption scope that is configured for infrastructure encryption.

Infrastructure encryption is recommended for scenarios where doubly encrypting data is necessary for compliance requirements. For most other scenarios, Azure Storage encryption provides a sufficiently powerful encryption algorithm, and there's unlikely to be a benefit to using infrastructure encryption.

