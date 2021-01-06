---
title: "Infoblox - useful stuff"
date: 2020-10-21T17:36:39+01:00
draft: false
toc: false
images:
tags:
  - infoblox
  - api
  - dns
  - dhcp
  - curl
---






#### Get API Schema - versions supported etc
```
curl -k -u curlapi:Eyft6Sp74vUfyUDUDRq3mVm9 -H 'content-type: application/json' -X GET "https://54.73.145.228/wapi/v2.7/?_schema&_return_as_object=1"
```


#### Create a zone or subzone with curl
```
curl -k -u curlapi:Eyft6Sp74vUfyUDUDRq3mVm9 -H 'content-type: application/json' -X POST "https://54.73.145.228/wapi/v2.7/zone_auth?_return_fields%2B=fqdn&_return_as_object=1" -d '{"fqdn": "info.com"}'
```