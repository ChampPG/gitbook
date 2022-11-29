# Access-Lists

{% embed url="https://www.cisco.com/c/en/us/support/docs/security/ios-firewall/23602-confaccesslists.html" %}
Documentation
{% endembed %}

### Base Setup:

#### Standard

```
enable
config t
ip access-list standard {list name}
! To deny network and allow everything else
deny {network address} {wildcard subnet}
permit any
! To permit network and deny everything else
permit {network address} {wildcard subnet}
! This works becuase of the hidden deny any any
exit
! Below is to apply list to interface
interface {interface} {interface #}
ip access-group {list name} {in or out}
```

#### Extended

```
enable
config t
ip access-list extended {list name}
! To deny ip from the network to specified host and allow ip for everything else
deny ip {network address} {wildcard subnet} host {host ip}
permit ip any any
! To permit only www (website) traffic to specifed machine and deny everything else
permit tcp any host {host ip} eq www
! This works becuase of the hidden deny any any
exit
! Below is to apply list to interface
interface {interface} {interface #}
ip access-group {list name} {in or out}
```

### Example:&#x20;

#### Standard

```
enable
config t
ip access-list standard STND-1
! To deny network and allow everything else
deny 192.168.10.0 0.0.255.255
permit any
! To permit network and deny everything else
permit 192.168.1.0 0.0.255.255
! This works becuase of the hidden deny any any
exit
! Below is to apply list to interface
interface serial 0/0/0
ip access-group STND-1 in
```

#### Extended

```
enable
config t
ip access-list extended EXTEND-1
! To deny ip from the network to specified host and allow ip for everything else
deny ip 200.200.200.0 0.0.0.3 host 192.168.20.210
permit ip any any
! To permit only www (website) traffic to specifed machine and deny everything else
permit tcp any host 192.168.20.201 eq www
! This works becuase of the hidden deny any any
exit
! Below is to apply list to interface
interface FastEthernet 0/0
ip access-group EXTEND-1 out
```
