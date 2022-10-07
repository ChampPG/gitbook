# Lab 3.3: DHCP Server in Packet Tracer

### Summary

In this lab we worked on creating a DHCP server that was able to communicated over multiple VLANs and used ip helpers on the core switches. We used the same [Subnet Table](broken-reference) as the previous lab.

### How to create pools

![Pool Creation](https://user-images.githubusercontent.com/71086240/189728852-ddf5f08d-e89e-4e64-8779-9a5b6777d8b8.PNG)

1. First select `Services` tab
2. Then select `DHCP` on the right side
3. Next type in the information you want
4. Finally Saving and Adding a. If new Pool select `Add` b. If editing Pool select `Save`

### Working with serverPool

* `serverPool` is the Default Pool and cannot be removed
* In this lab we used `serverPool` for `VLAN 1 Management`
* In the photo shown above once you edit `serverPool` select `Save` because it's already been made

### Assigning IP helper addresses

1. Enter the `CLI` for a MLS
2. In `(config)` mode type `interface vlan {VLAN-ID}`
3. Then type `ip helper-address {IPaddr-DHCP-Server}`
4. Type `exit`
5. Repeat steps 2 to 4 for the rest of the VLANs

### Any issues you encountered

The only issue I ran into was my ports on the East-Core-Switch were off-set by one
