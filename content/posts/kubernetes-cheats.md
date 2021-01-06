---
title: "Kubernetes Cheats"
date: 2020-11-06T14:59:29Z
draft: false
toc: false
images:
tags:
  - kubernetes
  - cheats
  - hacks
  - quickref
---

```
# Print the namespace and name of each pod in Running state
kubectl get pods --all-namespaces -o jsonpath="{range .items[?(@.status.phase == 'Running')]}{.metadata.namespace}{' '}{.metadata.name}{'\n'}{end}"
```

