---
description: 'Week 2: 9/5/22'
---

# Week 2: Subnetting, VLANS, & Cisco Commands

### Subnetting

* Allow very common subnets: **/24** (256 IP’s, 254 Usable), **/23** (512 IP’s, 510 Usable), **/22** (1024 IP’s, 1022 Usable), **/30** (4 IP’s, 2 Usable), **/29** (8 IP’s, 6 Usable)
* Organizations are “assigned” a network address to use on the internet
  * 216.93.144.0/20
    * All champlain IPs start with the same 20 bits
    * Last 12 bits are used for host ID
    * 2^12 IPs can be used
      * All zeros and all 1’s in the host ID can’t be used
* But a /20 network cna support 4094 hosts - do we want them all on the same network?
  * Lots of broadcast packets congest the network
  * Machines are slowed by trying to process them
  * Anyone can contact anyone else on the network!
* Our network ID can’t change but what if we took some host ID bits to create a subnet ID
  * These bits are then ”added” to the network ID
  * For example if we used 4 bits for the subnet ID
* Wireless networks are normally larger networks because most devices are looking for information outside the network. Larger network means less communication inside the network.
* Smaller networks are found in places where devices communicate within the network. For example a data center. (Network to Network firewall rules instead of Host to Host rules)
* Always start with the largest subnet first: Larger subnet boundaries are always valid for smallers ones, but smaller boundaries are not always valid for larger ones
* All 0’s in the **Host ID** refers to the Network itself - cannot be assigned to a host
* All 1’s in the **Host ID** is the broadcast -cannot be assigned to a host
* So if we have n bits in our Host ID, we can assign 2^2 -2 IP addresses\


### VLANS

* Multilayer switching
* A virtual LAN is a group of devices on one or more physical LANs that are configured to communicate as if they were on the same LAN.
* VLANs define broadcast domains in a Layer 2 network
* Need a router to pass packets between 2 different VLANs
* **Access Ports:** Can only be assigned to/carry traffic from a single VLAN
  * Used to connect end device to a switch
* **Trunk Ports:** Carry traffic from multiple VLANs - used to connect switches
  * Will “tag” packets with the proper VLAN ID\


### CISCO IOS Config File

* **Startup-config:** This is the last version that was saved. If the router/switch was restarted, this is the config that would load
* **Running-config:** Whats running in memory. It has all of the config changes made at the command line since it was last saved.&#x20;
* **User EXEC Mode:** Basic monitoring and status commands
  * Prompt it: router>
  * Type enable to get to Privileged
* **Privileged EXEC Mode:** Administrative access
  * Prompt: router#
  * Type config to get to the config mode
* **Config EXEC MODE:** config mode
  * Prompt: router(config)#
* The question mark ?:
  * Just hit enter and it will show everything you can do
* Tab works in IOS
