# Microsoft Cybersecurity Reference Architecture (MCRA)

The Microsoft Cybersecurity Reference Architectures (MCRA) are a set of technical diagrams that describe Microsoft’s cybersecurity capabilities. The diagrams describe how Microsoft security capabilities integrate with the following:

Microsoft platforms like Microsoft 365 and Microsoft Azure

Third party apps like ServiceNow and salesforce

Third party platforms like Amazon Web Services (AWS) and Google Cloud Platform (GCP)

The MCRA contains diagrams on the following topics:

Microsoft cybersecurity capabilities

1) Zero Trust and a Zero Trust rapid modernization plan (RaMP)

2) Zero trust user access

3) Security operations

4) Operational technology (OT)

5) Multicloud and cross-platform capabilities

6) Attack chain coverage

7) Azure native security controls

8) Security organizational functions

### Link: https://github.com/MicrosoftDocs/security/blob/main/Downloads/mcra-december-2023.pptx?raw=true

### Link 2: https://learn.microsoft.com/en-us/security/adoption/mcra

## Capabilities and controls with MCRA

Key best practices in the MCRA include:

1) Learn what you have available - Learn about and utilize all the security capabilities and controls that you have access to.

2) Use the right tool for the job - Use a multi-technology approach to apply the best solution to the problem, rather than relying on the same technology over and over like a network firewall or Security Information and Event Management (SIEM).

 - Data and Management Plane Security - Ensure that you include both data plane security controls (available since pre-cloud on-premises datacenters) as well as management plane security controls (embedded into cloud platforms that allow additional layer of visibility and control).

 - Security for the platform/infrastructure and the workload - Ensure you have controls to protect the specific workload (such as web application firewalls (WAFs)) as well as the overall infrastructure and development environments.

 - Use native cloud controls that are designed to secure your cloud assets.

 - Use consistent tooling across cloud providers to ensure controls are effectively implemented across all your infrastructure and platforms. This reduces the time and effort to implement and monitor controls, allowing you to accomplish more in security with the resources you have.

3) Approach security holistically - Securing an asset requires establishing visibility and control over the full lifecycle. For the example of a cloud hosted resource, this would include the following:

People accessing it

Accounts and groups they use to access it

Devices they log into those accounts with

interface that provides access to the resource (Azure portal, Command Line Interface, application programming interfaces, etc.)

The resource itself

Any underlying storage, virtual machines, containers, or other cloud/application services that interact with the resource

Any devices and customer accounts that interact with the resources
4) Focus on security and productivity - Ensure that security enables productivity as well as reducing risk. Security should provide 'healthy friction' that causes people to think critically    about risk while designing or operating a system. Security shouldn't create 'unhealthy friction' that blocks productivity and/or doesn't reduce risk in a meaningful way.

5) Protect privileged access - Ensure that privileged accounts and systems are protected with elevated security protections, monitoring, and response. Compromises of privileged access enable an attacker to shut down business operations across the organization in a ransomware/extortion attack. Attackers frequently target highly privileged accounts because that level of access allows rapid and efficient compromise of many systems at once, which increases the attacker's return on investment. Elevated protections organizations should include:
 
 - Protect privileged user accounts - with strong MFA, threat detection, and tagging accounts to ensure rapid response to anomalous events.

 - Protect workstations and devices used by these accounts with Privileged Access Workstations (PAWs) and additional monitoring and response.
 
 - Protect intermediaries that handle privileged accounts and sessions such as Virtual Private Networks (VPNs), PIM/PAM solutions, Domain Controllers, and more with elevated protections, security policy monitoring, threat detection, and more. For more information, see securing privileged access.
6) Prepare for ransomware and extortion attacks - Ensure that you are mitigating the risk of ransomware attacks starting with the most impactful controls
 - Validate BC/DR process - Ensure your business continuity and disaster recovery (BC/DR) process includes all business-critical systems in scope and a scenario for a ransomware/extortion attack. Also ensure that you have exercised this scenario recently. Without this, your ability to recover from this type of attack may be much slower and may not recover all business-critical systems.
 
 - Secure backups against sabotage - Ensure that backups are protected against deliberate attacker erasure or encryption, which is a common attacker tactic. If your backups are not secure, you may not be able to recover critical business operations without paying for the ransom/extortion payment. Paying a ransom is much slower, has no guarantee of success, and incurs potential liability and other risks.

