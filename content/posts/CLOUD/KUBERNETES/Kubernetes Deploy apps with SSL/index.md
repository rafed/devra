---
title: "Kubernetes: Deploy apps with SSL the Easy Way"
date: 2022-06-16
tags: [cloud, kubernetes]
image: kubernetes.png
---

Deploying apps in Kubernetes is not enough, you need to secure it with HTTPS. In this guide, I'll walk you through setting up SSL/TLS for your Kubernetes apps using cert-manager and Ingress NGINX Controller.

## Prerequisites

Before jumping in, make sure you have:

* A running Kubernetes cluster
* kubectl configured properly
* A domain name pointing to your cluster (if you want real SSL certs)

## Step 1: Install Cert-Manager

Cert-Manager automates the SSL cert process, so you don’t have to deal with renewals manually. It is simply a tool you install on your cluster to handle certificate renewals automatically. To install it, run:

```sh
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.8.2/cert-manager.yaml
```

Check if it’s running:

```sh
kubectl get pods -n cert-manager
```

## Step 2: Install Ingress NGINX Controller

The Ingress NGINX Controller is what routes traffic to your app. Install it like this:

```sh
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.3.1/deploy/static/provider/aws/deploy.yaml
```

Make sure it's up:

```sh
kubectl get pods -n ingress-nginx
```

## Step 3: Set Up a ClusterIssuer

For automatic SSL certs, configure a ClusterIssuer using Let’s Encrypt:

```yaml
apiVersion: cert-manager.io/v1
kind: ClusterIssuer
metadata:
  name: letsencrypt-prod
spec:
  acme:
    server: https://acme-v02.api.letsencrypt.org/directory
    email: your-email@example.com
    privateKeySecretRef:
      name: letsencrypt-prod
    solvers:
    - http01:
        ingress:
          class: nginx
```

Apply it:

```sh
kubectl apply -f cluster-issuer.yaml
```

## Step 4: Secure Your App with TLS

Now, create an Ingress resource for your app with SSL enabled:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: my-app-ingress
  annotations:
    cert-manager.io/cluster-issuer: "letsencrypt-prod"
spec:
  ingressClassName: nginx
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: my-app-service
            port:
              number: 80
  tls:
  - hosts:
    - myapp.example.com
    secretName: myapp-tls
```

Deploy it:

```sh
kubectl apply -f ingress.yaml
```

## Step 5: Verify SSL Cert

Check if your cert is good to go:

```sh
kubectl get certificate
```

If all is set up right, your app should now be reachable via HTTPS. 🎉

## Wrapping Up

With cert-manager and Ingress NGINX, SSL in Kubernetes is a breeze. No more non HTTP sites from your cluster!

