---
title: Kubernetes Autoscaling
date: 2021-09-18
tags: [cloud, kubernetes]
image: autoscaling.png
---

In the previous blog post we deployed an nginx container with 3 replicas. Replicas allows us to upscale an application and increase its availability and performance. However, we generally want the replica count of a pod to be dynamic. When demand increases, number of pods should increase. And when demand decreases, the number of pods should decrease. 

When we say demand increases or decreases, it can mean a lot of different things. Most commonly they are:
* CPU
* Memory
* Messages in queues
* No of open connections

Depending upon the demand, we can perform scaling in three ways:
* Horizontal Pod Autoscaler (Add more pods)
* Cluster Autoscaler (Add more nodes)
* Vertical Pod Autoscaler


#### Horizontal Pod AutoScaler

A **horizontal pod autoscaler (HPA)** autoscaler increases the replica count in a deployment object. 

The following yaml definition attaches an autoscaler to a deployment:

```yaml
apuVersion: autoscaling/v1
kind: HorizontalPodAutoscaler
metadata: 
  name:
  namespace: 
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: nginx ## name of the deployment object
  minReplicas: 1
  maxReplicas: 10
targetCPUUtilizationPercentage: 50%

```

Autoscaling occurs based on _targetCPUUtilizationPercentage_. As per the example, when all the existing pods of a deployment have reached 50% usage, a new pod will be added to distribute the load. The addition of a new pod will happen until it reaches the _maxReplicas_ count which in our case is 10. The minReplicas enforce the minimum number of pods that should be kept running.

#### Cluster Autoscaler

If all the nodes in the cluster are full, then more pods cannot be added due to a lack of resources. By activating cluster autoscaling, nodes can be dynamically added or removed based on resource availability in the cluster. After nodes are added, pods can continue upscaling.

To activate Cluster autoscaling, make sure it is enabled when configuring Kubernetes with your cloud service provider. Usually, it is a checkbox or a dropdown field.

#### Vertical pod autoscaler

Vertical pod autoscaler adjusts the CPU/memory of a single pod based on the demand. For example, if a pod has 1 CPU allocated to it, when need arises, it can be allocated 2 CPUs. As of now, this is still in experimentation and a work in progress. Hopefully, it will soon become stable.