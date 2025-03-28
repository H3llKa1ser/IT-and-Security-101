# Microsoft Defender for Cloud DevOps Security

Microsoft Defender for Cloud enables comprehensive visibility, posture management, and threat protection across multicloud environments including Azure, AWS, GCP, and on-premises resources.

DevOps security within Defender for Cloud uses a central console to empower security teams with the ability to protect applications and resources from code to cloud across multi-pipeline environments, including Azure DevOps, GitHub, and GitLab. DevOps security recommendations can then be correlated with other contextual cloud security insights to prioritize remediation in code. Key DevOps security capabilities include:

1) Unified visibility into DevOps security posture: Security administrators now have full visibility into DevOps inventory and the security posture of preproduction application code across multi-pipeline and multicloud environments, which includes findings from code, secrets, and open-source dependency vulnerability scans. They can also assess the security configurations of their DevOps environment.

2) Strengthen cloud resource configurations throughout the development lifecycle: You can enable security of Infrastructure as Code (IaC) templates and container images to minimize cloud misconfigurations reaching production environments, allowing security administrators to focus on any critical evolving threats.

3) Prioritize remediation of critical issues in code: Apply comprehensive code-to-cloud contextual insights within Defender for Cloud. Security admins can help developers prioritize critical code fixes with pull request annotations and assign developer ownership by triggering custom workflows feeding directly into the tools developers know and love.

These features help unify, strengthen, and manage multi-pipeline DevOps resources.

## Manage your DevOps environments in Defender for Cloud

DevOps security in Defender for Cloud allows you to manage your connected environments and provide your security teams with a high-level overview of issues discovered in those environments through the DevOps security console.

![image](https://github.com/user-attachments/assets/f23066b1-4cde-4942-80ef-2d5149f4ad0a)

Here, you can add Azure DevOps, GitHub, and GitLab environments, customize the DevOps workbook to show your desired metrics, and configure pull request annotations.

![image](https://github.com/user-attachments/assets/4b1fbd65-4bc8-46d8-8f91-38c3f535b115)

## Understanding your DevOps security

![image](https://github.com/user-attachments/assets/83090929-3a0c-4e77-883c-99dbb6721d60)

### Review your findings

The DevOps inventory table allows you to review onboarded DevOps resources and the security information related to them.

![image](https://github.com/user-attachments/assets/558cd99b-7ab5-49c1-8936-3ba059e6763c)

On this part of the screen you see:

Name - Lists onboarded DevOps resources from Azure DevOps, GitHub, and/or GitLab. View the resource health page by selecting it.

1) DevOps environment - Describes the DevOps environment for the resource (that is, Azure DevOps, GitHub, GitLab). Use this column to sort by environment if multiple environments are onboarded.

2) Advanced security status - Shows whether advanced security features are enabled for the DevOps resource.

3) On - Advanced security is enabled.

4) Off - Advanced security isn't enabled.

5) Partially enabled - Certain Advanced security features aren't enabled (for example, code scanning is off).

6) N/A - Defender for Cloud doesn't have information about enablement.

#### NOTE: Currently, this information is available only for Azure DevOps and GitHub repositories.

Pull request annotation status - Shows whether PR annotations are enabled for the repository.

1) On - PR annotations are enabled.

2) Off - PR annotations aren't enabled.

3) N/A - Defender for Cloud doesn't have information about enablement.

#### NOTE: Currently, this information is available only for Azure DevOps repositories.

Findings - Shows the total number of codes, secrets, dependency, and infrastructure-as-code findings identified in the DevOps resource.

This table can be viewed as a flat view at the DevOps resource level (repositories for Azure DevOps and GitHub, projects for GitLab) or in a grouping view showing organizations/projects/groups hierarchy. Also, the table can be filtered by subscription, resource type, finding type, or severity.

## DevOps environment security posture

With an increase of cyber attacks on source code management systems and continuous integration/continuous delivery pipelines, securing DevOps platforms against the diverse range of threats identified in the DevOps Threat Matrix is crucial. Such cyber attacks can enable code injection, privilege escalation, and data exfiltration, potentially leading to extensive impact.

DevOps posture management is a feature in Microsoft Defender for Cloud that:

1) Provides insights into the security posture of the entire software supply chain lifecycle.

2) Uses advanced scanners for in-depth assessments.

3) Covers various resources, from organizations, pipelines, and repositories.

4) Allows customers to reduce their attack surface by uncovering and acting on the provided recommendations.

