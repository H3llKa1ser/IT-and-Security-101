# Application and DevOps security

DevOps Security covers the controls related to the security engineering and operations in the DevOps processes, including deployment of critical security checks (such as static application security testing, vulnerability management) prior to the deployment phase to ensure the security throughout the DevOps process; it also includes common topics such as threat modeling and software supply security.

This unit gives a summary of the Microsoft cloud security benchmark controls in the DevOps Security family.

Please refer to Introduction to Microsoft Cybersecurity Reference Architecture and cloud security benchmark for more background on Microsoft Cloud Security Benchmark.

In the summary below, we have included controls from the full baseline where:

1) Security controls were supported but not enabled by default

2) There was explicit guidance which contained action to be taken on the part of the customer

Microsoft cloud security benchmark outlines seven critical controls for DevOps security.

DS-1: Conduct threat modeling

DS-2: Ensure software supply chain security

DS-3: Secure DevOps infrastructure

DS-4: Integrate static application security testing into DevOps pipeline

DS-5: Integrate dynamic application security testing into DevOps pipeline

DS-6: Enforce security of workload throughout DevOps lifecycle

DS-7: Enable logging and monitoring in DevOps

Those controls are summarized in the following table:

| **Control number** | **Title**                                             | **Summary**                                                                                                                                                                   |
|--------------------|-------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **DS-1**           | Conduct threat modeling                               | Perform threat modeling to identify potential threats and enumerate the mitigating controls.                                                                                  |
| **DS-2**           | Ensure software supply chain security                 | Ensure your enterprise’s SDLC includes security controls to govern both in-house and third-party software components (including open-source software) with dependency management. |
| **DS-3**           | Secure DevOps infrastructure                          | Ensure the DevOps infrastructure and pipeline follow security best practices across environments including build, test, and production stages.                                  |
| **DS-4**           | Integrate static application security testing into DevOps pipeline | Ensure static application security testing (SAST), fuzzy testing, interactive testing, and mobile application testing are part of the gating controls in the CI/CD workflow.      |
| **DS-5**           | Integrate dynamic application security testing into DevOps pipeline | Ensure dynamic application security testing (DAST) is part of the gating controls in the CI/CD workflow to prevent vulnerabilities from reaching production.                     |
| **DS-6**           | Enforce security of workload throughout DevOps lifecycle | Ensure the workload is secured throughout the entire lifecycle (development, testing, and deployment stages), with security controls like network security and identity management. |
| **DS-7**           | Enable logging and monitoring in DevOps               | Ensure logging and monitoring include non-production environments and CI/CD workflow elements to identify vulnerabilities and threats early in the development process.            |

