# Tips and Tricks

### Access List Tips

Command below will show access-lists

```
show access-lists
```

Command below will delete access lit

```
enable
conf t
no access-list {access-list-num}
```

### Make Script from Command List

If you're given a command list of

```
Router>enable
Router#configure terminal
Router(config)#hostname R0
R0(config)#interface fastethernet 0/0
R0(config-if)#ip address 30.0.0.1 255.0.0.0
R0(config-if)#no shutdown
R0(config-if)#exit
R0(config)#interface serial 0/0/0
R0(config-if)#ip address 20.0.0.1 255.0.0.0
R0(config-if)#clock rate 64000
R0(config-if)#bandwidth 64
R0(config-if)#no shutdown
R0(config-if)#exit
```

Use [cyberchef](https://gchq.github.io/CyberChef/) with `Find / Replace` to remove the EXEC mode

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

What is happening here is

```
.* is a wildcard 
| means or
[] denotes a character class
```

This means remove anything that comes before a `#` or `>` and replace it with nothing.

```
.*[#|>]
```

Now in packet tracer copy all of the output code and click paste. This will run all of the code line by line.

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>I had run this before so I get the overlap output</p></figcaption></figure>

