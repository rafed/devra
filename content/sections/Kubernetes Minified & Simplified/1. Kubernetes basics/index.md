---
title: Kubernetes Overview
date: 2021-08-10
tags: [cloud, kubernetes]
image: main.png
---

#### What is Kubernetes?

1. Kubernetes is an open source platform for running **cloud native apps**
1. Its a layer over Vms and provide a rich set of APIs for running cloud native apps

#### What are cloud native apps?

1. Cloud native apps are built of small interacting services that work together to do something useful
1. Making them small makes them easy to **scale** and **update** 

#### Prerequisites to learn Kubernetes?

Compulsory requirements-
* Container technology (Preferably Docker)

Optional requirements-
1. Concept of System design 
1. Orchestration (Docker-compose)

#### How to run Kubernetes?

Kubernetes clusters can be purchased from cloud providers-
* GKE: Google Kubernetes Engine
* AKS: Azure Kubernetes Service
* EKS: Elastic Kubernetes Service

However, they can be expensive and paying for learning is not worthwhile. Kubernetes can be run locally using
* Minikube
* Kind

#### How to work with Kubernetes?

**Kubectl** is a CLI that is used for managing and operating a Kubernetes cluster.

* The CLI makes requests to the K8s API server
* Everything in Kubernetes is a resource that is defined in the API
* The K8s APIs are CRUD style

Example Kubectl commands-

```bash
$ kubectl apply -f deployment.yml
$ kubectl get pods
$ kubectl get pv,pvc
```

#### Kubernetes Componenets

There are two types of Nodes in a Kubernetes cluster-
1. Master Nodes
1. Worker Nodes

##### Master Node
1. Hosts the control pane. This is where the Kubernetes magic happens.
1. It coordinates/manages nodes and pods in the cluster

In a managed Kubernetes cluster (GKE, AKS, EKS) the master node is not visible among the service nodes. It can be accessed only via the Kubernetes API. 

##### Worker Node
1. A Kubernetes cluster consists of a set of worker machines, called **nodes**
1. Every cluster has **at least one worker node**
1. The worker node(s) host the **Pods** that are the components of the application

#### How Kubernetes work?

The overall desired state of a cluster is defined in a **yaml file**. Then, Kubectl is used to post that yaml file to the cluster. This in turn kicks work pane nodes into action. Control panes constantly check whether the current state is in the desired state. When a mismatch is found from the current state with the desired state, the current state is updated.

#### Kubernetes Objects

The following are some Kubernetes objects.

1. A **Pod** is a wrapper for containers. Although Kubernetes mainly runs containers, pods are the atomic units in a K8s cluster. 
1. Pods are wrapped in a high level object called **Deployments**. This helps to-
    - make them _scalable_
    - make easier _rolling updates_
    - apply _rollbacks_
1. A **Daemonset** ensures that all (or some) Nodes run a copy of a Pod. As nodes are added to the cluster, Pods are added to them.
1. A **Volume** is a directory that contains data accessible to containers in a given Pod. Volumes make data stored by containers persistent.
1. A **Service** exposes an interface to a group of pods that perform the same function
1. A **Secret** is an object that contains a small amount of sensitive data such as a password, a token, or a key
1. **Namespaces** are a way to organize clusters into virtual sub-clusters 

Here's how different Kubernetes Objects map to a real world cloud native app.

![Kubernetes objects to application mapping](./object-to-app.png)

#### Application mapping with yaml file

Here is a sample yaml file that creates a **service** and **deployment** object in the cluster (for wordpress)

```yaml
apiVersion: v1
kind: Service
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  ports:
    - port: 80
  selector:
    app: wordpress
    tier: frontend
  type: LoadBalancer
---
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: wp-pv-claim
  labels:
    app: wordpress
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 20Gi
---
apiVersion: apps/v1 #  for k8s versions before 1.9.0 use apps/v1beta2  and before 1.8.0 use extensions/v1beta1
kind: Deployment
metadata:
  name: wordpress
  labels:
    app: wordpress
spec:
  selector:
    matchLabels:
      app: wordpress
      tier: frontend
  strategy:
    type: Recreate
  template:
    metadata:
      labels:
        app: wordpress
        tier: frontend
    spec:
      containers:
      - image: wordpress:4.8-apache
        name: wordpress
        env:
        - name: WORDPRESS_DB_HOST
          value: wordpress-mysql
        - name: WORDPRESS_DB_PASSWORD
          valueFrom:
            secretKeyRef:
              name: mysql-pass
              key: password
        ports:
        - containerPort: 80
          name: wordpress
        volumeMounts:
        - name: wordpress-persistent-storage
          mountPath: /var/www/html
      volumes:
      - name: wordpress-persistent-storage
        persistentVolumeClaim:
          claimName: wp-pv-claim
```

