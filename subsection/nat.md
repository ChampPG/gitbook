---
description: Network Address Translation
---

# NAT

## Types of NAT

### Static

#### Base Setup:

```
enable
conf t
interface {interface} {interface_#}
ip nat inside
exit
interface {interface} {{interface_#}
ip nat outside
exit
ip nat inside source static {source_ip} {static_ip}
```

#### Example:

```
enable
conf t
interface fastEthernet 0/0
ip nat inside
exit
interface serial 0/0/0
ip nat outside
exit
ip nat inside source static 10.0.0.2 50.0.0.1
```

### PAT

#### Base Setup:

```
enable
conf t
interface {interface} {interface_#}
ip nat inside
exit
interface {interface} {{interface_#}
ip nat outside
exit
ip nat pool {pool_name} {start_ip} {stop_ip} netmask {subnet_mask}
access-list 1 permit {internal_network_address} {wildcard_subnet}
ip nat inside source list 1 pool {pool_name} overload
```

#### Example:

```
enable
conf t
interface fastEthernet 0/0
ip nat inside
exit
interface serial 0/0/0
ip nat outside
exit
ip nat pool test 30.0.0.120 30.0.0.120 netmask 255.0.0.0
access-list 1 permit 192.168.0.0 0.0.0.255
ip nat inside source list 1 pool test overload

```

### Notes:

To show active nat stats

```
enable
show ip nat statistics
```
