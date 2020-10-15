---
title: "Kubernetes certmanager - Quick ref"
date: 2020-06-10T12:40:16Z
draft: false
toc: false
images:
tags:
  - kubernetes
  - certmanager
  - letsencrypt

---
### Force cert renewal
```
# renew
kubectl patch certificate example-certificate --type=merge -p '{"spec":{"renewBefore":"2159h00m00s"}}' -n <namespace>

# MAKE SURE YOU REMOVE (or it will get stuck in a renew cycle)
kubectl patch certificate example-certificate --type=json -p='[{"op": "remove", "path": "/spec/renewBefore"}]' -n <namespace>
```


### Is your install correct?
1. Ensure you have all the CRDS
```
▶ kubectl get crd | grep cert-manager

certificaterequests.cert-manager.io            2020-06-16T11:42:24Z
certificates.cert-manager.io                   2020-06-16T11:42:24Z
challenges.acme.cert-manager.io                2020-06-16T11:42:25Z
clusterissuers.cert-manager.io                 2020-06-16T11:42:25Z
issuers.cert-manager.io                        2020-06-16T11:42:24Z
orders.acme.cert-manager.io                    2020-06-16T11:42:24Z
```

2. Ensure all the pods are running 
```
▶ kubectl get pods --namespace cert-manager

NAME                                       READY   STATUS    RESTARTS   AGE
cert-manager-68cfd787b6-5984h              1/1     Running   0          2d21h
cert-manager-cainjector-5975fd64c5-6zmd9   1/1     Running   0          2d21h
cert-manager-webhook-5c7f95fd44-9ltf4      1/1     Running   0          2d21h
```

3. Test that we can issue basic cert types
```
cat <<EOF > test-resources.yaml
apiVersion: v1
kind: Namespace
metadata:
  name: cert-manager-test
---
apiVersion: cert-manager.io/v1alpha2
kind: Issuer
metadata:
  name: test-selfsigned
  namespace: cert-manager-test
spec:
  selfSigned: {}
---
apiVersion: cert-manager.io/v1alpha2
kind: Certificate
metadata:
  name: selfsigned-cert
  namespace: cert-manager-test
spec:
  dnsNames:
    - example.com
  secretName: selfsigned-cert-tls
  issuerRef:
    name: test-selfsigned
EOF

kubectl apply -f test-resources.yaml

kubectl describe certificate -n cert-manager-test
```


### Check the expiry of certificates
```
kubectl get orders.acme.cert-manager.io/nginx-tls-144042275-3483654949 -n default -o json | jq -r .status.certificate | base64 -D | openssl x509 -noout -dates
```