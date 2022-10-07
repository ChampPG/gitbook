# Assignment 2.0: DHCP is Down!

OH NO your DHCP server has been stolen now setup DHCP on windows Core

### Steps

1. Add Remote Server Management for DHCP on the AD server
2. Add Core server DHCP server features
3. Add Core as a DHCP server
   * use wizard to configure Core via AD
4. On Core `netsh dhcp add securitygroups`
5. Now `powershell` then `Restart_Service dhcpserver`

### Links

https://www.c-sharpcorner.com/article/dhcp-role-on-windows-2019-core/
