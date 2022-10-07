# Cisco IOS Cheat Sheet

### Documentation <a href="#commands-to-navigate-different-modes-on-a-cisco-switch-router-enable-config-t...-and-how-you-know-wh" id="commands-to-navigate-different-modes-on-a-cisco-switch-router-enable-config-t...-and-how-you-know-wh"></a>

[Documentation](https://www.cisco.com/c/en/us/td/docs/ios/fundamentals/command/reference/cf\_book/cf\_c1.html)

### EXEC Modes <a href="#commands-to-navigate-different-modes-on-a-cisco-switch-router-enable-config-t...-and-how-you-know-wh" id="commands-to-navigate-different-modes-on-a-cisco-switch-router-enable-config-t...-and-how-you-know-wh"></a>

* If terminal reads `Router>` type `enable` to enter `Router#`
  * Under `Router>` you're allowed to do `ping, show, enable, etc...`
* If terminal reads `Router#` type `config` to enter `Router(config)#`
  * Under `Router#` you're allowed to do `all User EXEC Commands, debug commands, reload, configure(config), etc...`
* If terminal reads `Router(config)#` view the Official Guide because config branches into 3 different sections.
  * Under `Router(config)#` you're allowed to do `hostname, enable secret, ip route, interface (ethernet, serial, bri, etc...), router (rip, ospf, igrp, etc...), line (vty, console, etc...)`
* ​[Official Cisco Guide](https://www.cisco.com/E-Learning/bulk/public/tac/cim/cib/using\_cisco\_ios\_software/02\_cisco\_ios\_hierarchy.htm) (Below is image and table included on the website)

<figure><img src="https://www.cisco.com/E-Learning/bulk/public/tac/cim/cib/using_cisco_ios_software/mod_pix/iostree.gif" alt=""><figcaption><p>Image from Cisco Website</p></figcaption></figure>

| EXEC Mode                  | Decription                                                                                       |
| -------------------------- | ------------------------------------------------------------------------------------------------ |
| **Router>**                | User EXEC mode                                                                                   |
| **Router#**                | Privileged EXEC mode                                                                             |
| **Router(config)#**        | Configuration mode (notice the # sign indicates this is accessible only at privileged EXEC mode) |
| **Router(config-if)#**     | Interface level within configuration mode                                                        |
| **Router(config-router)#** | Routing engine level within configuration mode                                                   |
| **Router(config-line)#**   | Line level (vty, tty, async) within configuration mode                                           |
