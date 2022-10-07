# Lab 3.0: CentOS Intro

### Summary

In this lab we got a CentOS Virtual Machine and had to set it up on our network along with add it to the Active Directory. We then fought with the CentOS machine for a long time trying to figure out why the windows machine wont let us ping it and then we figured out windows doesn't allow pings by default. We then were able to ssh into the CentOS machine through the Windows Workstation. We then learned some commands and found out about command history and how to delete it.

### Commands

#### Linux

1. `ifconfig` Shows details for connected network adapters
2. `cd` Change location in file system
   * `cd ..` goes back to the parent directory
   * `~` normally means you're in the user folder/directory
   * `/` means you're in the root folder/directory
3. `ls` Show what's in a folder/location
   * `ls -l` shows a more detailed list of folders along with the read, write, execute groups
   * `ls -la` shows every `ls -l` does along with hidden files
4. `nano` Basic text editor in terminal
5. `cat` Reads out a file in terminal
6. `systemctl restart network` Reset the network adapter
7. `hostnamectl set-hostname ___` Set the host name \_\_\_ is where you put host name
8. `nmtui` GUI network interface to setup network config
9. `ping` Sends packets to desired location and gives a response if they made it or not
   * **Linux:** after ping use `-c_` the \_ is the location for the number of pings
   * **Windows:** after ping use `-n _` the \_ is the location for the number of pings
10. `pwd` Shows the present working directory
11. `man` Gives description if a command
    * `man tree` will give description of tree
    * almost the same as doing `tree --help`
12. `mkdir` creates a new directory
    * `mkdir sys255` would create a directory called sys255 in current location
13. `sudo yum install -y tree` yum is a package manager and this command will install `tree`
14. `groups` Shows the username then what group they belong to
15. `sudo -i` gives root control till disabled
16. `whoami` Shows user
17. `exit` logs out
    * if done after `sudo -i` this will just turn you back to the normal user
18. `history | head -n 10` shows the last 10 commands that were run
    * `|` is called a pipe
    * `cat /dev/null >/.bash_history` will delete history
