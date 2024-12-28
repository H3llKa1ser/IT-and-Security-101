# Kubernetes API Request Stages

When you communicate with the Kubernetes API, you will be asking to do something, whether that be getting some logs, creating a pod or deleting a service. When you perform one of these actions, you will be sending a request to the API. This request will go through multiple stages before being actioned. Let's take a look at what those stages are: 

### 1) Authentication - Are you who you say you are?

Authenticating an API request can be done in multiple ways. These include methods such as setting up client certificate authentication or using API bearer tokens. Authentication can also be done using other auth plugins such as Authenticating Proxy or HTTP basic auth. Another authentication method would be ServiceAccount tokens, which are used to authenticate a Kubernetes ServiceAccount. Multiple authentication methods can be used, and it is often the case that at least two would be used (ServiceAccount Tokens and another auth plugin for user authentication). A request passes this stage only when it has the right attributes needed to confirm the requestee identity.  

### 2) Authorisation - Do you have permission to do what you are trying to do?

Once the requester's identity has been authenticated, it needs to be determined if this user/ServiceAccount is allowed to make this request (e.g., access this resource). For example, does user example-user have sufficient permissions to delete pod example-pod. The request needs to be authorised. Kubernetes has four authorisation modes. One commonly used is RBAC. There are three other authorisation modes:

#### 1) Node authorisation

A Kubernetes cluster has a kubelet process running in each node. This process communicates with the API. This authorisation method is used to authorise requests made by kublet processes. It is not intended for user authorisation.
 
#### 2) ABAC (Attribute Based Access Control)

 ABAC is similar to RBAC, but instead of granting authorisation based on roles, it grants access based on Attributes. These attributes include user attributes (such as name, position, clearance level, etc.), resource attributes (creation date, resource owner, resource group) or environmental attributes (such as the time and location from which the resource is being accessed). ABAC allows for a very granular level of access control; for example, you could allow a user to access a resource from one location (an office) but not another (their home). However, implementing this for a growing user base can quickly become complex, and the maintenance of ABAC policies can become difficult. This is often cited as a reason RBAC is favoured over ABAC for organisations: its implementation simplicity.
 
#### 3) Webhook

Another authorisation method is delegating the authorisation to an external http service (known as a webhook).  A webhook allows a user/organisation to define custom logic for authorisation and have API requests authorised using this logic. This is useful for organisations with more complex authorisation requirements or ones that want to defer to an external service (like Active Directory or LDAP, etc) to make authorisation decisions. The webhook would then send back a response based on the outcome.

Using one of the above methods, a request is checked to see if the authenticated user is authorised to access the resources/perform the action requested. Before the request is accepted, there is one more stage.

### 3) Admission Controllers - Does this request pass all checks?

After a request has been authenticated and authorised the next API request stage is Admission Controllers.  Admission Controllers are checks done against an API request. They can be validating (is this action permitted, does it breach a check) or Mutating (e.g. in a request to create a pod, the pod's name might need to be changed to match a custom naming convention). As well as built-in admission controllers, you may remember it is possible to define custom checks. These admission controllers are triggered after the authentication and authorisation stages, and only after all admission controller checks have been passed will this request persist.

We have followed an API Request through all of its stages. When asked how to restrict access to a Kubernetes cluster, you should now be able to elaborate more than just "harden your cluster" and discuss how a cluster is accessed and how access can be restricted at each stage.

# Accessing the Kubernetes API

Accessing the Kubernetes cluster is done through the use of the Kubernetes API. This is our communication channel to the cluster, and there are different methods of accessing the Kubernetes API itself: 

1) Kubectl - Kubectl is Kubernetes' command line tool. When accessing a cluster, you need to know two things: the cluster location and credentials. When configured, kubectl handles the locating and authenticating to the API server—making it easy to perform actions on the cluster using various kubectl commands. This is the most common method of accessing a Kubernetes cluster; however, if you wish to directly access the cluster yourself (using curl, wget or a browser), there are a couple of ways to do this, which will be discussed next.

2) Proxy - Kubectl can be run in "proxy mode" using the kubectl proxy command. This command will start a proxy server on port 8080 that will forward requests to the Kubernetes API server. This is the recommended method for directly accessing the Kubernetes API because it uses the stored API server location and verifies the identity of the API server using a self-signed certificate, meaning a man-in-the-middle (MITM) attack is not possible.

3) Auth Token - This method accesses the Kubernetes API directly by providing the HTTP client with the cluster location and credentials. For this reason, it is not recommended (as it would be vulnerable to a MITM attack). 

4) Programmatic - Kubernetes supports programmatic access to the API using client libraries. It officially supports client libraries such as Python, Java, Javascript, Go, and some community-supported libraries (although these do not have official Kubernetes support). 

