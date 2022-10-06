---
title: "Kubernetes: Deploy apps with SSL"
date: 2021-06-16
tags: [cloud, kubernetes]
image: kubernetes.png
draft: true
---

kubectl apply -f https://github.com/cert-manager/cert-manager/releases/download/v1.8.2/cert-manager.yaml

kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.3.1/deploy/static/provider/aws/deploy.yaml