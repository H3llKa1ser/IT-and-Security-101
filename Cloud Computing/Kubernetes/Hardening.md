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


## Kubelet Security

The kubelet component listens for requests on the following ports: 

 - Port 10250: Where it serves the kublet-api and allows for full access 

 - Port 10255: Where it serves another API which has unauthorised, unauthenticated read-only access

The kubelet-api is used to manage containers running on a node and, as mentioned, has full access; this makes it a prime target for hackers who could use this API to interact directly with the kubelet component and create containers of their own or delete containers running within the worker node. For this reason, it is critical that you should ensure that unauthorised traffic is locked down. 

The kubelet component should only respond to traffic which originates from the kube-apiserver. This can be done by making configuration changes to the kubelet config file. Note: To find out where the kubelet config file is located, run

    ps ef | grep kubelet

and find the directory in the --config flag. The first step to locking down unauthorised traffic is to disable anonymous traffic (this implements CIS security benchmark 4.2.1). We do this by setting authentication:anonymous:enabled to false. Like so: 

    apiVersion: kubelet.config.k8s.io/v1beta1
    authentication: 
      anonymous: 
        enabled: false 
      webhook: 
        cacheTTL: 0s 
        enabled: true 
      x509: 
        clientCAFile: /var/lib/minikube/certs/ca.crt


### 1) Kubelet Authentication

With anonymous traffic now restricted, the kubelet component will need to authenticate a request. This can be done using one of two methods: 

1) X509 Client Certificate Authentication: Kubelet will need to start with the --client-ca-file flag (providing a CA bundle to authenticate certificates with), separately for this method the apiserver component will have to be started with the --kubelet-client-certificate and --kubelet-client-key flags.

2) API Bearer Token: This is configured by setting authentication:webhook:enabled to "true". Kubelet will then need to start with the flags --authentication-token-webhook and --kubeconfig. The API group authentication.k8s.io/v1beta1 will also need to be enabled in the API server.

With either of those authentication methods implemented, the kublet component will no longer accept requests from unauthenticated sources, and the cluster is a bit more hardened! For example, if certificate authentication was enabled and a call was made to the kubelet component trying to list pods, it would be rejected as "unauthorised" unless the appropriate key and certificate were provided along with the request.

## API Traffic Security

Within a Kubernetes cluster, there are many components. These components need to communicate; Kubernetes is entirely API driven, meaning restricting this communication (who can access it, what they can do) should be the first line of defence. One way in which we can secure API traffic is through encryption.