## DevOps scanners

To provide findings, DevOps posture management uses DevOps scanners to identify weaknesses in source code management and continuous integration/continuous delivery pipelines by running checks against the security configurations and access controls.

Azure DevOps and GitHub scanners are used internally within Microsoft to identify risks associated with DevOps resources, reducing attack surface and strengthening corporate DevOps systems.

Once a DevOps environment is connected, Defender for Cloud autoconfigures these scanners to conduct recurring scans every 24 hours across multiple DevOps resources, including:

Builds
Secure Files
Variable Groups
Service Connections
Organizations
Repositories

## DevOps threat matrix risk reduction

DevOps posture management assists organizations in discovering and remediating harmful misconfigurations in the DevOps platform. This leads to a resilient, zero-trust DevOps environment, which is strengthened against a range of threats defined in the DevOps threat matrix. The primary posture management controls include:

1) Scoped secret access: Minimize the exposure of sensitive information and reduce the risk of unauthorized access, data leaks, and lateral movements by ensuring each pipeline only has access to the secrets essential to its function.

2) Restriction of self-hosted runners and high permissions: prevent unauthorized executions and potential escalations by avoiding self-hosted runners and ensuring that pipeline permissions default to read-only.

3) Enhanced branch protection: Maintain the integrity of the code by enforcing branch protection rules and preventing malicious code injections.

4) Optimized permissions and secure repositories: Reduce the risk of unauthorized access, modifications by tracking minimum base permissions, and enablement of secret push protection for repositories.

## DevOps threat matrix

Our goal for developing the threat matrix for DevOps is to build a comprehensive knowledgebase that Defenders can use to keep track of and build defenses against relevant attack techniques. Using the MITRE ATT&CK framework as a base, we collected techniques and attack vectors associated with DevOps environments and created a matrix dedicated to DevOps attack methods.

It is worth noting that the tactics in this matrix must be looked at from the DevOps perspective. For example, execution techniques in a Virtual Machine running Windows or Linux OS are different from the Execution in a DevOps pipeline. In the Linux case, execution means running code in the OS. When we talk about DevOps environments, it means running code in the pipeline or DevOps resources. In addition to using this threat matrix to categorize attacks and corresponding defense methods, Defenders can work alongside red teams to continuously test assumptions and find new potential attack techniques.

## MITRE ATT&CK Defined

The MITRE ATT&CK matrix is a publicly accessible knowledge base for understanding the various tactics and techniques used by attackers during a cyberattack.

The knowledge base is organized into several categories: pre-attack, initial access, execution, persistence, privilege escalation, defense evasion, credential access, discovery, lateral movement, collection, exfiltration, and command and control.

Tactics (T) represent the "why" of an ATT&CK technique or sub-technique. It is the adversary's tactical goal: the reason for performing an action. For example, an adversary may want to achieve credential access.

Techniques (T) represent "how'" an adversary achieves a tactical goal by performing an action. For example, an adversary may dump credentials to achieve credential access.

Common Knowledge (CK) in ATT&CK stands for common knowledge, essentially the documented modus operandi of tactics and techniques executed by adversaries.

### Initial access

The initial access tactic refers to techniques an attacker may use for gaining access to the DevOps resources – repositories, pipelines, and dependencies. The following techniques may be a precondition for the next steps:

Source Code Management (SCM) authentication – Access by having an authentication method to the organization’s source code management. It may be a personal access token (PAT), an SSH key, or any other allowed authentication credential. An example of a method an attacker can use to achieve this technique is using a phishing attack against an organization.

Continuous Integration (CI) and Continuous Delivery (CD) service authentication – Similar to SCM authentication, an attacker can leverage authentication to the CI/CD service in order to attack the organization’s DevOps.

Organization’s public repositories – Access to the organization’s public repositories that are configured with CI/CD capabilities. Depending on the organization’s configuration, these repositories may have the ability to trigger a pipeline run after a pull request (PR) is created.

Endpoint compromise – Using an existing compromise, an attacker can leverage the compromised developer’s workstation, thus gaining access to the organization’s SCM, registry, or any other resource the developer has access to.

Configured webhooks – When an organization has a webhook configured, an attacker could use it as an initial access method into the organization’s network by using the SCM itself to trigger requests into that network. This could grant the attacker access to services that are not meant to be publicly exposed, or that are running old and vulnerable software versions inside the private network.

### Execution

