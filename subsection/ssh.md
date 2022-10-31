# SSH

{% embed url="https://www.cisco.com/c/en/us/support/docs/security-vpn/secure-shell-ssh/4145-ssh.html" %}

```
enable
config t
hostname {hostname}
aaa new-model
username {username} password 0 {password}
ip domain-name {domain}
crypto key generate rsa
ip ssh time-out 60
ip ssh authentication-retries 2
line vty 0 4
transport input ssh
```
