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


