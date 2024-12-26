# Interaction with Kubernetes

## Tools: Kubectl (CLI), Kubernetes dashboard

We've just covered how to define the desired state of your cluster using YAML config files, but currently, those exist only as files. To take these from configurations to running processes, we need to interact with the cluster. We can do this by interacting with the apiserver component of the control plane using different methods: UI if using the Kubernetes dashboard, API if using some sort of script or command line using a tool called kubectl.

### Kubectl Commands:

#### 1) Kubectl apply

Once you have defined your deployment and service configurations in the YAML file, the next step would be to apply them so Kubernetes can take the desired configuration and turn it into a running process(s). This is done using the aptly named apply command.

    kubectl apply -f example-deployment.yaml

#### 2) Kubectl get

Once both configurations have been applied, you'll want to check the status of both to ensure things are running as expected. This would be done using the Kubectl get command. This is a very versatile command, and you will be using it a lot in your time with Kubernetes. The get command can be used to check the state of resources. The resource type will follow 'get', then -n or --namespace followed by the namespace (unless you are checking a cluster-level resource like a node).

    kubectl get pods -n example-namespace

As mentioned, this command can be used to check on a variety of resources such as deployments, services, pods, and ReplicaSets.

#### 3) Kubectl describe

This command can be used to show the details of a resource (or a group of resources). These details can help in troubleshooting or analysis situations. For example, say one of the pods in your cluster has started erroring out, and you want to get more information about the pod to try to determine why it has crashed. You would run the following command:

    kubectl describe pod example-pod -n example-namespace

You can see that the describe command details contain some "events". These events can help shine a light on what the issue is. For more details surrounding this event, Kubernetes captures logs from each container in a running pod.

#### 4) Kubectl logs

Say you want to view the application logs of the erroring pods. Maybe you want to view the logs surrounding the event error. For this, we would use the kubectl logs command. Here is an example of how this would be used:

    kubectl logs example-pod -n example-namespace

These logs can provide valuable insight not just for troubleshooting but for security analysis as well.  

#### 5) Kubectl exec

Now, let's say the log information was helpful, but there are still some unanswered questions, and you want to dig deeper and access the container's shell. The kubectl exec command will allow you to get inside a container and do this! If a pod has more than one container, you can specify a container using the -c or --container flag. The command for this is (the -it flag runs the command in interactive mode, everything after -- will be run inside the container): 

    kubectl exec -it example-pod -n example-namespace -- sh

From here, you can run any command you want from within the container itself. Maybe you want to snoop around for your security analysis or run a command to test connectivity from the container.

#### 6) Kubectl port-forward

Another handy command is kubectl port-forward. This command allows you to create a secure tunnel between your local machine and a running pod in your cluster. An example of when this might be useful is when testing an application. Let's imagine we have an nginx web application running across 3 pods which are exposed by a web application service. If you remember, a service makes a pod externally accessible. We take the port that is used to expose these pods and map it to one of our local ports. For example, matching the target port (the port the service is exposed on, which in our configuration example was 8080) to local port 8090 would make this web application accessible on our local machine at http://localhost:8090. The resources specified are resource-type/resource-name. This would be done using the kubectl port-forward command with the following syntax : 

    kubectl port-forward service/example-service 8090:8080
