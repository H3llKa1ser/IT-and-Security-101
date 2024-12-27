# Kubernetes Hardening

## Pod Security best practice

 - Containers that run applications should not have root privileges

 - Containers should have an immutable filesystem, meaning they cannot be altered or added to (depending on the purpose of the container, this may not be possible) 

 - Container images should be frequently scanned for vulnerabilities or misconfigurations 

 - Privileged containers should be prevented  

 - [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and [Pod Security Admission](https://kubernetes.io/docs/concepts/security/pod-security-admission/)

## Secure network communications best practice

 - Access to the control plane node should be restricted using a firewall and role-based access control in an isolated network

 - Control plane components should communicate using Transport Layer Security (TLS) certificates

 - An explicit deny policy should be created

 - Credentials and sensitive information should not be stored as plain text in configuration files. Instead, they should be encrypted and in Kubernetes secrets

## Authentication and Authorisation

 - Anonymous access should be disabled 

 - Strong user authentication should be used 

 - RBAC policies should be created for the various teams using the cluster and the service accounts utilised 

## Logging best practices

 - Audit logging should be enabled 

 - A log monitoring and alerting system should be implemented

## General best practices

 - Security patches and updates should be applied quickly

 - Vulnerability scans and penetration tests should be done semi-regularly 

 - Any obsolete components in the cluster should be removed


### Breakdown on some of the security best practices

#### 1) RBAC

RBAC (Role-Based Access Control) in Kubernetes regulates access to a Kubernetes cluster and its resources based on defined roles and permissions. These permissions (permission to create/delete x resource, etc.) are assigned to users, groups or service accounts. RBAC is a good way to ensure the resources in your cluster can only be accessed by those who need to access it. RBAC can be configured using a YAML file (same as defining a resource) where specific rules can be defined by declaring the resource type and verbs. Verbs are the actions being restricted, such as 'create' and 'get'.

#### 2) Secrets Management

A Kubernetes secret is an object used to store sensitive information (like credentials, OAuth tokens or SSH keys). Secrets are a good way to ensure that sensitive data isn't leaked and allow for more control over how this information is used. Secrets are stored as a base64 encoded string, unencrypted by default. For security, it is best to configure encryption at rest. Another way to promote secure secrets management in your Kubernetes cluster is to configure the least privilege access to secrets using RBAC.

#### 3) PSA (Pod Security Admission) and PSS (Pod Security Standards)

Pod Security Standards are used to define security policies at 3 levels (privileged, baseline and restricted) at a namespace or cluster-wide level. What these levels mean: 

 - Privileged: This is a near unrestricted policy (allows for known privilege escalations)

 - Baseline: This is a minimally restricted policy and will prevent known privilege escalations (allows deployment of pods with default configuration)

 - Restricted: This heavily restricted policy follows the current pod hardening best practices

Pod Security Admission (using a Pod Security Admission controller) enforces these Pod Security Standards by intercepting API server requests and applying these policies.

## Security Benchmarks

### 1) CIS Security Benchmarks

Cluster hardening best practices change regularly as new vulnerabilities are introduced, old features are retired/new features are introduced, etc, so how do we keep up to speed on what these practices are? Thankfully, this is done by CIS (Centre for Internet Security), a non-profit organisation that helps collect and define standards that can be implemented as preventative measures against cyber attacks. They define these standards as "security benchmarks"; this way, your cluster can be checked against these benchmarks to check your level of security

CIS provides security benchmarks for many different technologies (including browser, database and cloud technologies).

Full benchmark document: https://www.cisecurity.org/benchmark/kubernetes

This document separates the cluster hardening practices into the different Kubernetes components, each providing a method of auditing and remediation. CIS Security Benchmarks are just one example of a cyber security baseline resource; it is one of the most commonly used along with STIG (Security Technical Information Guidelines) provided by DISA (US Department of Defence Systems Agency).

### 2) Kube-bench https://github.com/aquasecurity/kube-bench

This tool developed by Aqua Security can perform automated assessments to check if Kubernetes has been implemented using best cluster hardening practices.

Kube-bench can be installed in multiple ways, some of which include: 

 - Kube-bench can be run inside a pod but will need to be granted sufficient permissions to access certain directories/ config files and the host's PID namespace (The process ID namespace to check running processes)  

 - Run inside of a container

 - Run within a cloud provider service such as Azure's AKS (Azure Kubernetes Service) or Amazon's EKS (Elastic Kubernetes Service) 


