# Lab 6-1 NAT Configuration - Static NAT

### Summary

Configuring of static NAT to be able to connect the network on the left to the server on the right.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Network Layout</p></figcaption></figure>

### Router 1 (R1):

```
enable
configure terminal
hostname R1
interface fastethernet 0/0
ip address 10.0.0.1 255.0.0.0
no shutdown
exit
interface serial 0/0/0
ip address 20.0.0.2 255.0.0.0
no shutdown
exit
```

### Router 2 (R2):

```
enable
configure terminal
hostname R0
interface fastethernet 0/0
ip address 30.0.0.1 255.0.0.0
no shutdown
exit
interface serial 0/0/0
ip address 20.0.0.1 255.0.0.0
clock rate 64000
bandwidth 64
no shutdown
exit
```

### Configure Routing:

Router 1:

```
R1(config)#ip route 30.0.0.0 255.0.0.0 20.0.0.1
```

Router 0

```
R0(config)#ip route 50.0.0.0 255.0.0.0 20.0.0.2
```

### Configure Static NAT on Router 1

#### Define "Inside" and "Outside" on your NAT interfaces:

in R1(config)$

```
interface fastEthernet 0/0
ip nat inside
exit
interface serial 0/0/0
ip nat outside
exit
```

#### Create The Static Rule

```
R1(config)#ip nat inside source static 10.0.0.2 50.0.0.1
```
