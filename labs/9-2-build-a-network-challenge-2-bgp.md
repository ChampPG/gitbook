# Lab 9-2: Build a Network Challenge 2 - BGP

### Summary

During this lab we took the frame work from the last lab and built out BGP from BTV-Router to Vermont-ISP then to Pacific-ISP.

### Subnet Tables

#### Subnet Table Routers

| Name                | Network Address | Subnet          | Gateway     |
| ------------------- | --------------- | --------------- | ----------- |
| Vermont to BTV      | 192.168.2.0     | 255.255.255.252 | 192.168.2.1 |
| Vermont to Pacific  | 192.168.1.0     | 255.255.255.252 | 192.168.1.1 |
| Pacific to Partner  | 192.168.3.0     | 255.255.255.252 | 192.168.3.1 |
| Pacific to Customer | 192.168.4.0     | 255.255.255.252 | 192.168.4.1 |

#### Subnet Table Burlington <a href="#subnet-table" id="subnet-table"></a>

| Name         | Network Address | Subnet          | Gateway     |
| ------------ | --------------- | --------------- | ----------- |
| BTV to MTL   | 172.16.0.0      | 255.255.255.252 | 172.16.0.1  |
| BTV Core     | 172.16.10.0     | 255.255.255.0   | 172.16.10.1 |
| BTV Users    | 172.16.5.0      | 255.255.255.0   | 172.16.5.1  |
| BTV Data Ctr | 172.16.6.0      | 255.255.255.0   | 172.16..1   |
| MTL          | 172.16.20.0     | 255.255.255.0   | 172.16.20.1 |

**Subnet Table Customer**

| Name      | Network Address | Subnet         | Gateway      |
| --------- | --------------- | -------------- | ------------ |
| ​Customer | 10.200.24.0     | 255.255.255.0​ | ​10.200.24.1 |

#### Subnet Table Partner

| Name    | Network Address | Subnet        | Gateway   |
| ------- | --------------- | ------------- | --------- |
| Partner | 10.15.6.0       | 255.255.255.0 | 10.15.6.1 |

<figure><img src="../.gitbook/assets/image (1) (4).png" alt=""><figcaption><p>Network Photo</p></figcaption></figure>

### Steps:

#### Vermont-ISP

```
enable
config t
hostname vermont-router
interface FastEthernet 0/0
ip address 192.168.1.1 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 192.168.2.1 255.255.255.252
no shutdown
router bgp 1010
neighbor 192.168.2.2 remote-as 3033
neighbor 192.168.1.2 remote-as 2054
network 192.168.1.0 mask 255.255.255.252
```

#### BTV-Router

```
enable
config t
hostname btv-router
interface FastEthernet 0/1
ip address 192.168.2.2 255.255.255.252
no shutdown
interface FastEthernet 0/0
ip address 172.16.10.1 255.255.255.0
no shutdown
interface Serial 0/1/0
ip address 172.16.0.1 255.255.255.252
no shutdown
router ospf 1
default-information originate
network 172.16.10.0 0.0.0.255 area 0
network 172.16.0.0 0.0.0.3 area 0
ip route 0.0.0.0 0.0.0.0 192.168.2.1
router bgp 3033
neighbor 192.168.2.1 remote-as 1010
redistribute ospf 1
network 192.168.2.0 mask 255.255.255.252
```

#### BTV-Multilayer-Switch

```
enable
config t
hostname btv-multiplayer-switch
vlan 5
name users
vlan 6
name DC
ip routing
interface vlan 1
no shutdown
interface vlan 5
no shutdown
ip address 172.16.5.1 255.255.255.0
interface vlan 6
no shutdown
ip address 172.16.6.1 255.255.255.0
interface vlan 10
no shutdown
ip address 172.16.10.2 255.255.255.0
interface range FastEthernet 0/2
switchport access vlan 5
interface range FastEthernet 0/6
switchport access vlan 6
interface range FastEthernet 0/1
switchport access vlan 10
router ospf 1
network 172.16.5.0 0.0.0.255 area 0
network 172.16.6.0 0.0.0.255 area 0
network 172.16.10.0 0.0.0.255 area 0
```

#### MTL-Router

```
enable
config t
hostname mtl-router
interface FastEthernet 0/0
ip address 172.16.20.1 255.255.255.0
no shutdown
exit
interface Serial 0/1/0
ip address 172.16.0.2 255.255.255.252
no shutdown
exit
router ospf 1
network 172.16.20.0 0.0.0.255 area 0
network 172.16.0.0 0.0.0.3 area 0
```

#### Pacific-ISP

```
enable
config t
hostname pacific-router
interface FastEthernet 0/0
ip address 192.168.1.2 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 192.168.3.1 255.255.255.252
no shutdown
interface Serial 0/1/0
ip address 192.168.4.1 255.255.255.252
no shutdown
router bgp 2054
neighbor 192.168.1.1 remote-as 1010
neighbor 192.168.3.2 remote-as 34908
neighbor 192.168.4.2 remote-as 5132
network 192.168.3.0 mask 255.255.255.252
network 192.168.4.0 mask 255.255.255.252
```

#### Customer-Router

```
enable
config t
hostname customer-router
interface FastEthernet 0/0
ip address 10.200.24.1 255.255.255.0
no shutdown
interface Serial 0/1/0
ip address 192.168.4.2 255.255.255.252
no shutdown
router bgp 5132
neighbor 192.168.4.1 remote-as 2054
network 10.200.24.0 mask 255.255.255.0
```

#### Partner-Router

```
enable
config t
hostname partner-router
interface FastEthernet 0/0
ip address 192.168.3.2 255.255.255.252
no shutdown
interface FastEthernet 0/1
ip address 10.15.6.1 255.255.255.0
no shutdown
router bgp 34908
neighbor 192.168.3.1 remote-as 2054
network 10.15.6.0 mask 255.255.255.0
```

### Notes:

#### BGP:

Remember to advertise the internal network...

#### Tips:

```
show ip bgp summary
```
