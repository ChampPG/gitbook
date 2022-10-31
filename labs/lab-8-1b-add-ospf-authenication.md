# Lab 8-1B Add OSPF Authenication

### Summary

During this lab we added OSPF Authentication to the framework from the lab [Lab 8-1B OSPF PT Activity](lab-8-1b-ospf-pt-activity.md)

### Steps

#### Border Router: Network 1

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```

#### East Router: Network 2

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```

#### Data Center: Network 3

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest 
exit
interface GigabitEthernet 0/1 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest 
exit
interface GigabitEthernet 0/2 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```

#### West Router: Network 4

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```

#### Tips and Tricks

If you run the command below it will show all ospf configuration on the specified interface

```
show ip ospf interface {interface} {interface #}
show ip ospf interface gigabitEthernet 0/0
```

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>command output</p></figcaption></figure>
