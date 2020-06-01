---
title: "Ssh_keygen"
date: 2020-06-01T16:04:02+01:00
draft: true
toc: false
images:
tags:
  - ssh
  - openssh
  - ssh-keygen
---

# Generating ssh keys (ssh-keygen)
This is a quick to the point doc, for more details try [here](https://www.ssh.com/ssh/keygen/)


### First off, pick your Algorithm 
| Algorithm  | Brief                                      | Should i use?                      |
| ---------- |:------------------------------------------ |:---------------------------------- |
| rsa        | Widely used, still works but aging.        | If you're nostalgic/feeling lazy.  |
| dsa        | Old, dont bother.                          | no.                                |
| ecdsa      | Wide ranging compatabilty, new and secure. | Yes, the best bet at the moment.   |
| ed25519    | Even newer with less compatability.        |  Might be the one for the furture. |

### Create the key...
```
export DATE=$(date '+%Y-%m-%d')
ssh-keygen -t ecdsa \
           -b 521 \
           -C "New key ${DATE}" \
           -f "${HOME}/.ssh/id_ecdsa"
```


### Copy your key to a host
```
ssh-copy-id -i ~/.ssh/id_ecdsa.pub user@host
```