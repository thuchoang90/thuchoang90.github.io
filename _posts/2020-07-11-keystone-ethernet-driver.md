---
layout: post
title: "Keystone: turn on ethernet driver"
categories: Project
tags: RISC-V TEE
---

## I. USB & Ethernet Drivers

There are two ways of doing this, the **formal** way, and the **shortcut** way.
But first, check the ```PATH```:
```shell
$ echo ${PATH}                      #and MAKE SURE that NO ANY TOOLCHAIN is on the PATH
$ cd <your keystone folder>         #go to your keystone folder
$ . source.sh
$ export KEYSTONE_DIR=`pwd`

$ cd <your keystone-demo folder>    #go to your keystone-demo folder
$ . source.sh
```

### I. a) Make the 'formal' way

The proper way to modify drivers in Linux kernel is open the kernel, select or diselect some drivers, apply the changes, and remake everything.
```shell
$ cd <your keystone folder>
$ make -f hifive.mk linux-menuconfig
```

Wait for the GUI to load, then:
  1. Device drivers -> Network device support -> USB network adapters
  2. choose the appropriate drivers and turn them on (usually they are the RTL** something)
  3. Exit to go back to the Network device support page
  4. Now go to Ethernet driver support page
  5. choose the appropriate drivers and turn them on (mostly they are the Intel and Realtek ones)
  6. Now just keep Exit till the end and choose Yes when asked to save the new configurations

This line is for applying the new config file into the build file:
```shell
$ cp hifive-conf/linux_defconfig hifive-conf/linux_cma_conf
```

Finally, remake everything:
```shell
$ make clean

If keystone-rv64:	$ make image -j`nproc`
If keystone-rv32:	$ make -j`nproc`
```

### I. b) Make the 'shortcut' way

So, the bottom line of the **formal** way above is just to creating a new ***linux_cma_conf*** file under the ```hifive-conf/``` folder.
Then, I give you the prebuilt file of [linux_cma_conf](/assets/sources/teehw/linux_cma_conf). Just download it, then:

  - Copy the ***linux_cma_conf*** file to your ```<keystone folder>/hifive-conf/linux_cma_conf```.
  - Check the PATH.
  - Finally:

```shell
$ make clean
$ make -j`nproc`
```

### I. c) Keystone-demo: remember to update hash

After your changes on the kernel, the hash value of the **bbl.bin** is different now.
So if you want to use the keystone-demo, you have to reapply the hashes to the **bbl.bin** image file:
```shell
$ cd <your keystone-demo folder>    #go to your keystone-demo folder
$ make getandsethash
$ rm trusted_client.riscv
$ make trusted_client.riscv
$ make copybins

$ cd <your keystone folder>         #go to your keystone folder and update the bbl.bin there

If keystone-rv64:   $ make image -j`nproc`	
If keystone-rv32:   $ make -j`nproc`
```
