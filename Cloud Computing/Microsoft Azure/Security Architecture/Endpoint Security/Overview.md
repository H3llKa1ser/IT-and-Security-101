# Introduction to endpoint security

## Security Control: Endpoint security

This section provides a summary of the security controls for Endpoint security from the Microsoft cloud security benchmark.

Endpoint Security covers controls in endpoint detection and response, including use of endpoint detection and response (EDR) and anti-malware service for endpoints in cloud environments.

Please refer to Introduction to Microsoft Cybersecurity Reference Architecture and cloud security benchmark for more background on Microsoft Cloud Security Benchmark.

In the summary below, we have included controls from the full baseline where:

1) Security controls were supported but not enabled by default

2) There was explicit guidance which contained action to be taken on the part of the customer

### ES-1: Use Endpoint Detection and Response (EDR)

Security principle: Enable Endpoint Detection and Response (EDR) capabilities for VMs and integrate with SIEM and security operations processes.

Azure guidance: Microsoft Defender for Servers (with Microsoft Defender for Endpoint integrated) provides EDR capability to prevent, detect, investigate, and respond to advanced threats.

Use Microsoft Defender for Cloud to deploy Microsoft Defender for Servers for your endpoint and integrate the alerts to your SIEM solution such as Microsoft Sentinel.

AWS guidance: Onboard your AWS account into Microsoft Defender for Cloud and deploy Microsoft Defender for Servers (with Microsoft Defender for Endpoint integrated) in your EC2 instances which provides EDR capability to prevent, detect, investigate, and respond to advanced threats.

Alternatively, use Amazon GuardDuty integrated threat intelligence capability to monitor and protect your EC2 instances. Amazon GuardDuty can detect anomaly activities such as includes activity indicating an instance compromise, such as cryptocurrency mining, malware using domain generation algorithms (DGAs), outbound denial of service activity, unusually high volume of network traffic, unusual network protocols, outbound instance communication with a known malicious IP, temporary Amazon EC2 credentials used by an external IP address, and data exfiltration using DNS.

### ES-2: Use modern anti-malware software

Security principle: Use anti-malware solutions (also known as endpoint protection) capable of real-time protection and periodic scanning.

Azure guidance: Microsoft Defender for Cloud can automatically identify the use of a number of popular anti-malware solutions for your virtual machines and on-premises machines with Azure Arc configured, and report the endpoint protection running status and make recommendations.

Microsoft Defender Antivirus is the default anti-malware solution for Windows server 2016 and above. For Windows server 2012 R2, use Microsoft Antimalware extension to enable SCEP (System Center Endpoint Protection). For Linux VMs, use Microsoft Defender for Endpoint on Linux for the endpoint protection feature.

For both Windows and Linux, you can use Microsoft Defender for Cloud to discover and assess the health status of the anti-malware solution.

AWS guidance: Onboard your AWS account into Microsoft Defender for Cloud to allow Microsoft Defender for Cloud automatically identify the use of a number of popular anti-malware solutions for EC2 instances with Azure Arc configured and report the endpoint protection running status and make recommendations.

Deploy Microsoft Defender Antivirus which is the default anti-malware solution for Windows server 2016 and above. For EC2 instances running Windows server 2012 R2, use Microsoft Antimalware extension to enable SCEP (System Center Endpoint Protection). For EC2 instances running Linux, use Microsoft Defender for Endpoint on Linux for the endpoint protection feature.

For both Windows and Linux, you can use Microsoft Defender for Cloud to discover and assess the health status of the anti-malware solution.

### ES-3: Ensure anti-malware software and signatures are updated

Security principle: Ensure anti-malware signatures are updated rapidly and consistently for the anti-malware solution.

Azure guidance: Follow recommendations in Microsoft Defender for Cloud to keep all endpoints up to date with the latest signatures. Microsoft Antimalware (for Windows) and Microsoft Defender for Endpoint (for Linux) will automatically install the latest signatures and engine updates by default.

For third-party solutions, ensure the signatures are updated in the third-party anti-malware solution.

AWS guidance: With your AWS account onboarded into Microsoft Defender for Cloud, follow recommendations in Microsoft Defender for Cloud to keep all endpoints up to date with the latest signatures. Microsoft Antimalware (for Windows) and Microsoft Defender for Endpoint (for Linux) will automatically install the latest signatures and engine updates by default.

For third-party solutions, ensure the signatures are updated in the third-party anti-malware solution.
