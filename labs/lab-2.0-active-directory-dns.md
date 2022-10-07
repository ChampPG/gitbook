# Lab 2.0: Active Directory DNS

### Summary

During this lab, we learned about Active Directory and more about DNS. We set up a Microsoft 2019 server and configured it. The main problem I ran into was my firewall name isn't fw01 and it's fwo1 so when I was trying to follow the documentation I had a very hard time. This was an easy fix and everything else was pretty straight foward.

### Steps

1. I had to test to make sure my Firewall and Workstation were working
2. Changed the server to have the correct adapter settings
3. Setup server wizard and gave it a password
4. Setup network
   * IP Address: 10.0.5.5
   * Netmask: 255.255.255.0
   * Gateway 10.0.5.2 (Make sure fw01 is running).
   * DNS 10.0.5.2
5. Changed timezone and computers name
   * double-checked system is working
6. Set up the roles and features wizard
   * selected to add Active Directory Domain Services
7. Promotion
   * Add a new forest (paul.local)
   * made a DSRM password
8. Then add a new A host for the firewall and it's IP of 10.0.5.2

* Make a New Zone for 10.0.5...
* Add new users for adm and base user for the paul.local

1. Change the DNS of the wks01 to the DNS of 10.0.5.5 or the ad01
2. Join wks01 to the domain
   * change the computer name and select domain to equal paul

### Commands Used

* `whoami` A command to see who you are logged in as.
* `ping` A command used to say hey to other networks and machines.
* `nslookup` A command to query the DNS for a domain name and IP address.
* `hostname` A command to see the name of a system.
