# Lab 1.0: Firewall and Work Station

### Summary

During this [lab](https://docs.google.com/document/d/1-XcJ2gEjgBkTEluPB4NYKCjHchag2m1UZANIAqLSLMU/edit#heading=h.23gysb7e448l) I learned how to set up a pfsense firewall and have a working windows 10 computer connect through it. We started with connecting to the Vsphere client to access our virtual machines from there we set up the networking for the Firewall VM. Then turned to the windows VM and changed the hostname and the IPv4 configuration to use the ip of the firewall as the DNS of the workstation. After that and once the connection was set we pinged the Champlain servers to confirm it was connected.

### Commands Used

1.
   * In PfSense, 1 allows you to reassign the network interfaces.
2.
   * In PfSense, 2 allows you to set the IP interfaces.
3. `whoami`
   * In Windows 10, this command displays who you are logged in as.
4. `hostname`
   * In Windows 10, this command displays the name of the machine.
5. `ping -n 1 champlain.edu`
   * In Windows 10, this command will ping champlain.edu one time.
6. `ipconfig`
   * In Windows 10, this command displays the networking information about the machine.
