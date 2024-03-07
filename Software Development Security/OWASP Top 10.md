# OWASP TOP 10 2023

## Cited from: https://owasp.org/www-project-top-ten/

## 1) Broken Access Control

### Access controls limit users to the resources and functionalities they are authorized to use, and broken access control is the term used when a system fails to enforce appropriate restrictions.

### This can happen for various reasons, including a misconfiguration, IDOR (Insecure Direct Object References) which is where an application exposes direct references to resources like files or database records, insecure session management, where flaws in session management can allow attackers to hijack users’ sessions, and others.

### Developers and system administrators should follow the Principle of Least Privilege here, which means only granting users the minimum set of permissions that are required for them to perform their tasks and nothing more.

### All user input should be validated and sanitized to prevent attackers from injecting malicious data, access controls should be applied to APIs, and authorization checked for every request.

### Regular security audits and code reviews are a must to identify and fix access control issues, and multi-factor authentication should be enforced to limit unauthorized access.

## 2) Cryptograhic Failures

### Cryptography is used to protect highly sensitive data like credit card numbers and PII while it’s in transit, but it can fail due to factors like weak encryption algorithms or short encryption keys which can make it easier for attackers to decrypt sensitive data.

### Other examples of cryptography failures include insecure password storage, insufficient transport layer security (which can lead to man-in-the-middle attacks), weak SSL/TLS protocols, and insecure cipher suites that can expose the web application to attacks.

### Implement regular security testing (including code reviews and vulnerability assessments) to identify and fix cryptographic weaknesses, and also consider using secure cryptographic libraries too.

## 3) Injection

### Injection attacks exploit vulnerabilities in input validation and inadequate data handling. Attackers inject data such as SQL queries, code snippets, or commands into web application forms or URLs. They allow adversaries to access sensitive data and manipulate an application’s behavior.

### Examples include:

#### 1) SQL Injection for database attacks

#### 2) Cross-Site Scripting (XSS): usually JavaScript-based browser attacks launched via infected web pages, leading to session hijacking, cookie theft, or other attacks on users.

#### 3) Command Injection: attackers inject malicious commands into system commands executed by the application, potentially gaining control of the server or executing unauthorized operations.

#### 4) LDAP Injection: attackers manipulate LDAP queries used for authentication and authorization to gain access.

#### 5) XML Injection: attackers insert malicious content into XML data, potentially disrupting the application’s parsing process to gain access.

#### 6) Server-Side Template Injection (SSTI): where attackers inject malicious code into server-side templates to execute code on the server.

## 4) Insecure Design

### Insecure design vulnerabilities occur when teams don’t adhere to security best practices, and they fail to adequately anticipate and evaluate potential threats during the code design phase of creating the application.

### An example of insecure design is an app that produces overly detailed error messages. If it reports on error conditions in too much detail and offers diagnostic clues about the application environment, or other associated data, it could be revealing potentially useful information to attackers. They could then use it to launch other attacks like path traversal or SQL injection.

### It’s important to mitigate design vulnerabilities by using consistent threat modeling to shut down known methods of attack.

## 5) Security Misconfiguration

###  Security misconfigurations encompass a variety of potential vulnerabilities, but these are the most common ones:

#### 1) Unpatched vulnerabilities

#### 2) Default configurations

#### 3) Unused pages

#### 4) Unprotected files and directories

#### 5) Unnecessary services

#### 6) Use of vulnerable XML files

### A common mistake that webmasters commit is leaving CMS (Content Management System) default configurations unchanged. While CMS apps are user-friendly, they can pose security risks for end-users. Many attacks are entirely automated and rely on exploiting default settings, which makes changing these settings during CMS installation crucial for mitigating a significant number of potential attacks.

### Adjusting settings to control comments, user access, user information visibility, and default file permissions can bolster security.

## 6) Vulnerable and Outdated Components

### Even the simplest of websites have many dependencies like frameworks, libraries, extensions, and plugins, and every one of them must be kept up to date. Attackers are actively looking for websites with vulnerable components which they can exploit to spread malware, launch phishing attacks, and more, so failing to install updates for whatever reason is a bad idea.

### The latest version of any software is going to contain the latest security updates, but if your website relies on a lot of dependencies that can be easier said than done. The first step to fixing this is to create an inventory that lists all the connected components in your environment and keeps you up to date on each one’s behavior.

## 7) Identification and Authentication Failures

### Authentication and identity management failures expose applications to the risk of malicious actors posing as genuine users. A session ID configured without a validity period can run and run. Weak passwords can be susceptible to guessing and with no rate limits imposed on login attempts automated attacks keep doing that until they succeed.

### To address these issues, implement multi-factor authentication (MFA) within applications. Also, developers should be made aware of the need to adhere to recommended password length, complexity, and rotation policies.

## 8) Software and Data Integrity Failures

### These are a type of design flaw. The complexity of modern architectures means that developers often add plugins and libraries to the pipeline from various sources without verifying their integrity. If any of them fail, this can leave applications susceptible to unauthorized information disclosure, system compromise, or malicious code insertion. This is another reason why it’s important to have an active inventory of all third-party and open-source plugins and libraries, along with continuous threat monitoring.

## 9) Security Logging and Monitoring Failures

### Poor logging and monitoring capabilities mean that incidents are missed and alerts aren’t generated, and they could remain unnoticed for long enough to do substantial damage.

### Login attempts and failures need to be logged, and logs need to be backed up in case of server failure. Logs need to be accurate so that monitoring systems can detect suspicious activities or raise timely alerts, and they also need to be protected against tampering.

### To mitigate vulnerabilities, record all login attempts (including failures), maintain copies of logs, use anti-tamper mechanisms, and test monitoring systems regularly.

## 10) Server-Side Request Forgery (SSRF)

### This vulnerability allows attackers to make unauthorized requests from the server to other internal or external resources. In SSRF attacks, the attacker can manipulate input fields or parameters in the application to trick the server into sending requests to arbitrary URLs, often without the user’s knowledge.

### Attackers can abuse this vulnerability to access sensitive data, interact with internal resources, or perform actions on behalf of the server, potentially leading to a complete compromise of the application or its infrastructure.

### To mitigate SSRF vulnerabilities, developers should follow best practices such as:

#### 1) Input Validation: Properly validate and sanitize user-supplied input to prevent malicious URLs or IP addresses from being used in requests

#### 2) Whitelisting: Implement whitelisting for allowed URLs or IP ranges to restrict the server’s ability to make requests to known safe resources.

#### 3) Firewall Rules: Configure firewalls and network settings to restrict outgoing requests from the server to specific resources and protocols.

#### 4) Use of Safe APIs: If the application needs to make requests to external resources, use safe APIs or specific endpoints that are intended for public access.

#### 5) Least Privilege: Ensure that the server has the least privileges necessary to access external resources to limit potential damage if an SSRF attack occurs.