The execution tactic refers to techniques that may be used by a malicious adversary to gain execution access on pipeline resources – the pipeline itself or the deployment resources. Some of the techniques in this section contain explanations about the different ways to perform them, or what we call sub-techniques:

Poisoned pipeline execution (PPE) – Refers to a technique where an attacker can inject code to an organization’s repository, resulting in code execution in the repository’s CI/CD system. There are different sub-techniques to achieve code execution:

Direct PPE (d-PPE) – Cases where the attacker can directly modify the configuration file inside the repository. Since the pipeline is triggered by a new PR and run according to the configuration file – the attacker can inject malicious commands to the configuration file, and these commands are executed in the pipeline.
Indirect PPE (i-PPE) – Cases where the attacker cannot directly change the configuration files, or that these changes are not taken into account when triggered. In these cases, the attacker can infect scripts used by the pipeline in order to run code, for example, make-files, test scripts, build scripts, etc.
Public PPE – Cases where the pipeline is triggered by an open-source project. In these cases, the attacker can use d-PPE or i-PPE on the public repository in order to infect the pipeline.
Dependency tampering – Refers to a technique where an attacker can execute code in the DevOps environment or production environment by injecting malicious code into a repository’s dependencies. Thus, when the dependency is downloaded, the malicious code is executed. Some sub-techniques that can be used to achieve code execution include:

Public dependency confusion – A technique where the adversary publishes public malicious packages with the same name as private packages. In this case, because package search in package-control mechanisms typically looks in public registries first, the malicious package is downloaded.
Public package hijack (“repo-jacking”) – Hijacking a public package by taking control of the maintainer account, for example, by exploiting the GitHub user rename feature.
Typosquatting – Publishing malicious packages with similar names to known public packages. In this way, an attacker can confuse users to download the malicious package instead of the desired one.
DevOps resources compromise – Pipelines are, at the core, a set of compute resources executing the CI/CD agents, alongside other software. An attacker can target these resources by exploiting a vulnerability in the OS, the agent’s code, other software installed in the VMs, or other devices in the network to gain access to the pipeline.

Control of common registry – An attacker can gain control of a registry used by the organization, resulting in malicious images or packages executed by the pipeline VMs or production VMs.

### Persistence
The persistency tactic consists of different techniques that an attacker may use for maintaining access to a victim environment:

Changes in repository – Adversaries can use the automatic tokens from inside the pipeline to access and push code to the repository (assuming the automatic token has enough permissions to do so). They can achieve persistency this way using several sub-techniques:

Change/add scripts in code – we can change some of the initialization scripts/add new scripts, so they download a backdoor/starter for the attacker, so each time the pipeline is executing these scripts, the attacker’s code will be executed too.
Change the pipeline configuration – we can add new steps in the pipeline to download an attacker-controlled script to the pipeline before continuing with the build process.
Change the configuration for dependencies locations – to use attacker-controlled packages.
Inject in Artifacts – some CI environments have the functionality for creating artifacts to be shared between different pipeline executions. For example, in GitHub we can store artifacts and download them using a GitHub action from the pipeline configuration.

Modify images in registry – In cases where the pipelines have permissions to access the image registry (for example, for writing back images to the registry after build is done) the attacker could modify and plant malicious images in the registry, which would continue to be executed by the user’s containers.

Create service credentials – A malicious adversary can leverage the access they already have on the environment and create new credentials for use in case the initial access method is lost. This could be done by creating an access token to the SCM, to the application itself, to the cloud resources, and more.

### Privilege escalation

The privilege escalation techniques are used by an attacker to elevate the privileges in the victim’s environment, gaining higher privileges for already compromised resources:

Secrets in private repositories – Leveraging an already gained initial access method, an attacker could scan private repositories for hidden secrets. The chances of finding hidden secrets in a private repo are higher than in a public repository, as, from the developer’s point of view, this is inaccessible from outside the organization.

Commit/push to protected branches – The pipeline has access to the repository that may be configured with permissive access, which could allow to push code directly to protected branches, allowing an adversary to inject code directly into the important branches without team intervention.

Certificates and identities from metadata services – Once an attacker is running on cloud-hosted pipelines, the attacker could access the metadata services from inside the pipeline and extract certificates (requires high privileges) and identities from these services.

### Credential access

Credential access techniques are used by an attacker to steal credentials:

User credentials – In cases where the customer requires access to external services from the CI pipeline (for example, an external database), these credentials reside inside the pipeline (can be set by CI secrets, environment variables, etc.) and could be accessible to the adversary.

