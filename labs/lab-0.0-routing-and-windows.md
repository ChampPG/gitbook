# Lab 0.0: Routing and Windows

### Summary



### Machine Setup

* fw01-paul 10.0.5.2 (Static)
* wks01-paul 10.0.5.100 (Static) Gate = 10.0.5.2 DNS = 10.0.5.5
* ad01-paul 10.0.5.5 (Static) Gate = 10.0.5.2 DNS = 10.0.5.5
* mgmt01-paul 10.0.5.10 (Static) Gate = 10.0.5.2 DNS = 10.0.5.5

### Steps

1. Add LAN Adapter to fw01
2. Had to cable all the VM's
3. Configure fw01-paul
4. Configure wk01-paul
   * Finish web config fw01-paul
     * Make sure to uncheck block RFC1918 Private Network
5. Configure ad01-paul
   * Use `sconfig` to get to configuration menu
   * Type `powershell`
     * Type `Install-WindowsFeature AD-Domain-Services -IncludeManagementTools` to install AD
     * Type `Install-ADDSForest -DomainName paul.local` to great the forest for paul.local
6. Join wk01-paul to domain
7. Configure mgmt01-paul
   * Add Roles and Features under `Remote Server Administrations Tools` then `Role Administration Tools` check `DNS Server Tools`, `DHCP Server Tools`, `File Services Tools`, `AD DS and AD LDS Tools`
8. Now add ad01-paul to `All Server list` (DONT FORGET THIS STEP)
9. Create user and user-adm (Add to domain admins)
10. Create Reverse Look Up Zone and add points for computers

### Terms

1. Domain Controllers - This is a server that controllers the data for the domain. I want to know more about the extent which these can be used.
2. Server Core - Windows Server operating system. I want to know more about why it's just a cmd window and how I can better understand why way around it.
3. RFC1918 - This blocks pings from private networks. I want to know more about why we need to not check this and how it has effected our way of networking.

### Notes

1. Get PTR Records in powershell `Get-DnsServerResourceRecord -ComputerName [DNS-Server] -ZoneName [Reverse IP].in-addr.arpa -RRType Ptr`
