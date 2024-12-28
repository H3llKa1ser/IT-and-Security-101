# Kubernetes ServiceAccount (sa)


One of the most important security practices in Kubernetes is the efficient and secure implementation of access control. Service Accounts are a part of the Access Control puzzle you'll need to complete to understand how to implement. "Service account" is a general term that you may be familiar with if you use other cloud technologies. 

Service accounts can be thought of as digital identities or non-human accounts. In Kubernetes, this identity is used in a security context to associate an identity with a specific process. In other words, Kubernetes system components, application pods, or other entities, both inside and outside of the cluster, can use ServiceAccount credentials to identify as this ServiceAccount. From a security perspective, this means API authentication can take place or, as just mentioned, identity/access control can be implemented using these ServiceAccounts. 

### ServiceAccounts vs Users

| **Category**               | **ServiceAccounts**                                    | **Users**                                            |
|----------------------------|--------------------------------------------------------|------------------------------------------------------|
| **Managed by**              | K8s                                                    | Managed outside of K8s                               |
| **Created by the API**      | Yes                                                    | No                                                   |
| **Kubernetes Object**       | There is no “User” Kubernetes Object                  | N/A                                                  |
| **Associated Credentials**  | Stored as Secrets                                      | N/A                                                  |
| **Creation via API**        | Can be created by the API                             | Cannot be created by API                             |

Essentially, user access is usually handled using some kind of account management solution. Kubernetes does have one built-in, but this is generally integrated with another user management system such as LDAP or AD. Non-human access to the cluster and its resources is handled using Kubernetes ServiceAccounts.

ServiceAccounts are characterised by the following attributes:

#### 1) Lightweight

Kubernetes ServiceAccounts allow you to create an account associated with a specific task/process in your Kubernetes cluster. This saves many of the headaches that come with using a user account to run processes (with special systems and business logic tied to databases involved in user account creation) and makes it easier to define more granular, task-specific permissions following the principle of least privilege.

#### 2) Namespaced

 In Kubernetes, ServiceAccounts are a namespaced resource, meaning ServiceAccount names need only be unique within the namespace they are associated with. Every namespace, upon creation, gets a default ServiceAccount associated with it aptly named "default". Suppose you don't manually define a ServiceAccount in the pod/deployment definition. In that case, this "default" ServiceAccount (in the namespace the pod is being created in)  will be assigned to it, and the ServiceAccounts credentials (a token) will be mounted to it as a secret. Note that the "default" ServiceAccount has few permissions by default, so if a task needs more, a ServiceAccount will need to be created. 

 #### 3) Portable

Because ServiceAccounts are lightweight and only need to be unique at a namespace level, they can be bundled together for use in other namespaces or projects, making them portable.

### Example use cases

 - A task/process running in a pod needs to communicate with the API to retrieve secret or sensitive information. A ServiceAccount could be used here to grant read-only access to this secret. 

 - You have a pod running in "example-namespace". Its process involves ensuring all pods are running in "other-namespace." A ServiceAccount can be used here, with a combination of RBAC (more on this soon), to ensure this pod has sufficient permissions to list pods in "other-namespace". 

 - ServiceAccounts can be used to authenticate external services. For example, imagine you have a CI/CD pipeline, and a stage in this pipeline involves authentication to your Kubernetes cluster.


### Creating and Configuration of ServiceAccounts

ServiceAccounts are very easy to define using kubectl. You can create a ServiceAccount on your cluster using the following command.


    kubectl create serviceaccount example-name --namespace example-namespace

#### TIP: serviceaccount can be abbreviated as sa

If you wanted this ServiceAccount to be associated with a specific pod, you would define that in the pod/deployment configuration YAML like so:

    apiVersion: v1
    kind: Pod
    metadata:
      name: example-pod
      Namespace: example-namespace
    spec:
      serviceAccountName: example-sa
      containers:
      - name: example-container
        image: nginx:latest
        ports:
        - containerPort: 80