Service credentials – There are cases where the attacker can find service credentials, such as service-principal-names (SPN), shared-access-signature (SAS) tokens, and more, which could allow access to other services directly from the pipeline.

### Lateral movement

The lateral movement tactic refers to techniques used by attackers to move through different resources. In CI/CD environments, this may refer to moving to deployment resources, to build artifacts and registries, or to new targets.

Compromise build artifacts – As in other supply chain attacks, once the attacker has control of the CI pipelines, they can interfere with the build artifacts. This way, malicious code could be injected into the building materials before building is done, hence injecting the malicious functionality into the build artifacts.

Registry injection – If the pipeline is configured with a registry for the build artifacts, the attacker could infect the registry with malicious images, which later would be downloaded and executed by containers using this registry.

Spread to deployment resources – If the pipeline is configured with access to deployment resources, then the attacker has the same access to these resources, allowing the attacker to spread. This could result in code execution, data exfiltration and more, depending on the permissions granted to the pipelines.

### Defense evasion

Defense evasion techniques could be used by attackers to bypass defenses used in a DevOps environment and allow attacks to continue under the radar:

Service logs manipulation – Service logs enable Defenders to detect attacks in their environment. An attacker running inside an environment (for example, in the build pipelines) could change the logs to prevent Defenders from observing the attack. This is similar to an attacker changing the history logs on a Linux machine, preventing any observer from seeing the commands executed by the attacker.

Compilation manipulation – if an attacker wishes to leave no traces in the SCM service, the attacker may change the compilation process in order to inject the malicious code. This may be done in several ways:

Changing the code on the fly – Changing the code right before the build process begins, without changing it in the repository and leaving traces in it.

Tampered compiler – Changing the compiler in the build environment to introduce the malicious code without leaving any traces before that process begins.

Reconfigure branch protections – Branch protection tools allow an organization to configure steps before a PR/commit is approved into a branch. Once an attacker has admin permissions, they may change these configurations and introduce code into the branch without any user intervention.

### Impact

The impact tactic refers to the techniques an attacker could use for exploiting access to the CI/CD resources for malicious purposes, and not as another step in the attack, as these techniques could be noisy and easy to detect:

Distributed Denial-of-Service (DDoS) – An adversary could use the compute resources they gained access to in order to execute distributed denial of services (DDoS) attacks on external targets.

Cryptocurrency mining – The compute resources could be used for crypto mining controlled by an adversary.

Local Denial-of-service (DoS) – Once the attacker is running on the CI pipelines, the attacker can perform a denial service attack from said pipelines to customers by shutting down agents, rebooting, or by overloading the VMs.

Resource deletion – An attacker with access to resources (cloud resources, repositories, etc.) could permanently delete the resources to achieve denial of services.

### Exfiltration

The exfiltration tactic refers to different techniques that could be used by an attacker to exfiltrate sensitive data from victim environment:

Clone private repositories – Once attackers have access to CI pipelines, they also gain access to the private repositories (for example, the GITHUB_TOKEN can be used in GitHub), and therefore could clone and access the code, thus gaining access to private IP.

Pipeline logs – An adversary could access the pipeline execution logs, view the access history, the build steps, etc. These logs may contain sensitive information about the build, the deployment, and in some cases even credentials to services, to user accounts and more.

Exfiltrate data from production resources – In cases where the pipelines can access the production resources, the attackers will have access to these resources as well. Therefore, they can abuse this access for exfiltrating production data.

## DevOps posture management recommendations

When the DevOps scanners uncover deviations from security best practices within source code management systems and continuous integration/continuous delivery pipelines, Defender for Cloud outputs precise and actionable recommendations. These recommendations have the following benefits:

1) Enhanced visibility: Obtain comprehensive insights into the security posture of DevOps environments, ensuring a well-rounded understanding of any existing vulnerabilities. Identify missing branch protection rules, privilege escalation risks, and insecure connections to prevent attacks.

2) Priority-based action: Filter results by severity to spend resources and efforts more effectively by addressing the most critical vulnerabilities first.

3) Attack surface reduction: Address highlighted security gaps to significantly minimize vulnerable attack surfaces, thereby hardening defenses against potential threats.

4) Real-time notifications: Ability to integrate with workflow automations to receive immediate alerts when secure configurations alter, allowing for prompt action and ensuring sustained compliance with security protocols.

