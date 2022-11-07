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
```

### PAT

#### Base Setup:

```
```

#### Example:

```
```
