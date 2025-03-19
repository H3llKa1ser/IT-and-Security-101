# Azure Front Door

Whether you’re delivering content and files or building global apps and APIs, Azure Front Door can help you deliver higher availability, lower latency, greater scale, and more secure experiences to your users wherever they are.

Azure Front Door is Microsoft’s modern cloud Content Delivery Network (CDN) that provides fast, reliable, and secure access between your users and your applications’ static and dynamic web content across the globe. Azure Front Door delivers your content using Microsoft’s global edge network with hundreds of global and local points of presence (PoPs) distributed around the world close to both your enterprise and consumer end users.

![image](https://github.com/user-attachments/assets/613163df-fe24-468c-ad6f-2581ab516001)

#### NOTE: For web workloads, we highly recommend utilizing Azure DDoS protection and a web application firewall to safeguard against emerging DDoS attacks. Another option is to employ Azure Front Door along with a web application firewall. Azure Front Door offers platform-level protection against network-level DDoS attacks.

Azure Front Door enables internet-facing application to:

1) Build and operate modern internet-first architectures that have dynamic, high-quality digital experiences with highly automated, secure, and reliable platforms.

2) Accelerate and deliver your app and content globally at scale to your users wherever they're creating opportunities for you to compete, weather change, and quickly adapt to new demand and markets.

3) Intelligently secure your digital estate against known and new threats with intelligent security that embrace a Zero Trust framework.

## Key Benefits

Global delivery scale using Microsoft’s network

Scale out and improve performance of your applications and content using Microsoft’s global Cloud CDN and WAN.

1) Leverage over 118 edge locations across 100 metro cities connected to Azure using a private enterprise-grade WAN and improve latency for apps by up to 3 times.

2) Accelerate application performance by using Front Door’s anycast network and split TCP connections.

3) Terminate SSL offload at the edge and use integrated certificate management.

4) Natively support end-to-end IPv6 connectivity and the HTTP/2 protocol.

## Deliver modern apps and architectures

Modernize your internet first applications on Azure with Cloud Native experiences

Integrate with DevOps friendly command line tools across SDKs of different languages, Bicep, Azure Resource Manager templates, CLI and PowerShell.

Define your own custom domain with flexible domain validation.

Load balance and route traffic across origins and use intelligent health probe monitoring across apps or content hosted in Azure or anywhere.

Integrate with other Azure services such as DNS, Web Apps, Storage and many more for domain and origin management.

Move your routing business logic to the edge with enhanced rules engine capabilities including regular expressions and server variables.

Analyze built-in reports with an all-in-one dashboard for both Front Door and security patterns.

Monitoring your Front Door traffic in real time, and configuring alerts that integrate with Azure Monitor.

Log each Front Door request and failed health probes.

## Simple and cost-effective

Unified static and dynamic delivery offered in a single tier to accelerate and scale your application through caching, SSL offload, and layer 3-4 DDoS protection.

Free, autorotation managed SSL certificates that save time and quickly secure apps and content.

Low entry fee and a simplified cost model that reduces billing complexity by having fewer meters needed to plan for.

Azure to Front Door integrated egress pricing that removes the separate egress charge from Azure regions to Azure Front Door.

## Intelligent secure internet perimeter

Secure applications with built-in layer 3-4 DDoS protection, seamlessly attached Web Application Firewall (WAF), and Azure DNS to protect your domains.

Protect your applications against layer 7 DDoS attacks using WAF.

Protect your applications from malicious actors with Bot manager rules based on Microsoft’s own Threat Intelligence.

Privately connect to your backend behind Azure Front Door with Private Link and embrace a zero-trust access model.

Provide a centralized security experience for your application via Azure Policy and Azure Advisor that ensures consistent security features across apps.

## Comparison between Azure Front Door and Azure CDN services

Azure Front Door and Azure CDN are both Azure services that offer global content delivery with intelligent routing and caching capabilities at the application layer. Both services can be used to optimize and accelerate your applications by providing a globally distributed network of points of presence (POP) close to your users. Both services also offer a variety of features to help you secure your applications from malicious attacks and to help you monitor your application's health and performance.

