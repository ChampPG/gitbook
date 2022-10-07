# Lab 4.0: Ansible

### Summary

This lab was very interesting I want to understand Ansible more thought because I feel I don't fully understand it.

#### Ansible Commands and Steps

* `sudo apt install ansible sshpass python3-paramiko` - This installs all dependencies and ansible
* Make user with the same passwork to be used as deployer
* `keygen -t rsa -C <user>`
* `ssh-copy-id -i ~/.ssh/mykey.pub <user>@<host>`
* `vi /etc/sudoers.d/sys265` - to look like the following | this allows a user to enter sudo without password

```
 <user>           ALL=(ALL)           NOPASSWD: ALL
```

* Now create `inventory.txt` if applicable make this in a dir called ansible

```
[role_name]
<host_ip> or <hostname>
```

* `ansible all -m ping -i inventory.txt` - This is an easy way to test if the inventory is setup right
* `ansible-galaxy install <package> -p <dir>/` - This is used to install packages for ansible
* `ansible-playbook -i invetory.txt <dir>/<path.yml>`

#### My Playbook for java

* `ansible-galaxy install gantsign.java`

```
- hosts: java
  roles:
         - roles: gantsign.java
```
