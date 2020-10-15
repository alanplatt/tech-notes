---
title: "Openssl Quickref"
date: 2020-06-16T15:10:25+01:00
draft: false
toc: false
images:
tags:
  - openssl
---

### view cert details
* see who has issued the SSL certificate -issuer
* whom the SSL certificate is issued to -subject
* what dates the SSL certificate is valid - dates
```
openssl x509 -noout -issuer -subject -dates
```

#### -text gives you all the details
```
openssl x509 -noout -text
```