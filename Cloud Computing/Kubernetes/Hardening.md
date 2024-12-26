# Kubernetes Hardening

## Pod Security best practice

 - Containers that run applications should not have root privileges

 - Containers should have an immutable filesystem, meaning they cannot be altered or added to (depending on the purpose of the container, this may not be possible) 

 - Container images should be frequently scanned for vulnerabilities or misconfigurations 

 - Privileged containers should be prevented  

 - [Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/) and https://kubernetes.io/docs/concepts/security/pod-security-admission/
