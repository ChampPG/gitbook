# Lab 6.0: Server Core & Remote Administrator Tools

### Summary

### Steps

1. Configure the networking
   * `vCenter` - make lan
   * `Vmware` - VMNet 5 for 10.0.5.X network
2. Configure systems using `sconfig`
3. Install Remote Server Administration Tools on AD
4. Add Core Server to All Servers
5. `Add Roles and Features` to the Core Server and select `File Server Resource Manager`
6. On Core Server run `netsh advfirewall firewall set rule group="Remote File Server Resource Manager Management" new enable=yes`
7. Under `File and Storage Services` select `Shares`
8. Create `New Share...`
9. click this through menu and select and Core Server
10. if needed change the `Share` tab to have the group you want to see it

### Commands

* `sconfig` - On the Core Server this lets you configure the system
* `netsh` - stands for network shell
  * `netsh advfirewall firewall set rule group="Remote File Server Resource Manager Management" new enable=yes` - This allows AD File Resource Manager through the firewall

### Resources

[How to map a drive](https://activedirectorypro.com/map-network-drives-with-group-policy/)
