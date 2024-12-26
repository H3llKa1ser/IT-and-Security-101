# Configuration

## File format

 - 1) YAML
  
 - 2) JSON

### Required fields (YAML)

1) apiVersion: The version of the Kubernetes API you are going to use to create this object. The API version you use will depend on the object being defined. A cheatsheet for what API version to use for which object can be found here: https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-apiversion-definition-guide.html

2) kind: What kind of object you are going to create (e.g. Deployment, Service, StatefulSet).

3) metadata: This will contain data that can be used to uniquely identify the object (including name and an optional namespace).

4) spec: The desired state of the object (for deployment, this might be 3 nginx pods).

# Configuring resources

Those are the very basics of Kubernetes YAML configuration files. Let's consider those and look now at the two files mentioned above. We're going to take a look at the service config file first, as when defining a deployment and service, it is generally best practice to first define the service before the back-end deployment/replicaset that it points to (this is because when Kubernetes starts a container, it creates an env variable for each service that was running when a container started).

### Example service YAML file

    apiVersion: v1
    kind: Service
    metadata:
      name: example-nginx-service
    spec:
      selector:
        app: nginx
      ports:
        - protocol: TCP
          port: 8080
          targetPort: 80
      type: ClusterIP

  
