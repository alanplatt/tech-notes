---
title: "lxc - quick usage"
date: 2020-05-12T15:45:34+01:00
draft: false
toc: false
images:
tags:
  - lxc
---
### Install lxc
```
apt-get update
apt-get install lxc
```


### Set up host device bridging
Example config
```
cat >> /etc/netplan/01-netcfg.yaml << EOF

network:
  version: 2
  renderer: networkd
  ethernets:
    enp2s0:
      dhcp4: yes
      nameservers:
          addresses: [209.244.0.3, 1.1.1.1]
    enp3s0:
      dhcp4: no
      addresses: [192.168.0.111/24]
      nameservers:
          addresses: [209.244.0.3, 1.1.1.1]
    enp5s4:
      dhcp4: no
  bridges:
      br0:
          dhcp4: no
          addresses:
          - 192.168.53.53/24
          gateway4: 192.168.0.111
          nameservers:
              addresses:
              - 192.168.0.111
          interfaces:
          - enp5s4
EOF

reboot
```

### Create example server 1
```
lxc launch ubuntu:18.04 example1
lxc config device add example1 eth0 nic nictype=bridged parent=br0 name=eth0
lxc config set example1 boot.autostart true
lxc config set example1 boot.autostart.priority 5
lxc config set example1 boot.autostart.delay 1

lxc exec example1 /bin/bash # Edit your config
# Example netplan 
cat >> /etc/netplan/50-cloud-init.yaml << EOF
network:
    version: 2
    ethernets:
        eth0:
            dhcp4: no
            addresses: [192.168.0.51/24, 192.168.0.52/24, 192.168.0.53/24] 
            nameservers:
                addresses: [209.244.0.3, 1.1.1.1]
EOF

netplan apply --debug
```

### Create example server 2
```
lxc launch ubuntu:18:04 example2
lxc config device add example2 eth0 nic nictype=bridged parent=br0 name=eth0
lxc config set example2 boot.autostart true
lxc config set example2 boot.autostart.priority 8
lxc config set example2 boot.autostart.delay 1
```


### Allow docker containers in lxc container
```lxc config set example security.nesting true```