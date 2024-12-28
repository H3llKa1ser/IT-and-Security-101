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

### 1) Understanding Kubernetes API communication

Kubernetes expects all API communication in the cluster to be encrypted by default, with most installation methods supporting the creation and distribution of certificates to cluster components. Before implementing TLS encryption and distributing the certificates, we should establish if a component acts as a client or a server (or both) when communicating in the cluster. Understanding this will help determine which certificate should be generated for each component.

### 2) Certificate Generation and Implementation in Kubernetes

That's Kubernetes API communication in a nutshell; it can be a lot, but understanding these components and the nature of their communication is key to being able to secure it. With this foundational understanding, you can start creating your certificates. First, you would generate a CA (Certificate Authority) cert, which must be present on each component to validate the certificates received. Then, each of the components identified above, such as a client or a server, would need a certificate generated for them. Note that in the case of the kube-apiserver which acts as a server and a client, you can choose to use the same certificates for all communication or to make separate certificates for server communication, etcd client communication and kubelet client communication). 

The certificate creation step would be done using a tool like OpenSSL to first generate the CA certificate, then generate a certificate for each of the components using the following steps:

1) Generate a private key

       openssl genrsa --out ca.key 2048

2) Generate a CSR (Certificate Signing Request)

       openssl req --new --key ca.key --subj "/CN=192.168.0.100" --out ca.csr

3) Generate certificate (signing with CA cert and private key)

       openssl x509 --req --in ca.csr --signkey ca.key --out ca.crt --days 365

#### Some further considerations need to be made when, for example, dealing with components like kube-apiserver, which has alternate names (so we can connect to it using alternate routes such as kubernetes.default and kubernetes.default.svc, etc.), but generally, these steps can be followed to generate certs for each of the components.

https://blog.yarsalabs.com/kubernetes-cluster-from-scratch-part2/

Once the certificates have been generated, the corresponding Kubernetes components need to be configured for use. This is done by adding these configurations to the component YAML file. Here is an example of a code block from the kube-apiserver config YAML could look like with certs generated and defined:

    spec:
      containers:
      - command:
        - kube-apiserver
        - --*******************
        - --*******************
        - --client-ca-file=/var/lib/certs/ca.crt
        - --etcd-cafile=/var/lib/certs/etcd/ca.crt
        - --etcd-certfile=/var/lib/certs/apiserver-etcd-client.crt
        - --etcd-keyfile=/var/lib/certs/apiserver-etcd-client.key
        - --kubelet-client-certificate=/var/lib/certs/apiserver-kubelet-client.crt
        - --kubelet-client-key=/var/lib/certs/apiserver-kubelet-client.key
        - --proxy-client-cert-file=/var/lib/certs/front-proxy-client.crt
        - --proxy-client-key-file=/var/lib/certs/front-proxy-client.key
   

Implementing TLS encryption like this will implement CIS security benchmarks 1.2.24 - 27, hardening the cluster even further. However, note that when these certificates have been created and distributed, they have a validity date. This means that, at some point, these certificates will have to be rotated. As you can probably tell, this process can become quite time-consuming. To help with this, Kubernetes made the Kubernetes Certificate API. This API can be used to create CSRs and have them approved to generate certificates. In a production environment, these actions will likely be protected by RBAC having ClusterRoles for users to create CSRs and for admins to approve CSRs. 

## Admission Controllers

They intercept a request after authentication/authorisation (but before an object is created) and perform checks to see if the request should be allowed. Think of it like a bouncer at a nightclub, checking the ID of a potential customer. Sure, their ID is valid, but considering they can't walk in a straight line, should they be let in? 

Admission controllers have two characteristics. They can be one, the other or both. The characteristics are:

 - Mutating: This means the admission controller can modify the object related to the request they admit. For example an admission controller which ensures a pod configuration is set to a certain value. The admission controller would receive the request to create a pod and change (or mutate) this configuration value before persistence.

 - Validating: This means the admission controller validates the request data to approve or deny the request. For example, if the admission controller receives a request to create a pod but doesn't have a specific label, it is rejected.

The actual check done by the admission controller depends on which admission controller it is. You can think of admission controllers in two groups: Built-in admission controllers and custom user defined admission controller webhooks.

### 1) Built-in

Kubernetes comes with many built-in admission controllers, which are compiled into the kube-apiserver binary and, therefore, can only be configured by a cluster administrator. Some examples of built-in admission controllers and what their function/check is: 

