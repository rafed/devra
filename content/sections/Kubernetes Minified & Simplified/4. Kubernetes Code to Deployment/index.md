---
title: "#04 - Kubernetes: From Writing Code to Deploying in Kubernetes"
date: 2021-09-07
tags: [cloud, kubernetes]
image: cover.png
mermaid: true
---

A typical Kubernetes workflow follows the following steps-

1. Write code
1. Containerize app
1. Send to container registry
1. Deploy to Kubernetes

<div class="mermaid">
    graph TD
    A[Write Code] --> B
    B[Containerzie app] --> C
    C[Send to container registry] --> D[Deploy to Kubernetes]
</div>

#### 1. Write Code

This step is pretty self explanatory. We write code that solves a business problem. For microservices/distributed systems we write code in multiple small cohesive services so that they can be deployed independently.

#### 2. Containerize App

Containers make deployment easy as it contains both the code and the environment needed for running. Containers are at the heart of Kubernetes because Kubernetes essentially runs and manages containers. Although containerization can be done manually, it is preferred to be done automatically through a CD pipeline. Creating a CD pipeline ensures that whenever code is pushed, a new container with the updated code is built.

#### 3. Send to container registry

After building a container it needs to be sent to a container registry. A container registry is like a vault where containers can be stored. Just as Github stores code, a container registry stores containers. Sending containers to a registry is necessary because when a Kubernetes deployment is made, the cluster pulls containers from the registry.

#### 4. Deploy to Kubernetes

Finally, a deployment is made to the Kubernetes cluster. A YAML file containing the desired state of the cluster is defined and pushed to the Kubernetes engine. The Kubernetes engine pulls the containers from the registry to run and changes the cluster configuration to match the desired state mentioned in the YAML files.

## Theory of Deployments

In Kubernetes, a _deployment_ determines how many Pods are to be deployed and how many ReplicaSets should be made. The relation between containers, pods, replicasets and deployments can be summarized by the following diagram.

![Kubernetes Deployment object](./deployment.png)

Code is placed in Containers. Containers are kept in Pods. How many replicas of a Pod should run is determined by replicasets. And all of this is defined in a deployment.

A deployment yaml will typically have a configuration like the following:


```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  minReadyseconds: 300
  replicas: 3
  strategy:
    rollingupdate :
        maxSurge: 1       
        maxUnavailable: 0 
    type: RollingUpdate
  template:
    metadata:
      labels:
      app: nginx
  spec:
    containers:
    - name: nginx
      image: nginx:1.14.2
      ports:
        - containerPort: 80
```

What some of these fields mean are described below:

* **minReadySeconds**: minimum number of seconds for which a newly created Pod should be ready without any of its containers crashing, for it to be considered available
* **maxSurge**: maximum number of Pods that can be created over the desired number of Pods
* **maxUnavailable**: maximum number of Pods that can be unavailable during the update process

A deployment isn't accessible unless a **service** is attached to it (recall from the [networking section](../2.-kubernetes-networking/)). Let's make the above deployment available though a service.

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-deployment
  labels:
    run: nginx
spec:
  ports:
  - port: 80
    protocol: TCP
  selector:
    run: nginx
```

Now the deployed nginx service can be accessed and used.

That was all about how you can deploy your code to Kubernetes. Head on to the next section to learn about how you can [autoscale pods](../5.-kubernetes-auto-scaling).