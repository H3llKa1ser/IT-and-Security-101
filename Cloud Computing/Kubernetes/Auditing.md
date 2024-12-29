# Kubernetes Auditing

Kubernetes Auditing provides users/cluster administrators with a set of chronological records which document sequences of action in a cluster. These records are helpful in a security context as they record actions performed by users, applications (that use Kubernetes API) and the control plane itself that can provide valuable insights, answering questions like: 

1) When did it happen?

2) What happened?

3) On what did it happen?

4) To where was it going?

5) Where was it observed?

6) From where was it initiated?

7) Who initiated it?

In a typical production cluster, there are going to be A LOT of events. We're now going to take a look at how we can configure our cluster to capture specific events. Before doing this, though, we need to understand two terms that are critical when defining our criteria for an audit event: stages and levels.

### 1) Stages

An audit log can be captured at various stages of a request in the kube-apiserver component (where all requests are sent). The different stages are defined as follows:

#### 1) RequestReceived

The audit handler (in the kube-apiserver) has received the request, but no response has been generated yet.

#### 2) ResponseStarted

This is when the response headers have been sent out, but the response body hasn't. This stage will only be present for long-running requests such as “wait” (a Kubernetes command you can use to wait for a condition to be met, such as the running status of a resource).

#### 3) ResponseCompleted

When the response body has been completed and sent out.

#### 4) Panic

This is an event generated when a panic occurs (critical error causing failure)

 ### 2) Levels

 We use levels to tell Kubernetes how much event data we want to be captured in our audit log. There are four levels in total. As the level increases, more data is captured:

#### 1) None 

This tells Kubernetes not to log this request 

#### 2) Metadata

This tells Kubernetes only to log the request metadata 

#### 3) Request

This tells Kubernetes to log the request metadata and the request body

#### 4) RequestResponse

This tells Kubernetes to log the request metadata, request body and response body.

## Defining Audit Policy

Now that stages and levels have been defined, we are going to take a look at how we define what events we want to be audited (and what data should be included) in our Kubernetes cluster using an audit policy. The official Kubernetes documentation defines an example audit policy, which we can take a look at now:

        apiVersion: audit.k8s.io/v1 # This is required.
        kind: Policy
        # Don't generate audit events for all requests in RequestReceived stage.
        omitStages:
          - "RequestReceived"
        rules:
          # Log pod changes at RequestResponse level
          - level: RequestResponse
            resources:
            - group: ""
              # Resource "pods" doesn't match requests to any subresource of pods,
              # which is consistent with the RBAC policy.
              resources: ["pods"]
          # Log "pods/log", "pods/status" at Metadata level
          - level: Metadata
            resources:
            - group: ""
              resources: ["pods/log", "pods/status"]

          # Don't log requests to a configmap called "controller-leader"
          - level: None
            resources:
            - group: ""
              resources: ["configmaps"]
              resourceNames: ["controller-leader"]

          # Don't log watch requests by the "system:kube-proxy" on endpoints or services
          - level: None
            users: ["system:kube-proxy"]
            verbs: ["watch"]
            resources:
            - group: "" # core API group
              resources: ["endpoints", "services"]

          # Don't log authenticated requests to certain non-resource URL paths.
          - level: None
            userGroups: ["system:authenticated"]
            nonResourceURLs:
            - "/api*" # Wildcard matching.
            - "/version"

          # Log the request body of configmap changes in kube-system.
          - level: Request
            resources:
            - group: "" # core API group
              resources: ["configmaps"]
            # This rule only applies to resources in the "kube-system" namespace.
            # The empty string "" can be used to select non-namespaced resources.
            namespaces: ["kube-system"]

          # Log configmap and secret changes in all other namespaces at the Metadata level.
          - level: Metadata
            resources:
            - group: "" # core API group
              resources: ["secrets", "configmaps"]

          # Log all other resources in core and extensions at the Request level.
          - level: Request
            resources:
            - group: "" # core API group
            - group: "extensions" # Version of group should NOT be included.

          # A catch-all rule to log all other requests at the Metadata level.
          - level: Metadata
            # Long-running requests like watches that fall under this rule will not
            # generate an audit event in RequestReceived.
            omitStages:
              - "RequestReceived"
   
    
