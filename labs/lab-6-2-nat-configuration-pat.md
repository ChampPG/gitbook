# Lab 6-2 NAT Configuration - PAT

### Summary



### Commands

#### Router 2: Base Setup

```
enable
configure terminal
hostname Router2
interface fastethernet 0/0
ip address 20.0.0.1 255.0.0.0
no shutdown
exit
interface serial 0/0/0
ip address 30.0.0.2 255.0.0.0
no shutdown
exit
```

#### Router 1: Base Setup

```
enable
configure terminal
hostname Router1
interface fastethernet 0/0
ip address 192.168.0.1 255.255.255.0
no shutdown
exit
interface serial 0/0/0
ip address 30.0.0.1 255.0.0.0
clock rate 64000
bandwidth 64
no shutdown
exit
```

#### Router 2: Routing

```
ip route 192.168.0.0 255.255.255.0 30.0.0.1
```

#### Router 1: Routing

```
ip route 0.0.0.0 0.0.0.0 30.0.0.2
```

#### Router 1: Define Inside and Outside

```
interface fastEthernet 0/0
ip nat inside
exit
interface serial 0/0/0
ip nat outside
exit
```

#### Create Pools:

```
ip nat pool test 30.0.0.120 30.0.0.120 netmask 255.0.0.0
```

#### Create Access-list: Defines which internal IP's can use the Public Pool

```
access-list 1 permit 192.168.0.0 0.0.0.255
```

#### Assign Pool and Access Rule:

```
ip nat inside source list 1 pool test overload
```

#### Show NAT translations

```
show ip nat translations
```
