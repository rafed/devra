---
title: MLT in Kubernetes (Monitoring, Logging, Tracing)
date: 2021-06-29
tags: [cloud, kubernetes]
image: kubernetes.png
---

**THIS IS YET TO BE COMPLETED**

Monitoring, Logging and Tracing (MLT) are the three trios that provide us with a way to observe the behavior and performance of a system. In a app deployed in kubernetes, MLT is very important as it can provide us with a way how each deployed node is behaving and performing. Without observing the system we cannot identify bottlenecks and potential problems that could arise in deployed apps.

In this article I'll show you how to implement MLT in Kubernetes using the following technologies:

1. Grafana: This is a central dashboard where every MLT data will be collected and displayed. All other apps
2. Prometheus [Monitoring]: This will collect system statistics (CPU, Memory, Bandwidth, etc)
3. Promtail [Logging]: This collects log data from containers
4. Loki [Logging]: This aggregates all logs collected by Promtail and forwards it to Grafana
5. Opentracing [Tracing]: ***
6. Jaeger [Tracing]: ***

## 1. Monitoring + Logging

#### Process 1

Execute the following commands

```bash
# Install prometheus
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm install prometheus prometheus-community/prometheus
kubectl expose service prometheus-server --type=NodePort --target-port=9090 --name=prometheus-server-np

# Install grafana
helm repo add grafana https://grafana.github.io/helm-charts

helm install  grafana grafana/grafana --set persistence.enabled=true,persistence.type=pvc,persistence.size=10Gi 

kubectl expose service grafana --type=NodePort --target-port=3000 --name=grafana-np

# Use the password provided by this to login
kubectl get secret --namespace default grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo

# Install loki
helm repo add loki https://grafana.github.io/loki/charts
helm repo update

helm upgrade --install loki loki/loki-stack --set grafana.enabled=true

helm install loki-stack grafana/loki-stack \  
                                --create-namespace \  
                                --namespace loki-stack \                                
    --set promtail.enabled=true,loki.enabled=true,loki.persistence.size=100Gi
```

# Process 2

Everythin in process 1 can be done in just this 1 step

```bash
helm upgrade --install loki grafana/loki-stack  --set grafana.enabled=true,prometheus.enabled=true,prometheus.alertmanager.persistentVolume.enabled=false,prometheus.server.persistentVolume.enabled=false,loki.persistence.enabled=true,loki.persistence.storageClassName=standard,loki.persistence.size=5Gi
```

## 2. Tracing

Coming soon!