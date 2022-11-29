# IPv6

### Base Setup:

```
enable
config t
ipv6 general-prefix {prefix name} {prefix}
interface {interface} {interface #}
no shutdown
ipv6 address {ipv6 address}
ipv6 unicast-routing
interface {interface} {interface #}
ipv6 rip process1 enable
interface {interface} {interface #}
ipv6 address autoconfig
no shutdown
ipv6 rip process1 enable
```

### Examples:

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

#### Notes

```
! For eui-64
enable
config t
ipv6 general-prefix {prefix name} {prefix}
interface {interface} {interface #}
no shutdown
ipv6 address {ipv6 address} eui-64
ipv6 unicast-routing
interface {interface} {interface #}
ipv6 rip process1 enable
interface {interface} {interface #}
ipv6 address autoconfig
no shutdown
ipv6 rip process1 enable
```
