# Internet of Things Security

This unit summarizes the Azure security baseline for IoT Hub to assist you in creating new requirements specifications for IoT workloads.

Please refer to Introduction to Microsoft Cybersecurity Reference Architecture and cloud security benchmark for more background on Microsoft Cloud Security Benchmark.

In the table below, we have included controls from the full baseline where:

1) Security controls were supported but not enabled by default

2) There was explicit guidance which contained action to be taken on the part of the customer

| **Area**              | **Control**                                                   | **Feature**                                  | **Guidance Summary**                                                                                                                                                                          |
|-----------------------|---------------------------------------------------------------|----------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Network security      | NS-2: Secure cloud services with network controls             | Azure Private Link                            | Deploy private endpoints for all Azure resources that support the Private Link feature, to establish a private access point for the resources.                                               |
|                       | NS-2: Secure cloud services with network controls             | Disable Public Network Access                 | Disable public network access either using the service-level IP ACL filtering rule or a toggling switch for public network access.                                                           |
| Identity management   | IM-1: Use centralized identity and authentication system      | Local Authentication Methods for Data Plane Access | Restrict the use of local authentication methods for data plane access. Instead, use Microsoft Entra ID as the default authentication method to control your data plane access.        |
|                       | IM-3: Manage application identities securely and automatically | Managed Identities                            | Use Azure managed identities instead of service principals when possible, which can authenticate to Azure services and resources that support Microsoft Entra authentication.               |
|                       |                                                               | Service Principals                            | There is no current Microsoft guidance for this feature configuration. Please review and determine if your organization wants to configure this security feature.                          |
|                       | IM-7: Restrict resource access based on conditions            | Conditional Access for Data Plane             | Define the applicable conditions and criteria for Microsoft Entra Conditional Access in the workload.                                                                                        |
| Privileged access     | PA-7: Follow just enough administration (least privilege) principle | Azure RBAC for Data Plane                  | With Azure AD and RBAC, IoT Hub requires the principal requesting the API to have the appropriate level of permission for authorization. Assign appropriate roles as needed.                 |
| Data protection       | DP-6: Use a secure key management process                     | Key Management in Azure Key Vault             | Use Azure Key Vault to create and control the life cycle of your encryption keys, including key generation, distribution, and storage. Rotate/revoke keys per schedule or incidents.        |
| Asset management      | AM-2: Use only approved services                              | Azure Policy Support                          | Use Microsoft Defender for Cloud to configure Azure Policy to audit and enforce configurations of your Azure resources.                                                                      |
| Logging and threat detection | LT-4: Enable logging for security investigation        | Azure Resource Logs                           | Enable resource logs for the service.                                                                                                                                                         |

