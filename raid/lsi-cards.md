# LSI Cards

## Updating LSI Firmware:

1. Download zip from this link: [https://www.truenas.com/community/resources/lsi-9300-xx-firmware-update.145/download](https://www.truenas.com/community/resources/lsi-9300-xx-firmware-update.145/download)
2. Unzip the .zip file
3. Copy the SAS9300\_xx\_IT.bin
4. `sas3flash -o -f SAS9300_xx_IT.bin`

The output of last command should look like the the following:

```
Avago Technologies SAS3 Flash Utility
Version 16.00.00.00 (2017.05.02)
Copyright 2008-2017 Avago Technologies. All rights reserved.

Advanced Mode Set

Adapter Selected is a Avago SAS: SAS3008(C0)

Executing Operation: Flash Firmware Image

Firmware Image has a Valid Checksum.
Firmware Version 16.00.12.00
Firmware Image compatible with Controller.

Valid NVDATA Image found.
NVDATA Major Version 0e.01
Checking for a compatible NVData image...

NVDATA Device ID and Chip Revision match verified.
NVDATA SubSystem Vendor and SubSystem Device ID match verified.
NVDATA Versions Compatible.
Valid Initialization Image verified.
Valid BootLoader Image verified.

Beginning Firmware Download...
Firmware Download Successful.

Verifying Download...

Firmware Flash Successful.

Resetting Adapter...
Adapter Successfully Reset.

NVDATA Version 0e.01.00.07
Finished Processing Commands Successfully.
Exiting SAS3Flash.
```
