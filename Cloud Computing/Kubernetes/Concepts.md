# Common Kubernetes Concepts

## 1) Namespaces

In Kubernetes, namespaces are used to isolate groups of resources in a single cluster. For example, say you want to group resources associated with a particular component, or if you are using a cluster to host multiple tenants, to group resources by tenant. Resources must be uniquely named within a namespace, but the same resource name can be used across various namespaces.

## 2) ReplicaSet

As the name suggests, a ReplicaSet in Kubernetes maintains a set of replica pods and can guarantee the availability of x number of identical pods (identical pods are helpful when a workload needs to be distributed between multiple pods). ReplicaSets usually aren't defined directly (neither are pods, for that matter) but are instead managed by a deployment, which brings us to our next concept.

## 3) Deployments

Deployments in Kubernetes are used to define a desired state. Once this desired state is defined, the deployment controller (one of the controller processes) changes the actual state to the desired state. Deployments provide declarative updates for pods and replica sets. In other words, as a user, you can define a deployment, let's say, for example, "test-nginx-deployment". In the definition, you can note that you want this deployment to have a ReplicaSet comprising three nginx pods. Once this deployment is defined, the ReplicaSet will create the pods in the background. 

## 4) StatefulSets

To understand what Kubernetes Statefulsets are, you must first understand the difference between stateful and stateless apps. Stateful apps store and record user data, allowing them to return to a particular state. For example, suppose you have an open session using an email application and read 3 emails, but your session is interrupted. In that case, you can reload this application, and the state will have saved, ensuring these 3 emails are still read. Stateless applications, however, have no knowledge of any previous user interactions as it does not store user session data. For example, think of using a search engine to ask a question. If that session were to be interrupted, you would start the process again by searching the question, not relying on any previous session data.

For these stateless applications (search engine example), deployments can be used to define and manage pod replicas. Because of the application's stateless nature, replicas can be created with random pod names, and when removed, a pod can be deleted at random.

However, this is not the case for stateful applications (email example), because stateful applications need to access and update the current state of the user session. Imagine this current state is being stored in a database running across 3 pods (meaning the database is replicated 3 times). Now, what happens when one of the databases is updated? This would leave 2 of the databases out of sync. This is where StatefulSets come in and is why you would use that instead of a deployment to manage stateful applications in Kubernetes. 

Statefulsets enable stateful applications to run on Kubernetes, but unlike pods in a deployment, they cannot be created in any order and will have a unique ID (which is persistent, meaning if a pod fails, it will be brought back up and keep this ID) associated with each pod. In other words, these pods are created from the same specification but are not interchangeable. StatefulSets will have one pod that can read/write to the database (because there would be absolute carnage and all sorts of data inconsistency if the other pods could), referred to as the master pod. The other pods, referred to as slave pods, can only read and have their own replication of the storage, which is continuously synchronised to ensure any changes made by the master node are reflected.

## 5) Services

To best understand services in Kubernetes, it's important to understand the problem they are solving. Kubernetes pods are ephemeral, meaning they have a short lifespan and are spun up and destroyed regularly. Imagine now a connection needs to be made to these pods. This could be from within the cluster; maybe a back-end application is running in these pods, and a front-end application needs to access them, or perhaps the request is coming from a browser, and these pods are running a web application. For this connection to happen, an IP address is required. If IP addresses were tied to pods, then these IP addresses would change frequently, causing all kinds of issues; services are used so that a single static IP address can be associated with a pod and its replicas. In other words, a service is placed in front of these pods and exposes them, acting as an access point. Having this single access point allows for requests to be load-balanced between the pod replicas. There are different types of services you can define: ClusterIP, LoadBalancer, NodePort and ExternalName.

## 6) Ingress

In the above section on Kubernetes services, we mentioned an example of an application which can be made accessible by using a service to expose the pods running this application (let's call this service A). Imagine now that this web application has a new feature. This new feature requires its own application and so has its own set of pods, which are being exposed by a separate service (let's call this service B). Now, let's say a user requests to access this new feature of the web application; there will need to be some kind of traffic routing in place to ensure this request gets directed to service B. That is where ingress comes in. Ingress acts as a single access point to the cluster and means that all routing rules are in a single resource. 

