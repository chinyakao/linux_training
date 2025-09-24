# Build Kernel Module - dell_wmi_sysman
Kernel Version: Linux u-Vostro-3420 5.14.0-1054-oem #61-Ubuntu SMP Fri Oct 14 13:05:50 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
## Create Module
1. Download folder https://github.com/torvalds/linux/tree/master/drivers/platform/x86/dell/dell-wmi-sysman
2. Download file https://github.com/torvalds/linux/blob/master/drivers/platform/x86/firmware_attributes_class.h
3. Put them in same folder
4. Modify `sysman.c` line 16
    ``` (Original)
    #include "../../firmware_attributes_class.h"
    ```
    to
    ``` (Revised)
    #include "firmware_attributes_class.h"
    ```
5. Print anything in the module to test

## Compile Module - Makefile
Modify Makefile to make the module have the target directory ana make it in terminal

```
make
```

It will create multiple files

## Remove the original module
```
sudo rmmod dell_wmi_sysman
sudo lsmod | grep "dell_wmi_sysman"
```
and shows nothing

## Install self build module
```
sudo insmod dell_wmi_sysman.ko
sudo lsmod | grep "dell_wmi_sysman"
```
and shows 
```
ell_wmi_sysman        40960  0
firmware_attributes_class    16384  1 dell_wmi_sysman
wmi                    32768  5 dell_wmi_sysman,dell_wmi,wmi_bmof,dell_smbios,dell_wmi_descriptor

```

## Check Sys Log
```
dmesg
```

It will show

```
[ 6650.821650] rtw_8821ce 0000:03:00.0: firmware failed to leave lps state
[ 7212.670956] RILEY SAY HELLO !
[ 7252.813657] RILEY SAY GOODBYE !
```

###### REF
- https://jerrynest.io/how-to-write-a-linux-kernel-module/
