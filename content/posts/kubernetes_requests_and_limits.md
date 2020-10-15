---
title: "Requests & Limits - Quick ref"
date: 2020-05-01T15:05:26+01:00
draft: false
toc: false
images:
tags:
  - kubernetes
  - limits
  - requests
  - cpu
  - memory
---
[Full kubernetes doc](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

### CPU
Limits and requests for CPU resources are measured in cpu units
* 1 CPU is set as 1
* A tenth of a CPU would be 0.1
* A tenth of a CPU can also be 100m which is "one hundred millicpu"

### Memory
Limits and requests for memory are measured in bytes
* 256 Mebibytes of memory would be 256Mi
* 1 Gibibyte or 1Gi would equal 1024Mi

NOTE: A mebibyte is equal to 2^20 or 1,048,576 bytes. A megabyte is equal to 106 1,000,000 bytes


### Example
This ontainer has a request of 0.25 cpu and 64MiB (226 bytes) of memory. It also has a limit of 0.5 cpu and 128MiB of memory.
```
apiVersion: v1
kind: Pod
metadata:
  name: something
spec:
  containers:
  - name: somename
    image: someimage
    resources:
      requests:
        memory: "64Mi"
        cpu: "250m"
      limits:
        memory: "128Mi"
        cpu: "500m"
```