1) AlwaysPullImages: This admission controller modifies all new pods and enforces the "Always" ImagePullPolicy. As a DevSecOps engineer, this is the kind of AdmissionController you want to enable as it ensures that pods always pull the latest version of the container image while mitigating supply chain attacks. Enabling implements CIS Security Benchmark 1.2.11.

2) EventRateLimit: This admission controller helps avoid a problem where the Kubernetes API gets flooded with requests to store new events. Setting this limit implements CIS Security Benchmark 1.2.9.

3) ServiceAccount: Again, this admission controller is strongly recommended to be enabled (by Kubernetes themself); it ensures that default service accounts are created for pod which don't specify one. This prevents pods from running without an associated service account which can lead to privilege escalation. Enabling implements CIS Security Benchmark 1.2.13.

These built-in admission controllers are implemented by editing the kube-apiserver YAML file (kube-apiserver will need to be restarted after doing this):

    apiVersion: v1
    kind: Pod
    metadata:
     name: kube-apiserver
     namespace: kube-system
    spec:
     containers:
     - name: kube-apiserver
       command:
       - kube-apiserver
       - --admission-control=AlwaysPullImages

### 2) Admission Controller Webhooks

These built-in admission controllers can be very helpful for ensuring that your cluster meets pre-defined security standards followed by other organisations. However, what if your organisation wants to enforce custom security standards or bespoke pod deployment checks specific to its organisation, like namespace syntax? This is done using admission controller webhooks.

You define this custom admission controller webhook, which will contain the logic for the check. If defining a validating admission controller webhook, the logic will define admission or rejection conditions. If defining a mutating admission controller webhook, the logic will define changes that need made to the object/resource before persistence. The admission controller webhook would then be deployed as a service (or other method which ensures it has a HTTP endpoint). Now these custom admission controllers webhooks are not added to the kube-apiserver directly (for security/isolation reasons) but rather are called upon by one of two built-in admission controllers (depending on their logic

1) ValidatingAdmissionWebhook

2) MutatingAdmissionWebhook

Both of these built-in admission controllers act as an intermediary between the custom admission controller and the kube-apiserver. For example, if a custom validating admission controller was defined and exposed on an HTTP endpoint, that endpoint would be added to the ValidatingAdmissionWebhook (a resource which you create) along with any other parameters, such as TLS configuration. 

When Kubernetes then receives an API request (to create, update or delete resources), it invokes the enabled admission webhooks. The endpoint URLs in these webhooks will send the request and will produce a response to the API (if validating a pass or rejection with error messages. If mutating maybe an altered object.). For example, imagine you have defined a custom mutating admission controller to enforce a namespace format; this is what that might look like.


    apiVersion: admissionregistration.k8s.io/v1
    kind: MutatingWebhookConfiguration
    metadata:
      name: my-mutating-webhook
    webhooks:
    - name: my-mutating-webhook.example.com
      clientConfig:
        service:
          name: pod-name-admission-controller-service
          namespace: default
          path: "/mutate"
        caBundle: 
      admissionReviewVersions: ["v1"]
      rules:
      - operations: ["CREATE", "UPDATE"]
        apiGroups: [""]
        apiVersions: ["v1"]
        resources: ["pods"]

Admission controllers can be used to harden Kubernetes clusters to ensure that authorised requests are checked against and security best practices are enforced. 
    
## Network Policies


A NetworkPolicy is a Kubernetes resource which is used to limit what Kubernetes entity (service/endpoint) a pod can communicate with. They are deployed at a namespace level so that traffic can be restricted between namespaced resources (such as pods) or between namespaces themself.  Here is an example of how we can define a NetworkPolicy to restrict traffic so the database only accepts ingress traffic from port 8080 (the API): 

    apiVersion: networking.k8s.io/v1
    kind: NetworkPolicy
    metadata:
      name: db-ingress-policy #policy name
    spec:
      podSelector:
        matchLabels:
          app: database #label of app you want to protect
      policyTypes:
      - Ingress
      ingress:
      - from:
        - podSelector:
            matchLabels:
              app: api #label of app you want to allow traffic from
        ports:
        - protocol: TCP
          port: 8080 #port you want to allow traffic on



