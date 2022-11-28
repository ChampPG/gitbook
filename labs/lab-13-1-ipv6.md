# Lab 13-1: IPv6

### Summary



<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Network Diagram</p></figcaption></figure>

### Setup

#### Machines

On Champlain & Middlebury Hosts: `Desktop-IP configuration: Click Auto-Config under IPv6 Configuration`

#### CC-R

```
enable
config t
ipv6 general-prefix champ-pre 2620:E4:C000::/64
interface FastEthernet 0/1
no shutdown
ipv6 address 2620:E4:C000::1/64
ipv6 unicast-routing
interface FastEthernet 0/1
ipv6 rip process1 enable
interface FastEthernet 0/0
ipv6 address autoconfig
no shutdown
ipv6 rip process1 enable
```

#### MC-R

```
enable
config t
ipv6 general-prefix mid-pre 2001:1890:139D::/64
interface FastEthernet 0/1
no shutdown
ipv6 address 2001:1890:139D::1/64
ipv6 unicast-routing
interface FastEthernet 0/1
ipv6 rip process1 enable
interface FastEthernet 0/0
ipv6 address autoconfig
no shutdown
ipv6 rip process1 enable
```

#### VTEL-ISP

```
enable
config t
ipv6 general-prefix vtel-pre 1800:2200:185::/64
interface FastEthernet 0/0
no shutdown
ipv6 address 1800:2200:185::/64 eui-64
ipv6 unicast-routing
interface FastEthernet 0/0
ipv6 rip process1 enable
! Exit config mode and run show ipv6 interface brief
```
