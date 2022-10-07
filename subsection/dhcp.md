# DHCP

### How to create pools

![Pool Creation](https://user-images.githubusercontent.com/71086240/189728852-ddf5f08d-e89e-4e64-8779-9a5b6777d8b8.PNG)

1. First select `Services` tab
2. Then select `DHCP` on the right side
3. Next type in the information you want
4. Finally Saving and Adding a. If new Pool select `Add` b. If editing Pool select `Save`

### Working with serverPool

The Pool creates the DHCP limitations for specific subnets

* `serverPool` is the Default Pool and cannot be removed
* In this lab we used `serverPool` for `VLAN 1 Management`
* In the photo shown above once you edit `serverPool` select `Save` because it's already been made

### Assigning IP Helper Addresses

IP helpers allow computers on different VLANs to be able to access the DHCP Server

1. Enter the `CLI` for a MLS
2. Enter `config` mode and type&#x20;

```
router(config)# interface vlan {VLAN-ID}
```

&#x20; 3\. Then type&#x20;

```
router(config-if)# ip helper-address {IPaddr-DHCP-Server}
```

&#x20; 4\. Type&#x20;

```
exit
```

&#x20; 5\. Repeat steps 2 to 4 for the rest of the VLANs