We define the app we want to protect under the spec:PodSelector:matchLabels:app field (this will match the app's label defined in the database service spec). Since we only want to let traffic into this database (and not out), we set the spec:policyTypes field to simply "Ingress" However, if we were allowing for both, we would also include "Egress". Finally under the spec:ingress field we declare which service we want to accept traffic from and on what port (and which protocol). You then apply this NetworkPolicy YAML as you would any other configuration using the

    kubectl apply -f <network-policy-name>.yaml 

command, and there you have it! You have restricted network traffic into your database service. Note that defining NetworkPolicies in all namespaces implements CIS security benchmark 5.3.2.

## Role-Based Access Control (RBAC)

Let's define what four different Kubernetes objects that can be defined when implementing RBAC: 

1) Role: What can this role do, and to what resource(s)? Permissions are additive, meaning there are no deny permissions. Think of this as allowlisting for API access. You will provide a verb (what can this role do), e.g. "get" or "delete", and a resource (and to what), e.g. "pods" or "secrets". Note that sub-resources can also be defined here using a / after the resource name, e.g. pods/log. This will be visualised with a configuration example soon. Roles are namespaces, meaning they can allow actions within a given namespace, not the entire cluster.

2) RoleBinding: The RoleBinding object does what it says on the tin. It binds a Role (defined above) to a ServiceAccount or User. As Roles are namespaced, the role mentioned in the RoleBinding configuration YAML will need to exist in the same namespace as the RoleBinding.

3) ClusterRole: A ClusterRole is functionally the same as a Role, except roles are granted on a (non-namespaced) cluster level. This would be used if access is needed to cluster-level resources like nodes or resources across multiple namespaces. Again, only if this is NEEDED, with least privilege in mind.

4) ClusterRoleBinding: A ClusterRoleBinding is functionally the same as a RoleBinding except it binds a ClusterRole to a ServiceAccount or user.  

### 1) RBAC in context

Now that we've established the different kinds of RBAC objects, let's give some more context as to where these would be used. As mentioned, roles can be bound to either ServiceAccounts or Users. ServiceAccounts will be used if we are granting authorisation to an application, e.g. an application running in a pod within the cluster or a 3rd party external service. Meanwhile, users will be used if we are granting authorisation to, you guessed it, users! Let's now look at RBAC in the context of both of these.

| **Category**             | **Role/RoleBinding**                                                                 | **ClusterRole/ClusterRoleBinding**                                                             |
|--------------------------|--------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------|
| **ServiceAccount**        | A Role and RoleBinding allow an application/pod to perform actions on namespaced resources. For example, allowing a pod to get running pods in a namespace, with the ServiceAccount assigned to the pod. | Same as Role/RoleBinding but for actions on cluster-level resources, like a node.              |
| **Users**                 | A user, like "Bob," is granted permissions (e.g., "get" pods) in a specific namespace, like "dev," using a Role to ensure limited access to resources within that namespace. | A user, like "Alice," who needs to perform actions at the cluster level (e.g., "create" resources across all namespaces) is granted a ClusterRole with a ClusterRoleBinding. |


### 2) Defining RBAC

 Let's say we have a pod that is supposed to check the running status of pods in the "example-namespace" namespace. The pod identifies as ExampleServiceAccount. The pod definition YAML may look something like this: 

     apiVersion: v1
     kind: Pod
     metadata:
       name: up-checker
       namespace: example-namespace
     spec:
       serviceAccountName: ExampleServiceAccount
       containers:
       - name: kubectl
         image: bitnami/kubectl:latest
         command:
       # commands for pod status check logic would go here

We then want to ensure that this pod has only the permissions required to perform this upcheck. To do this, we would first define a Role, looking something like this:  

    apiVersion: rbac.authorization.k8s.io/v1
    kind: Role
    metadata:
      name: up-checker-role
      namespace: example-namespace
    rules:
    - apiGroups: [""]
      resources: ["pods"]
      verbs: ["get", "list", "watch"]

 This role allows get, list, and watch verbs to be used ONLY on pods and ONLY in the example-namespace namespace. Next, we would need to bind this role to a user or ServiceAccount. Since our pod used the ServiceAccount ExampleServiceAccount, we want to bind this ServiceAccount to the up-checker-role. To do this, we would define a RoleBinding like so: 

     apiVersion: rbac.authorization.k8s.io/v1
    kind: RoleBinding
    metadata:
      name: up-checker-role-binding
      namespace: example-namespace
    subjects:
    - kind: ServiceAccount
      name: ExampleServiceAccount
      namespace: example-namespace
    roleRef:
      kind: Role
      name: up-checker-role
      apiGroup: rbac.authorization.k8s.io

 Here, we tell Kubernetes the subjects (or, in this case, a single subject) to which we want to bind this role (the ServiceAccount ExampleServiceAccount) and what role we would like to bind this subject to (up-checker-role). Remember we can apply each configuration YAML using the following command:

    kubectl apply -f filename.yaml

#### TIP: Defining a ClusterRole/ClusterRoleBindng is almost identical, except there is no need to define a namespace and the "kind" would changed to ClusterRole/ClusterRoleBindng.



