# Lab 2.1: Subnet Design

### Summary

In this lab we setup a Packet Tracer file with the network shown below in the [Subnet Table](lab-2.1-subnet-design.md#subnet-table). During this lab we learned how to setup access and trunk ports from the CLI as well how to configure multiple ports at once. this lab also gave insight into how intervlan communication works at a Multilayer Switch.

#### Subnet Table <a href="#subnet-table" id="subnet-table"></a>

| VLAN | VLAN\_NAME  | Hosts Needed | Network    | Netmask | Router Address |
| ---- | ----------- | ------------ | ---------- | ------- | -------------- |
| 200  | StuWireless | 900          | 10.8.0.0   | /22     | 10.8.0.1       |
| 210  | FSWireless  | 650          | 10.8.4.0   | /22     | 10.8.4.1       |
| 110  | Student     | 450          | 10.8.8.0   | /23     | 10.8.8.1       |
| 1    | Management  | 250          | 10.8.10.0  | /24     | 10.8.10.1      |
| 100  | FacStaff    | 200          | 10.8.11.0  | /24     | 10.8.11.1      |
| 130  | StuLab1     | 35           | 10.8.12.0  | /26     | 10.8.12.1      |
| 140  | StuLab2     | 35           | 10.8.12.64 | /26     | 10.8.12.65     |

### Commands to navigate different modes on a Cisco Switch/Router (enable, config t...) and how you know what mode you are in

* If terminal reads `Router>` type `enable` to enter `Router#`
  * Under `Router>` you're allowed to do `ping, show, enable, etc...`
* If terminal reads `Router#` type `config` to enter `Router(config)#`
  * Under `Router#` you're allowed to do `all User EXEC Commands, debug commands, reload, configure(config), etc...`
* If terminal reads `Router(config)#` view the Official Guide because config branches into 3 different sections.
  * Under `Router(config)#` you're allowed to do `hostname, enable secret, ip route, interface (ethernet, serial, bri, etc...), router (rip, ospf, igrp, etc...), line (vty, console, etc...)`
* [Official Cisco Guide](https://www.cisco.com/E-Learning/bulk/public/tac/cim/cib/using\_cisco\_ios\_software/02\_cisco\_ios\_hierarchy.htm) (Below is image and table included on the website)

<figure><img src="https://www.cisco.com/E-Learning/bulk/public/tac/cim/cib/using_cisco_ios_software/mod_pix/iostree.gif" alt=""><figcaption><p>Image from Cisco Website</p></figcaption></figure>

| EXEC Mode                  | Description                                                                                        |
| -------------------------- | -------------------------------------------------------------------------------------------------- |
| **Router>**                | - User EXEC mode                                                                                   |
| **Router#**                | - Privileged EXEC mode                                                                             |
| **Router(config)#**        | - Configuration mode (notice the # sign indicates this is accessible only at privileged EXEC mode) |
| **Router(config-if)#**     | - Interface level within configuration mode                                                        |
| **Router(config-router)#** | - Routing engine level within configuration mode                                                   |
| **Router(config-line)#**   | - Line level (vty, tty, async) within configuration mode                                           |

### Commands to create VLANS on switch

* ```
  Switch(config)# vlan 100 
  Switch(config-vlan)# name student
  ```

### Setting access and trunk ports on switch

* For this to work you must select an interface using `Switch(config)# interface range FastEthernet 0/{port}`
* For an individual port type `Switch(config-if)# switchport 'access or trunk' vlan {port}`
* Configure interfaces in "ranges"
  * in 'Config' mode type `Switch(config)# interface range FastEthernet 0/{start port}-{stop port}`

### IP Routing

* To turn on routing on multilayer switch type `Router(config)ip routing`
* To enter vlan mode `Router(config) interface vlan 100`
* To set the ip address and subnet for vlan 100 `Router(config-if) ip address {ip} {subnet}`

### Side Notes

* side note you can cut down writing if it's within the ball park. The two below do the same thing.
  * `Switch(config)# interface range FastEthernet 0/{start port}-{stop port}`
  * `Switch(config)# inter rang FastEthernet 0/{start port}-{stop port}`
