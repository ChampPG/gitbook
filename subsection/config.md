# Config

### CISCO Steps to clear config

1. Say `no` if prompted to run setup wizard
2. Enter privileged mode `enable`
3. Enter the command `write erase`, which erases the NVRAM file system and removes all files.
4. At the prompt, confirm that you want to erase all files.
5. Enter command `reload`, and enter `no` when prompted whether to save the configuration. (Otherwise, the switch will reload the current running configuration.)
6. Confirm that you want to reload the switch, and your switch configuration is almost clean.
7. Upon reboot, say `no` if prompted to run setup wizard

```
router>enable
router#write erase
router#reload
```

### Running Config Save

Fully written out

```
switch#copy running-config startup-config
```

Short version

```
switch#copy run start
```
