# Lab 8-1B Add OSPF Authenication

### Summary

During this lab we added OSPF Authentication to the framework from the lab [Lab 8-1B OSPF PT Activity](lab-8-1b-ospf-pt-activity.md)

### Steps

Border: enable config t interface GigabitEthernet 0/0 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest

East: enable config t interface GigabitEthernet 0/0 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest

Data Center: enable config t interface GigabitEthernet 0/0 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest interface GigabitEthernet 0/1 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest interface GigabitEthernet 0/2 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest

West: enable config t interface GigabitEthernet 0/0 ip ospf message-digest-key 1 md5 testing ip ospf authentication message-digest

#### Border Router:

```
enable 
config t 
interface GigabitEthernet 0/0 
ip ospf message-digest-key 1 md5 testing 
ip ospf authentication message-digest
```
