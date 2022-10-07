# Assignment 3.0: Securing SSH

### Summary

This assignment went extremely well the only problem I had was a lot of the guides had different ways to restart the sshd service so it was tricky to find which one work.

### Commands

1. `vi /etc/shh/sshd_config`
2. Go to the line that says `#PermitRootLogin yes`
3. Get rid of the `#` and turn `yes` to `no`
   * end result `PermitRootLogin no`
4. Write and Quit
5. `service sshd restart`
6. Now root won't be able to ssh

### Notes

1. Root uid is 0
2. First user uid is 1000
3. uids 999(polkitd), 998(libstoragemgmt), 997(chrony)
   * `polkitd` is a system wide privilege controller
   * `libstoragemgmt` A library for storage management (API)
   * `chrony` Netowrk Time Protocol (NTP) uses port 323
