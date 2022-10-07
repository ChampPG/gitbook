# Lab 7.0: Apache

### Summary



### Commands

* `vi /etc/ssh/sshd_config` - about to change the SSH settings
* `sudo yum install httpd` - install httpd service
* `firewall-cmd --add-service="service" --permanent` - to allow a service through the firewall
* `yum install -y php` - install php

### Steps

#### Get http service

1. setup like any other Linux box
2. `vi /etc/ssh/sshd_config` find lime `#PermitRootLogin yes` change `yes` to `no` and get rid of the `#`
3. `sudo yum install httpd` - stall http service
4. allow http and https throught the firewall `firewall-cmd --add-service=http --permanent` and `firewall-cmd --add-service=https --permanent`
5. connect to webiste through `hostname`

#### PHP setup

1. `yum install -y php` - install php
2. `vi /var/www/html/index.php` this allows you to edit the `hostname/index.php` page
   * the `/var/www/html` is where all website-related documents are stored

#### Join Linux to domain

1. `sudo yum install realmd samba samba-common oddjob oddjob-mkhomedir sssd`
2. `realm join --user=your-domain-admin-username@yourdomain.local yourdomain.local realm list`
