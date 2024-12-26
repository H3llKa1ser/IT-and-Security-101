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



