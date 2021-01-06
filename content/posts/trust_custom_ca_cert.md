---
title: "How to trust a custom CA cert"
date: 2020-12-16T16:03:20Z
draft: false
toc: false
images:
tags:
  - ssl
  - root_cert
  - CA
  - trust
  - debian
  - ubuntu
  - tls
---

Annoyingly this is a different process per distribution. Here is what worked for me.  To test curl a url with a cert signed by the CA you're trying to add.


### RHEL 7.8
Accepts a cert in PEM format (the format that has ----BEGIN CERTIFICATE---- in it)
```
cp trustchain.pem /etc/pki/ca-trust/source/anchors/trustchain.pem
update-ca-trust extract
```

### Ubuntu 20.04
Accepts a cert in PEM format (the format that has ----BEGIN CERTIFICATE---- in it) but with crt file extension. PEM file can contain one or more certs like a true PEM file. You should add the whole chain here.
```
cp mycert.pem /usr/local/share/ca-certificates/mycert.crt
update-ca-certificates --verbose --fresh
```

### Debian 10
Same as Ubuntu but only accepts one cert in the Pem file.
```
cp mycert.pem /usr/local/share/ca-certificates/mycert.crt
update-ca-certificates --verbose --fresh
```
