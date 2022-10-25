# Lab 8-1B OSPF PT Activity

### Summary

To configure OSPF for a small enterprise with 4 routers.

### **Subnet Table**

| Network Name                | Network Address | Subnet Mask     | Default Gateway | Router acting as Gateway |
| --------------------------- | --------------- | --------------- | --------------- | ------------------------ |
| Border-to-Data Center       | 10.8.1.0        | 255.255.255.248 | 10.8.1.1        | Border                   |
| East-Router2 to Data Center | 10.8.1.20       | 255.255.255.252 | 10.8.1.21       | East-Router              |
| DataCenter-to WestRouter4   | 10.8.1.32       | 255.255.255.252 | 10.8.1.33       | Data Center-Router       |
| East                        | 10.8.20.0       | 255.255.255.0   | 10.8.20.1       | East-Router              |
| West                        | 10.8.40.0       | 255.255.255.0   | 10.8.40.1       | West-Router              |

\


<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p><strong>Network Layout</strong></p></figcaption></figure>

### Border Router: Network 1

```
enable
config t
hostname Paul-Border-Router1
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.1 255.255.255.248
exit
router ospf 1
network 10.8.1.0 0.0.0.7 area 0
```

### East Router: Network 2

```
enable
config t
hostname Paul-East-Router2
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.21 255.255.255.252
exit
interface GigabitEthernet 0/1
no shutdown
ip address 10.8.20.1 255.255.255.0
router ospf 1
network 10.8.1.20 0.0.0.3 area 0
network 10.8.20.0 0.0.0.255 area 0
```

### Data Center: Network 3

```
enable
config t
hostname Paul-DataCenter-Router3
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.22 255.255.255.252
exit
interface GigabitEthernet 0/1
no shutdown
ip address 10.8.1.33 255.255.255.252
exit
interface GigabitEthernet 0/2
no shutdown
ip address 10.8.1.2 255.255.255.248
exit
router ospf 1
network 10.8.1.0 0.0.0.7 area 0
network 10.8.1.32 0.0.0.3 area 0
network 10.8.1.20 0.0.0.3 area 0
```

### West Router: Network 4

```
enable
config t
hostname Paul-West-Router4
interface GigabitEthernet 0/0
no shutdown
ip address 10.8.1.34 255.255.255.252
exit
interface GigabitEthernet 0/1
no shutdown
ip address 10.8.40.1 255.255.255.0
exit
router ospf 1
network 10.8.1.32 0.0.0.3 area 0
network 10.8.40.0 0.0.0.255 area 0
```
