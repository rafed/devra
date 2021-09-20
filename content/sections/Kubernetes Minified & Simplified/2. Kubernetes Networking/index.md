---
title: "#02 - Kubernetes Networking"
date: 2021-08-13
tags: [cloud, kubernetes]
image: cover.png
---

Kubernetes is a container orchestration platform. It is used to help containers in a cluster communicate between them in an easy way. This is where networking in Kubernetes kicks in. To understand how Kubernetes works, knowing its basic underlying networking concepts is a fundamental necessity.

The basic objects that communicate in the Kubernetes network are
* **Nodes**: real machines in the cluster
* **Pods**: containers that are encapsulated
    * They are the atomic unit in Kubernetes
    * A pod may contain multiple containers (even though they usually run only one)

Kubernetes networking is based on a **flat network structure** and does not require you to map ports between hosts and containers. This means:
* All nodes in the cluster have to be able to talk to each other.
* All pods can communicate without NAT.
* Every pod gets its own IP address.

The following diagram shows a generalized view of how Kubernetes networking is implemented.

![Kubernetes Networking](networking.png)


#### Kubernetes Networking Scenarios

There are four common networking scenarios

* Container-to-Container Networking (Handled by Pods)
* Pod-to-Pod Networking (Handled by Pods)
* Pod-to-Service Networking (Handled by Services)
* Internet-to-Service Networking (Handled by Services)
    
##### 1. Container-to-Container Networking

* This occurs between containers that are within the same pod.
* The containers in a pos share a single IP and port space.

##### 2. Pod-to-Pod Networking

This occurs between-
* Pods in the same node
* Pods across multiple nodes

##### 3. Pod-to-Service Networking (Handled by Services)

Kubernetes allows pods to be created and replaced dynamically. Thus, pods running a particular service will have varying IP addresses over time. To address this issue **services** are used.

Services abstract pod addresses by assigning a single virtual IP (a cluster IP) to a group of pod IPs. Then, any traffic sent to the virtual IP is distributed to the associated pods.

There are three ways to map services to pods-
* **ClusterIP** (default)
    * Gets own IP
    * Service accessible only from within the cluster
* **Nodeport**
    * Gets cluster-wide port
    * service accessible from outside of the cluster
* **Loadbalancer**
    * Integrates with a public cloud load balancer (e.g. AWS ELB, GCP CLB)  

##### 4. Internet-to-Service Networking (Handled by Services)

The final networking situation that is needed for most deployments is between the Internet and services. This connectivity enables end-users to access your services.

They are of two types-
* **Ingress**: Ingress routes traffic an outside connection to a service in your cluster
* **Egress**: Egress routes traffic from your node to an outside connection

That was all about the basics of networking in Kubernetes. Head over to the next section about [Kubernetes storage](../3.-kubernetes-storage).