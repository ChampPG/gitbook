# Lab 6-3 NAT LAB 3- Champlain Example Lab

### Summary

In this lab, we setup the Champlain and CNCS labs as an example for implementing NAT.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Network Layout</p></figcaption></figure>

### Goals:

1. Configure IP addressing/gateways on all PC's and Servers using the IP Subnet Table provided
2. Configure PAT on **CC Border Router** so that Foster and Skiff PC's can ping the BT server.**(45 POINTS)**
   * Remember: Foster and Skiff are using private IP addresses (192.168....) - so they can use a shared public IP to access Internet services (such as the Burlington Telecom Server)
   * Must demonstrate that NAT is working by showing ip nat translation table.  You will need to ping the server from CC pc's to generate entries in the table
   * Hint: access lists can have more than one network in them - just enter a "access-list 1 permit..." line for each network that is allowed (Skiff and Foster)
   * Remember: make sure to use an IP from the Champlain Public Network as the PAT pool address
3. Configure Static NAT on Border Router so that BT Server can access the Ireland Pub Web Server(**15 POINTS)**
   * You want Internet users to be able to access your internal Public web server - but it is using a private address
   * Pub Web Server is assigned a 192.168.7.0/24 address - but needs to be reached on a 219.93.144.0 address by BT server

### Steps:&#x20;

Give all machines ip address and default gateways

#### Burlington:&#x20;

```
ip route 0.0.0.0 0.0.0.0 219.93.144.1
```

#### CC:&#x20;

```
ip route 0.0.0.0 0.0.0.0 219.93.144.2
```

#### CCore Switch:

```
interface vlan 1 
no shutdown
```

#### CC: Define Inside and Outside&#x20;

```
interface fastEthernet 0/0 
ip nat inside 
exit 
interface fastEthernet 0/1 
ip nat outside 
exit
```

#### Burlington: Define Inside and Outside&#x20;

```
interface fastEthernet 0/1 
ip nat inside 
exit 
interface fastEthernet 0/0 i
p nat outside 
exit
```

#### Burlington Static: To point the web server to 219.93.144.22&#x20;

```
ip nat inside source static 153.104.18.2 219.93.144.22
```

#### CC Create Pool:&#x20;

```
ip nat pool test 219.93.144.21 219.93.144.21 netmask 255.0.0.0
```

#### CC Access list to only allow skiff and foster use the public IP:&#x20;

```
access-list 1 permit 192.168.1.0 0.0.0.255 
access-list 1 permit 192.168.3.0 0.0.0.255
```

#### CC Access List:&#x20;

```
ip nat inside source list 1 pool test overload
```

#### CC Static: To point the Ireland web server to 219.93.144.23&#x20;

```
ip nat inside source static 192.168.7.2 219.93.144.23
```

#### Tips and tricks:&#x20;

`Router>show access-lists` - This will show all avaible acess lists \
`Router(config)#no access-list {access-list-num}` - This will delete the access list `Router#show ip nat statistics` - This will show active nat stats
