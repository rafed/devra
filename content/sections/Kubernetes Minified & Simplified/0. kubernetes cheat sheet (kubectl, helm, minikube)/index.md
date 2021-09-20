---
title: "#00 - Kubernetes CLI Cheat Sheet (kubectl, helm, minikube)"
date: 2021-06-29
tags: [cloud, kubernetes]
image: cover.png
---

This cheat sheet focuses on the most important CLI commands for Kubectl, helm and minikube CLIs.

But what are the differences between them you ask?

* **kubectl**: The most important CLI to learn. It is used to manage a Kubernetes cluster
* **helm**: Package manager for Kubernetes. It is sort of like _apt install_ in Linux but for installing services in Kubernetes clusters
* **minikube**: CLI for running Kubernetes locally

## 1. kubectl

#### Enable autocomplete

```bash
$ source <(kubectl completion bash) 
$ echo "source <(kubectl completion bash)" >> ~/.bashrc
```

#### Context and configuration

```bash
$ kubectl config current-context
$ kubectl config view

$ kubectl config set-context mia
$ kubectl config use-context mia
```

#### Run Yaml files / Make infrastructural changes

#####  Make a deployment

_Make sure to make a my-manifest.yaml file first!_

```bash
## This deploys our app to the Kubernetes cluster
$ kubectl apply -f ./my-manifest.yaml

# Compares the current state of the cluster against the state that the cluster would be in if the manifest was applied.
$ kubectl diff -f ./my-manifest.yaml
```

##### Create a virtual sub-cluster before making deployments

```bash
$ kubectl create ns name-of-namespace
$ kubectl apply -f ./my-manifest.yaml -n name-of-namespace
```

#### View resources

```bash
$ kubectl get deploy    # Shows deployments made
$ kubectl get service   # Shows services made
$ kubectl get pods      # Check the pods
$ kubectl get hpa       # Show horizontal pod autoscalers
$ kubectl get rs        # Show replica sets
```

Add ```--watch``` flag to watch updates in real time.

```bash
$ kubectl get deploy --watch
```

Use the name of pods/nodes to run the below.

```bash
$ kubectl describe nodes node-name
$ kubectl describe pods pod-name
$ kubectl describe deploy deployment-name
```

#### Storage

```bash
$ kubectl get pv              # Get persistent volumes
$ kubectl get pvc             # Get persistent volume claims
$ kubesctl describe pvc -n namespace
$ kubectl get storageClass    # or in short "sc"
```

#### Interact with Pods/Services

Sometimes it is useful to get inside a pod and execute shell commands.

##### Get shell in a pod

```bash
$ kubectl exec --stdin --tty pod-name -- /bin/bash
```

##### Access service with a proxy

```bash
# Port forward services to localhost (local-port:remote-port)
$ kubectl port-forward pod-name 3000:80
$ kubectl port-forward service/service-name 3000:80
```

##### Check logs of pods

```bash
$ kubectl logs pod-name -n namespace
```

#### Undo / Delete / Rollbacks

##### Get information about a deployment

```bash
$ kubectl rollout history deployment/frontend               # Check the history of deployments including the revision 
$ kubectl rollout status -w deployment/frontend             # Watch rolling update status of "frontend" deployment until completion
```

##### Restart a deployment / Rollback to a previous version

```bash
$ kubectl rollout restart deployment/frontend               # Rolling restart of the "frontend" deployment
$ kubectl rollout undo deployment/frontend                  # Rollback to the previous deployment
$ kubectl rollout undo deployment/frontend --to-revision=2  # Rollback to a specific revision
```

##### Delete services or deployments

```bash
$ kubectl delete svc/<service-name>
$ kubectl delete deployment/<deployment-name> 
```

## 2. Helm Commands

As an example, grafana (a browser based dashboard service) is deployed with helm. Don't use the following for deploying grafana. There are other variables that need to be set for using Grafana properly in production.

##### Add a repo to helm and update it

```bash
$ helm repo add grafana https://grafana.github.io/helm-charts
$ helm repo update
```

##### Install the service

```bash
$ helm install grafana grafana/grafana --set persistence.enabled=true,persistence.size=2Gi 

# Instead of installing, see the helm chart first
$ helm template grafana grafana/grafana --set persistence.enabled=true,persistence.size=2Gi 
```

##### Delete a release
```bash
$ helm delete grafana
```

## 3. Minkube Commands

After installation, use the following CLI commands to test out minikube.

```bash
$ minikube start        # Start minikube
$ minikube status       # Shows status
$ minikube delete       # WARNING! Deletes cluster
$ minikube dashboard    # Takes you to a browser based dashboard
$ minikube ip           # Shows ip of the minikube node
```

#####  First get the service name

```bash
$ kubectl get svc
```

##### Get a proxy to the service

```bash
$ minikube service <service-name>
$ minikube service <service-name> --url ## And paste the URL in the browser
```