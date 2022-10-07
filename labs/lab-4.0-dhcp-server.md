# Lab 4.0: DHCP Server

### Summary

The main objective was to create a DHCP server in our CentOS machines. This went relatively straightforward. The only problem I had was I got really confused with the max-lease-time and default-lease-time documentation because I forgot about the man command and I had to look through the online documentation.

### Steps

1. The first item related to DHCP is the `option domain-name example.com`. DHCP needs the domain name so it's easier for the DHCP server to know and allocate to different machines on the network.
2. The second item is how DHCP uses 2 ports because this is to prevent another protocol to clog the port as well so the flow of DHCP is smooth.
3. The third item is lease times and max lease times. a lease time is needed so a computer that is disconnected from the network doesn't just take up an IP for the rest of the time. the default lease time is just the time the computer can go with the original ping to the system and the max lease time is how long an active computer cna go before being kicked off.

### Commands

#### CentOS

1. `yum` = yum is the default package manager for CentOS
   * `sudo yum install dhcp` = this was to install the DHCP server we needed for the lab
2. `sudo -i` = puts the current user into superuser as well this command needs the current users password
3. `vi` = vim text editor
   * to write in vim press `i`
   * to quit vim hit `esc` then typ `:wq` to write and quit
   * `vi /etc/dhcp/dhcpd.conf` = goes to dhcpd.conf file using vim

```
# DHCP Server Configuration file.
#     see /usr/share/doc/dhcp* /dhcpd.conf.example
#     see dhcpd.conf(5) man page
#
subnet 10.0.5.0 netmask 255.255.255.0 {
    option routers 10.0.5.2;
    option subnet-mask 255.255.255.0;
    option domain-name "example.com";
    option domain-name-servers 10.0.5.5;
    range 10.0.5.100 10.0.5.150;
```

1. `systemctl` = sytem control program
   * `systemctl start dhcpd` = will start the process dhcpd
   * `systemctl status dhcpd` = will show the status of dhcpd
   * `systemctl enable dhcpd` = will make dhcpd start at boot
2. `firewall-cmd --list-all` = shows all the firewall options
   * `firewall-cmd --add-service=dhcp --permanent` = will make a permanent change so dhcp is allowed through the firewall
   * `firewall-cmd --reload` = will refresh the firewall
3. `sudo cat /var/log/messages | grep wks01-paul` = will show the dhcpd logs of connections for wks01-paul

#### Windows

1. `ssh` = by using ssh "hostname" in the POWERSHELL, not PowerShell ISE!! you can ssh into a client
2. `ipconfig` = shows basic network adapters and their properties
   * `ipconfig /all` = shows all network adapters and their properties
   * `ipconfig /release` = will release current dhcp
   * `ipconfig /renew` = new renew dhcp
