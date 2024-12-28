# Pod Security Standards and Pod Security Admission (PSS and PSA)

### Pod Security Standards

Pod Security Standards in Kubernetes essentially define three levels of security you want to be enforced. These levels of security are (rather confusingly) referred to as 3 policies in the official Kubernetes documentation. These levels/policies outline different restrictions for different use cases. Let’s take a look at what they are: 

1) Privileged: As the name suggests, this is the most relaxed policy and is unrestricted, with the widest level of permission being granted. Known privilege escalations are allowed using this policy but they are intentional. Use Case: for a policy like this would be a system or infrastructure-level workload, which is managed by a trusted cluster administrator. 

2) Baseline: The baseline policy is designed for ease of adoption. It is a minimally restrictive policy that prevents known privilege escalations. A default pod definition would be allowed using this policy. Use Case: This policy is for application operators and developers working on non-critical applications. Some applications will need Baseline permissions to run as ‘Restricted’ since the latter would be too, well, restrictive.

3) Restricted: As it sounds, this policy is highly restrictive and follows current pod hardening best practices. However, this does come at a cost of compatibility. Use Case: This policy would be used in the development and running of security-critical applications. 

These are the 3 levels/policies which can be enforced, ensuring pods created follow a pre-defined standard so you can rest easy knowing what is being deployed into your cluster. Only how are these standards enforced?

### Pod Security Admission

Kubernetes has many built-in Admission Controllers, one of which is the PodSecurity Admission Controller. It is this admission controller that enforced the pod security standards outlined in the previous section and is what is being referred to when we discuss PSA (Pod Security Admission). If a PSS has been set, for example, against a namespace then the PodSecuirty Admission controller will be triggered upon any pod creation requests in this namespace. What the PodSecurity admission controller will do upon a violation of this standard will depend on the mode that has been selected. There are 3 modes:

1) Enforce: If a pod creation request violates the policy, the request will be rejected.

2) Audit: If a pod creation request violates the policy, the event will be recorded in the audit log. However, the request will be allowed, and the pod will be created.

3) Warn: If a pod creation request violates the policy, a user-facing warning will be triggered. However, the request will be allowed, and the pod will be created.

### PSA and PSS in a Kubernetes Cluster

Let’s consider a common use case; we have a non-critical application running in “example-namespace” and want to ensure all pods running in this namespace are protected against known privilege escalations, denying all pods that do not meet these standards. To enable these pod security standards at a namespace level, we can use labels. Kubernetes defines labels that you can set to determine which of the pre-defined Pod Security Standards you want to use in a namespace and what mode you want to use. Here is the syntax of the label:

    pod-security.kubernetes.io/<MODE>=<LEVEL>

#### Examples:

For example, if you wanted to set a baseline level and have it be enforced:

    pod-security.kubernetes.io/enforce=baseline

An optional label can also be included if you want to pin the version of the policy being enforced (or audited/warned) to the one included in a Kubernetes minor release (or the latest release). This could be done with:

    pod-security.kubernetes.io/enforce-version: v1.30

That's the format of the label, but how would we apply this label to our “example-namespace”? We can do this using a Kubectl command. 

    Kubectl label –dry-run=server –overwrite ns example-namespace \ pod-security.kubernetes.io/enforce=baseline

#### TIP: The dryrun option is not essential, but it is best practice, as it allows you to check if all running pods in the namespace you are labelling would be admitted with the security standard you are applying. Essentially you are trying to avoid an instance where an application pod in this namespace created before labelling restarts but gets denied as it does not meet the newly labelled security standards. If the dryrun command returns “<namespace> labelled” without any warnings, this means all pods running in this namespace would be admitted using the security standards you are about to apply. The command would then be run without the dryrun flag to label the namespace.

