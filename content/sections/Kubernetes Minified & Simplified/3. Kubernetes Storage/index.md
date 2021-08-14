---
title: Kubernetes Storage
date: 2021-08-14
tags: [cloud, kubernetes]
image: cover.png
---

Pods in Kubernetes are volatile. That means if a pod crashes or restarts then the data stored previously is lost. **Volumes** in Kubernetes decouple storage from pods and provides a method for persisting data.

For persistent storage in Kubernetes, we need to know 3 things.
1. **PV**: Persistent Volume
1. **PVC**: Persistent Volume Claim
1. **SC**: Storage Classes

#### 1. PV - Persistent Volume

A persistent volume is a disk attached to the cluster that can store data. To attach a PV to the cluster-
1. An administrator needs to provision the disk (from GCP, AWS, Azure)
2. Load the PV in the cluster by applying a YAML (YAML configuration may vary according to cloud providers)


```yaml
# File: pv.yaml
kind: PersistentVolume
apiVersion: v1
metadata:
  name: volume-name
  labels:
    type: local
spec:
  capacity:
    storage: 10Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: "/tmp/data"
```

Apply the configuration using-

```bash
$ kubectl apply -f pv.yaml
# Check the created PV
$ kubectl get pv
$ kubectl describe pv
```

#### 2. PVC - Persistent Volume Claim

To use a PV a pod needs PVC. A PVC can be created with the following YAML-

```yaml
# File: pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-name
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 4Gi
  volumeName: volume-name
```

Apply the configuration using-

```bash
$ kubectl apply -f pvc.yaml
# Check the created PV
$ kubectl get pvc
$ kubectl describe pvc
```

There are three basic ways a pod can access volumes-
1. RWO: Read write once
1. RWM: Read write many
1. ROM: Read only many

Retain policy is what a cluster does when a claim on a volume is released. It's of two types-
1. Retain
1. Delete

When creating PVC, keep the following in mind-
1. Not all volumes support all modes
1. A single volume can be opened in only one mode at a time
1. If the claim asks for more capacity than the PV then it won't bind and the claim will stay there as pending
1. A PV can have multiple PVC. A PVC can be used by multiple pods.
1. You cant have two active claims against a PV with different policies

Finally, attach the PVC to a pod-

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  volumes:
    - name: nginx-storage
      persistentVolumeClaim:
        claimName: pvc-name
  containers:
    - name: nginx-container
      image: nginx
      volumeMounts:
        - mountPath: "/var/www/html"
          name: pvc-name
```

#### 3. SC - Storage Class

Creating PV manually can be a lot of work. However, it can be done more easily with storage classes. 

Storage classes enable the dynamic provisioning of volumes. After creating one or more storage classes pods can use them based on demand.

Create a storage class (YAML will vary according to cloud providers)-

```yaml
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
  name: default
  annotations:
    storageclass.kubernetes.io/is-default-class: "true"
provisioner: kubernetes.io/aws-ebs
```

Check storage classes present in your cluster.

```bash
$ kubectl get sc
```

Now dynamically provision PV with a PVC.

```yaml
# File: pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-name
spec:
  storageClassName: default # or the storage class name
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 4Gi
```

Now use the PVC with a pod like you would regularly do.