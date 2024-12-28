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
