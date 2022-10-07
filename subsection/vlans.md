# VLANs

### Description

A virtual LAN (VLAN) is a logical overlay network that groups together a subset of devices that share a physical LAN, isolating the traffic for each group. A LAN is a group of computers or other devices in the same place -- e.g., the same building or campus -- that share the same physical network.

VLANs operate at Layer 3

[Source](https://www.techtarget.com/searchnetworking/definition/virtual-LAN)

### Create VLANs&#x20;

```
Switch(config)# vlan {number}
Switch(config-vlan)# name {name}
```

### Set Access and Trunk Ports

For this to work you must select an interface using&#x20;

```
Switch(config)# interface range FastEthernet 0/{port}
```

For an individual port type&#x20;

```
Switch(config-if)# switchport 'access or trunk' vlan {port}
```

Configure interfaces in "ranges"

```
Switch(config)# interface range FastEthernet 0/{start port}-{stop port}
```

### Assigning VLAN IP

```
Router(config)# interface vlan <vlan-id>
Router(config-if)# ip address <ip-address> <subnet>
```

### VLAN State

This will make sure the vlan is in the up state. For the love of all make sure that you do this to vlan 1!

```
Router(config)#interface vlan {vlan-id}
Router(config-if)#no shutdown
```

