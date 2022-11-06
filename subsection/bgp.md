---
description: Border Gateway Protocol
---

# BGP

### Base Setup

```
enable
config t
interface {interface} {interface_#}
no shutdown
ip address {ip_address} {subnet_mask}
router bgp {as_#}
neighbor {neighbor_ip} remote-as {neighbor_as}
network {network} mask {subnet_mask}
```

Example

```
enable
config t
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.1 255.255.255.248
router bgp 1010
neighbor 192.168.2.2 remote-as 3033
network 192.168.1.0 mask 255.255.255.252
```

### Notes

For the line only 1 of the routers has to advertise the network. AS WELL INTERNET NETWORKS NEED TO BE ADVERTISED!

```
network 192.168.1.0 mask 255.255.255.252
```
