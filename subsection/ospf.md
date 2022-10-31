---
description: Open Shortest Path First
---

# OSPF

### Base Setup

```
enable
config t
interface GigabitEthernet 0/0
no shutdown
ip address {ip_address} {subnet}
exit
router ospf 1
network {network_address} {wildcard} area {area_#}
```

Example

```
enable
config t
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.1 255.255.255.248
exit
router ospf 1
network 10.8.1.0 0.0.0.7 area 0
```

### Add Authentication&#x20;

#### md5

```
enable 
config t 
interface {interface} {interface #} 
ip ospf message-digest-key {instance #} md5 {password}
ip ospf authentication message-digest
```

Example

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```

#### SHA

```
enable
config t
key chain {key_name}
key {#}
cryptographic-algorithm {algorithm}
key-string {password}
exit
interface {interface} {interface_#}
ip ospf authentication key-chain {key_name}
```

Example

```
enable
config t
key chain R2
key 1
cryptographic-algorithm hmac-sha-512
key-string testing
exit
interface GigabitEthernet 0/1
ip ospf authentication key-chain R2
```
