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

### Breakdown

apiVersion is set to v1 (the version of the Kubernetes API best used for this simple service example), and kind is set to service. For the metadata, we just called this service "example-nginx-service". The spec is where it gets more interesting, under 'selector', we have 'app: nginx'. This is going to be important going forward when we define our deployment configuration, as is the ports information, as we are essentially saying here: "This service will look for apps with the nginx label and will target port 80. An important distinction to make here is between the 'port' and 'targetPort' fields. The 'targetPort' is the port to which the service will send requests, i.e., the port the pods will be listening on. The 'port' is the port the service is exposed on. Finally, the 'type' is defined as ClusterIP (earlier, we discussed that there were multiple types of services, and this is one of them), which is the default service type.

### Example deployment YAML file

    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: example-nginx-deployment
    spec:
      replicas: 3
      selector:
        matchLabels:
          app: nginx
      template:
        metadata:
          labels:
            app: nginx
        spec:
          containers:
          - name: nginx
            image: nginx:latest
            ports:
            - containerPort: 80


### Breakdown

The first thing you might notice is that inside the 'spec' field, there is a nested field called 'template', which itself contains a 'metadata' and 'spec' field. We are defining a deployment which controls a ReplicaSet; here, in the outer 'spec' field, we tell Kubernetes we want 3 replicas (identical pods) in this ReplicaSet. This template field is the template that Kubernetes will use to create those pods and so requires its own metadata field (so the pod can be identified) and spec field (so Kubernetes knows what image to run and which port to listen on). Note that the port defined here is the same as the one in the service YAML. This is because the service's target port is 80 and needs to match. As well as this, in the outer 'spec' field, you can see we have also set the 'selector' field to have a 'matchLabels', which matches what we defined in the 'selector' field for the service YAML. This is so the service is mapped to the correct pods. With these two config YAML files, we have defined a deployment that controls a ReplicaSet that manages 3 pods, all of which are exposed to a service.

These config files are used to define the desired state of Kubernetes components; Kubernetes will constantly be checking this desired state against the current state of the cluster. Using the etcd (one of the control plane processes mentioned in an earlier task), Kubernetes populates these configuration files with the current state and does this comparison. For example, if we have told Kubernetes we want 3 nginx pods running, and it detects in the status that there are only 2 running pods, it will begin the actions to correct this.
