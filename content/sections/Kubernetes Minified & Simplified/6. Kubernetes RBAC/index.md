---
title: "#06 - Kubernetes Role Based Access Control (RBAC)"
date: 2021-09-20
tags: [cloud, kubernetes]
image: feature.png
draft: true
---

No matter how powerful and versatile a system is, without proper security measures it cannot be very useful. Thankfully Kubernetes come with a lot of builtin security controls. In this post we're going to talk about how we can manage users, create roles, limit privileges, etc. 

The core logical components of RBAC are:

#### Entity

A group, user, or service account (an identity representing an application that wants to execute certain operations (actions) and requires permissions to do so).

#### Resource

A pod, service, or secret that the entity wants to access using the certain operations.

#### Role
Used to define rules for the actions the entity can take on various resources.

#### Role binding
This attaches (binds) a role to an entity, stating that the set of rules define the actions permitted by the attached entity on the specified resources.

There are two types of Roles (Role, ClusterRole) and the respective bindings (RoleBinding, ClusterRoleBinding). These differentiate between authorization in a namespace or cluster-wide.

#### Namespace
Namespaces are an excellent way of creating security boundaries, they also provide a unique scope for object names as the ‘namespace’ name implies. They are intended to be used in multi-tenant environments to create virtual kubernetes clusters on the same physical cluster.








Kubernetes RBAC is built into Kubernetes, and grants granular permissions to objects within Kubernetes clusters. Permissions exist as ClusterRole or Role objects within the cluster. RoleBinding objects grant Roles to Kubernetes users, Google Cloud users, Google Cloud service accounts, or Google Groups.

If you primarily use GKE, and need fine-grained permissions for every object and operation within your cluster, Kubernetes RBAC is the best choice.


IAM manages Google Cloud resources, including clusters, and types of objects within clusters. Permissions are assigned to IAM members, which exist within Google Cloud, G Suite, or Cloud Identity.

There is no mechanism for granting permissions for specific Kubernetes objects within IAM. For instance, you can grant a user permission to create CustomResourceDefinitions (CRDs), but you can't grant the user permission to create only one specific CustomResourceDefinition, or limit creation to a specific Namespace or to a specific cluster in the project. An IAM role grants privileges across all clusters in the project, or all clusters in all child projects if the role is applied at the folder level.

If you use multiple Google Cloud components and you don't need to manage granular Kubernetes-specific permissions, IAM is a good choice.



https://cloud.google.com/kubernetes-engine/docs/concepts/access-control