![image](https://github.com/user-attachments/assets/0e72cf34-8563-44e4-ab72-9803e7773435)

#### NOTE: To switch between tiers, you will need to recreate the Azure Front Door profile. You can use the migration capability to move your existing Azure Front Door profile to the new tier. For more information about upgrading from Standard to Premium, see upgrade capability.

## Service comparison

| Features and Optimizations | Front Door Standard | Front Door Premium | Front Door Classic | Azure CDN Standard Microsoft | Azure CDN Standard Edgio | Azure CDN Premium Edgio |
|---------------------------|---------------------|---------------------|---------------------|-----------------------------|--------------------------|--------------------------|
| **Delivery and Acceleration** | | | | | | |
| Static file delivery | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Dynamic site delivery | ✓ | ✓ | ✓ |  | ✓ | ✓ |
| **Domains and Certs** | | | | | | |
| Custom domains | ✓ - DNS TXT record based domain validation | ✓ - DNS TXT record based domain validation | ✓ - CNAME based validation | ✓ - CNAME based validation | ✓ - CNAME based validation | ✓ - CNAME based validation |
| Prevalidated domain integration with Azure PaaS Service | ✓ | ✓ |  |  |  |  |
| HTTPS support | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Custom domain HTTPS | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Bring your own certificate | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Supported TLS Versions | TLS1.3, TLS1.2, TLS1.0 | TLS1.3, TLS1.2, TLS1.0 | TLS1.3, TLS1.2, TLS1.0 | TLS1.3, TLS1.2, TLS1.0/1.1 | TLS1.2, TLS1.3 | TLS1.2, TLS1.3 |
| **Caching** | | | | | | |
| Query string caching | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Cache manage (purge, rules, and compression) | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Fast purge |  |  |  | ✓ | ✓ |
| Asset pre-loading |  |  |  | ✓ | ✓ |
| Cache behavior settings | ✓ - using standard rules engine | ✓ - using standard rules engine | ✓ - using standard rules engine | ✓ - using standard rules engine | ✓ | ✓ |
| **Routing** | | | | | | |
| Origin load balancing | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Path based routing | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Rules engine | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Server variable | ✓ | ✓ |  |  |  |  |
| Regular expression in rules engine | ✓ | ✓ |  |  | ✓ |  |
| URL redirect/rewrite | ✓ | ✓ | ✓ | ✓ |  | ✓ |
| IPv4/IPv6 dual-stack | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| HTTP/2 support | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Routing preference unmetered | Not required as Data transfer from Azure origin to AFD is free and path is directly connected | Not required as Data transfer from Azure origin to AFD is free and path is directly connected | Not required as Data transfer from Azure origin to AFD is free and path is directly connected | Not required as Data transfer from Azure origin to CDN is free and path is directly connected | ✓ | ✓ |
| Origin Port | All TCP ports | All TCP ports | All TCP ports | All TCP ports | All TCP ports | All TCP ports |
| Customizable, rules based content delivery engine | ✓ | ✓ | ✓ | ✓ using Standard rules engine |  | ✓ using Premium rules engine |
| Mobile device rules | ✓ | ✓ | ✓ | ✓ using Standard rules engine |  | ✓ using Premium rules engine |
| **Security** | | | | | | |
| Custom Web Application Firewall (WAF) rules | ✓ | ✓ | ✓ |  |  |  |
| Microsoft managed rule set |  | ✓ | ✓ - Only default rule set 1.1 or below |  |  |  |
| Bot protection |  | ✓ | ✓ - Only bot manager rule set 1.0 |  |  |  |
| Private link connection to origin |  | ✓ |  |  |  |  |
| Geo-filtering | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Token authentication |  |  |  |  |  | ✓ |
| DDoS protection | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Domain Fronting Block | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| **Analytics and Reporting** | | | | | | |
| Monitoring Metrics | ✓ (more metrics than Classic) | ✓ (more metrics than Classic) | ✓ | ✓ | ✓ | ✓ |
| Advanced analytics/built-in reports | ✓ | ✓ - includes WAF report |  |  |  | ✓ |
| Raw logs - access logs and WAF logs | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Health probe log | ✓ | ✓ |  |  |  |  |
| **Ease of Use** | | | | | | |
| Easy integration with Azure services, such as Storage and Web Apps | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Management via REST API, .NET, Node.js, or PowerShell | ✓ | ✓ | ✓ | ✓ | ✓ | ✓ |
| Compression MIME types | Configurable | Configurable | Configurable | Configurable | Configurable | Configurable |
| Compression encodings | gzip, brotli | gzip, brotli | gzip, brotli | gzip, brotli | gzip, deflate, bzip2 | gzip, deflate, bzip2, brotli |
| Azure Policy integration |  |  | ✓ |  |  |  |
| Azure Advisory integration | ✓ | ✓ |  | ✓ | ✓ | ✓ |
| Managed Identities with Azure Key Vault | ✓ | ✓ |  |  |  |  |
| **Pricing** | | | | | | |
| Simplified pricing | ✓ | ✓ |  | ✓ | ✓ | ✓ |
