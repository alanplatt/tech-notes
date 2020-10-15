---
title: "Kubernetes apiGroups - Quick ref"
date: 2019-12-04T12:40:16Z
draft: false
toc: false
images:
tags:
  - kubernetes
  - RBAC
  - apiGroups
  - ClusterRole
---

### Get a list of apiGroups and appropriate verbs
```kubectl api-resources -o wide```

### Core apiGroup
Using the above command will give a list of apiGroups that can be used.
The `core` apiGroups do not have an apiGroup label and are represented by "" in k8s configuration YAMLs
```
Some example api groups
apiGroups: [""] #Core
apiGroups: ["extensions"]
apiGroups: ["apps"]
apiGroups: ["batch"]
apiGroups: ["autoscaling"]
apiGroups: ["policy"]
apiGroups: ["storage.k8s.io"]
```








### Example yaml to create a Clusterole using apiGroups
```
apiVersion: rbac.authorization.k8s.io/v1beta1
kind: ClusterRole
metadata:
  name: demo-app-clusterrole
  labels:
    app: demo-app
rules:
  - apiGroups:
      - ""
    resources:
      - namespaces
      - rolebinding
    verbs:
      - list
      - get
```

