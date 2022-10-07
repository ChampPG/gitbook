# Lab 4.1: Console Access Mini-Lab

### Summary

During this lab we got our hands on real CISCO hardware and were able to tinker with the CLI.

### Steps to Setup Computer

1. After connection to the console port open `Device Manager`
   1. Take now of the COM\<Num> is. This will be used later in the PuTTY config
2. You want the setting to be the same as the table below

| Variable     | Value |
| ------------ | ----- |
| Bits per sec | 9600  |
| Data bits    | 8     |
| Parity       | None  |
| Stop bits    | 1     |
| Flow Control | None  |

&#x20; 3\. Now open PuTTY and navigator to `Serial` under `SSH`

<figure><img src="../.gitbook/assets/Screenshot 2022-09-24 145237 (1).png" alt=""><figcaption><p>Shows the PuTTY config</p></figcaption></figure>

&#x20; 4\. Now under Session Select the COM\<Num> from earlier

<figure><img src="../.gitbook/assets/Screenshot 2022-09-24 145607.png" alt=""><figcaption><p>Session Config</p></figcaption></figure>

&#x20; 5\. Click `Open` and if everything was setup properly you should be in the CISCO CLI

### CISCO Steps to clear config

1. Say `no` if prompted to run setup wizard
2. Enter privileged mode `enable`
3. Enter the command `write erase`, which erases the NVRAM file system and removes all files.
4. At the prompt, confirm that you want to erase all files.
5. Enter command `reload`, and enter `no` when prompted whether to save the configuration. (Otherwise, the switch will reload the current running configuration.)
6. Confirm that you want to reload the switch, and your switch configuration is almost clean.
7. Upon reboot, say `no` if prompted to run setup wizard

