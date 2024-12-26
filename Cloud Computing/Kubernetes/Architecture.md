# Kubernetes Cluster Architecture

A Kubernetes cluster can be comprised of the components discussed below:

## 1) Kubernetes Pod


Pods are the smallest deployable unit of computing you can create and manage in Kubernetes. When you work in DevSecOps with Kubernetes, you'll hear a lot of this word. You can think of a pod as a group of one or more containers. These containers share storage and network resources. Because of this, containers on the same pod can communicate easily as if they were on the same machine whilst maintaining a degree of isolation. Pods are treated as a unit of replication in Kubernetes; if a workload needs to be scaled up, you will increase the number of pods running.

## 2) Kubernetes Nodes

Kubernetes workloads (applications) are run inside containers, which are placed in a pod. These pods run on nodes. When talking about node architecture, there are two types to consider. The control plane (also known as "master node") and worker nodes. Both of these have their own architecture/components, so let's take a look at them. Nodes can either be a virtual or physical machine. Think of it this way: if applications run in containers which are placed in a pod, nodes contain all the services necessary to run pods.

## 3) Kubernetes Cluster

At the highest level, we have our Kubernetes Cluster; put simply, a Cluster is just a set of nodes. 
