+++
date = '2024-12-23T12:57:27Z'
draft = false
tags = ['proxmox', 'firewall']
title = 'Setting up a firewall with Proxmox VE'
+++

## The issue

When enabling the firewall at the data center level, access to the WebGUI (port 8006) and SSH (port 22) was blocked from my local network, even though the [documentation](https://pve.proxmox.com/pve-docs/pve-admin-guide.html#_enabling_the_firewall) states it shouldn't be. 

## The fix

On a node, configure `/etc/pve/firewall/cluster.fw` like so: 

```toml
[OPTIONS]
enable: 1

[RULES]

IN ACCEPT -p icmp -log nolog
IN ACCEPT -source 192.168.1.0/24 -p tcp -dport 8006 -log nolog
IN SSH(ACCEPT) -source 192.168.1.0/24 -log nolog
```

After writing the changes, the firewall will be enabled and access allowed locally.

### Explanation
This allows for access to SSH and the WebGUI from the local network (my local network is the 192.168.1.0/24 block) and accepts ICMP for using `ping`.

As an alternative you could use `IN ACCEPT -source 192.168.1.0/24 -p icmp -log nolog` to only allow pinging the hosts from the local network.

---

I am new to Proxmox, so if there is a better solution let me know!