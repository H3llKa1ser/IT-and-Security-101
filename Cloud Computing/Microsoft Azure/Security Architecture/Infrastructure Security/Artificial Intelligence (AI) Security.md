# Artificial Intelligence (AI) Security

This unit presents a summary of the Well Architected Framework recommendations for securing Azure Open AI

For more information, see Azure Well-Architected Framework perspective on Azure OpenAI Service

The purpose of the Security pillar is to provide confidentiality, integrity, and availability guarantees to the workload.

The Security design principles provide a high-level design strategy for achieving those goals by applying approaches to the technical design around Azure OpenAI.

## Design checklist

Start your design strategy based on the design review checklist for Security and identify vulnerabilities and controls to improve the security posture. Then, review the Azure security baseline for Azure OpenAI. Finally, extend the strategy to include more approaches as needed.

1) Protect confidentiality: If you upload training data to Azure OpenAI, use customer-managed keys for data encryption, implement a key-rotation strategy, and delete training, validation, and training results data. If you use an external data store for training data, follow security best practices for that store. For example, for Azure Blob Storage, use customer-managed keys for encryption and implement a key-rotation strategy. Use managed identity-based access, implement a network perimeter by using private endpoints, and enable access logs.

2) Protect confidentiality: Guard against data exfiltration by limiting the outbound URLs that Azure OpenAI resources can access.

3) Protect integrity: Implement access controls to authenticate and authorize user access to the system by using the least-privilege principle and by using individual identities instead of keys.

4) Protect integrity: Implement jailbreak risk detection to safeguard your language model deployments against prompt injection attacks.

5) Protect availability: Use security controls to prevent attacks that might exhaust model usage quotas. You might configure controls to isolate the service on a network. If the service must be accessible from the internet, consider using a gateway to block suspected abuse by using routing or throttling.

## Recommendations

# Azure OpenAI Security Recommendations

| **Recommendation** | **Benefit** |
|---------------------|-------------|
| **Secure keys**: Store Azure OpenAI keys in Azure Key Vault instead of in application code. | Reduces the chance of secrets leaking and enables centralized management for tasks like key rotation. |
| **Restrict access**: Disable public access to Azure OpenAI unless needed. Use private endpoints for access from Azure VNets. | Prevents unauthorized access and keeps traffic private between application and platform. |
| **Microsoft Entra ID**: Use Entra ID for authentication and authorization with RBAC. Disable local authentication (`disableLocalAuth=true`). Assign appropriate roles (e.g., *Cognitive Services OpenAI User*, *Contributor*). | Centralizes identity management and eliminates use of API keys. Enables fine-grained access control through RBAC. |
| **Use customer-managed keys**: Apply for fine-tuned models and uploaded training data. | Provides flexibility to create, rotate, disable, and revoke encryption keys for stronger data governance. |
| **Protect against jailbreak attacks**: Use Azure AI Content Safety Studio. | Helps detect and block jailbreak attempts that try to bypass safety mechanisms in Azure OpenAI. |
