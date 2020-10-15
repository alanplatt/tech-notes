---
title: "Bash script tips"
date: 2020-06-05T17:32:46+01:00
draft: true
toc: false
images:
tags:
  - bash
  - scripting 
---


## Set these options for more robust scripts and easier debugging

```bash
set -euo pipefail
```
* `e` to exit on error
* `u` exit for unbound variables
* `o pipefail` prevents hidden errors when using pipes


## Identify your script filename

* `${0##*/}` - built in and my preferred method
* `basename "$0"` - classic
