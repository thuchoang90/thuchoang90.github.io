---
layout: post
title: "SiFive Freedom: a Rocket-chip computer system"
categories: Project
tags: RISC-V TEE
---

## I. Hardware

SiFive freedom demo on VC707 FPGA board is using the **U540** core with the ISA of ```RV64GC```.
Original [repository](https://github.com/sifive/freedom). Modified [repository](https://github.com/thuchoang90/freedom).

To build on VC707 FPGA, you need Xilinx Vivado design software. Install it in [Fresh-Ubuntu-setup](/tutorial/2020/07/23/Fresh-Ubuntu-setup#h-ii-h-vivado-20164).

### I. a) Build

Git clone:
```shell
$ git clone https://github.com/thuchoang90/freedom.git	
$ cd freedom/
$ git checkout keystone-fpga    #commit 76dd152a on 5-Nov-2019

This will 'submodule update' without download the toolchain again, and also patch the fpga-shells submodule afterward
$ . update.sh
```

#### (i) Make

Before ```$ make```, remember to set the environment (see [I. b) Other Utilities](#i-b-other-utilities)) simply by: ```$ . setenv.sh```

The format for ```$ make``` command is:
```shell
This is for creating .v files:
$ make [CONFIG] [MODEL] [BOOTROM_DIR] [BUILD_DIR] -f Makefile.vc707-u500devkit verilog -j`nproc`

This is for Vivado build:
$ make [CONFIG] [MODEL] [BOOTROM_DIR] [BUILD_DIR] -f Makefile.vc707-u500devkit mcs -j`nproc`
```

The ```[CONFIG]``` option is for selecting the frequency:
```
CONFIG=DevKitU500FPGADesign_WithDevKit50MHz (default value)
       DevKitU500FPGADesign_WithDevKit100MHz
       DevKitU500FPGADesign_WithDevKit125MHz
       DevKitU500FPGADesign_WithDevKit150MHz
```

The ```[MODEL]``` option is for selecting the PCIe option:
```
With PCIe build (default value):
  MODEL=VC707PCIeShell

Without PCIe build:
  MODEL=VC707BaseShell
```

The ```[BOOTROM_DIR]``` option is to specify the bootrom directory that you want to use:
```
Using the sifive's sdboot (default value):
  BOOTROM_DIR=`pwd`/bootrom/sdboot

Using the keystone's zsfl+fsbl boot:
  BOOTROM_DIR=`pwd`/bootrom/freedom-u540-c000-bootloader
```

The ```[BUILD_DIR]``` option is to specify the build directory:
```
BUILD_DIR=`pwd`/builds/<name>

Example:
  BUILD_DIR=`pwd`/builds/vc707-u500devkit
```

Example:
```shell
To build with PCIe, 125MHz, using sifive's sdboot:
$ make CONFIG=DevKitU500FPGADesign_WithDevKit125MHz BUILD_DIR=`pwd`/builds/vc707-u500devkit-withpcie-sdboot -f Makefile.vc707-u500devkit verilog -j`nproc`
$ make CONFIG=DevKitU500FPGADesign_WithDevKit125MHz BUILD_DIR=`pwd`/builds/vc707-u500devkit-withpcie-sdboot -f Makefile.vc707-u500devkit mcs -j`nproc`

To build without PCIe, 150MHz, using sifive's sdboot:
$ make CONFIG=DevKitU500FPGADesign_WithDevKit150MHz MODEL=VC707BaseShell BUILD_DIR=`pwd`/builds/vc707-u500devkit-nopcie-sdboot -f Makefile.vc707-u500devkit verilog -j`nproc`
$ make CONFIG=DevKitU500FPGADesign_WithDevKit150MHz MODEL=VC707BaseShell BUILD_DIR=`pwd`/builds/vc707-u500devkit-nopcie-sdboot -f Makefile.vc707-u500devkit mcs -j`nproc`

To build with PCIe, 125MHz, using keystone's zsbl-fsbl boot:
$ make CONFIG=DevKitU500FPGADesign_WithDevKit125MHz BOOTROM_DIR=`pwd`/bootrom/freedom-u540-c000-bootloader BUILD_DIR=`pwd`/builds/vc707-u500devkit-withpcie-keystoneboot -f Makefile.vc707-u500devkit verilog -j`nproc`
$ make CONFIG=DevKitU500FPGADesign_WithDevKit125MHz BOOTROM_DIR=`pwd`/bootrom/freedom-u540-c000-bootloader BUILD_DIR=`pwd`/builds/vc707-u500devkit-withpcie-keystoneboot -f Makefile.vc707-u500devkit mcs -j`nproc`

To build without PCIe, 150MHz, using keystone's zsbl-fsbl boot:
$ make CONFIG=DevKitU500FPGADesign_WithDevKit150MHz MODEL=VC707BaseShell BOOTROM_DIR=`pwd`/bootrom/freedom-u540-c000-bootloader BUILD_DIR=`pwd`/builds/vc707-u500devkit-nopcie-keystoneboot -f Makefile.vc707-u500devkit verilog -j`nproc`
$ make CONFIG=DevKitU500FPGADesign_WithDevKit150MHz MODEL=VC707BaseShell BOOTROM_DIR=`pwd`/bootrom/freedom-u540-c000-bootloader BUILD_DIR=`pwd`/builds/vc707-u500devkit-nopcie-keystoneboot -f Makefile.vc707-u500devkit mcs -j`nproc`
```

To clean and build again:

 - Remove the ```builds/<name>``` folder
 - If you used the keystone's zsbl-fsbl boot process, then go the ```bootrom/freedom-u540-c000-bootloader/``` folder and ```$ make clean```
 - Finally, go to the top folder and ```$ make``` again.

#### (ii) Notes

**1:** Guide for program & debug on VC707 can be found here: [VC707 program and debug guide](/project/2020/07/24/vc707-program-debug).

**2:** Internal coding structure of the SiFive Freedom folder can be found here: [SiFive Freedom chisel code structure](/project/2020/04/27/freedom-chisel).

**3:** The maximum frequency for the VC707 board with PCIE is 125MHz, and without PCIE is 150MHz.

**4:** Sometime the ```$ make mcs``` end with timing error and did not continue to generate the final mcs files for the flash programming, but still, it did generate the ***.bit*** file. Then, we can manually generate the ***.mcs*** from the ***.bit***:

```shell
$ cd builds/<name>/obj/   #cd to the build folder

For VC707PCIeShell:
$ vivado -nojournal -mode batch -source ../../../fpga-shells/xilinx/common/tcl/write_cfgmem.tcl -tclargs vc707 VC707PCIeShell.mcs VC707PCIeShell.bit

For VC707BaseShell:
$ vivado -nojournal -mode batch -source ../../../fpga-shells/xilinx/common/tcl/write_cfgmem.tcl -tclargs vc707 VC707BaseShell.mcs VC707BaseShell.bit
```

**5:** Built files are under ```builds/<name>/obj/```. The important built files are:

```shell
VC707Shell.v                        #the verilog source code
VC707Shell.mcs and VC707Shell.prm   #the two files for flash programming
VC707Shell.bit                      #the bitstream file for direct programming
```

### I. b) Other utilities

To quickly set build environment:
```shell
$ vi setenv.sh    #and change the correct corresponding paths in your machine

Then from this point forward, you can auto set your environment by simply:
$ . setenv.sh
```

If you want to change the ROM size:
```shell
BootRom size is declared in the file:
	rocket-chip/src/main/scala/devices/tilelink/MaskROM.scala

On the line 12:
	case class MaskROMParams(address: BigInt, name: String, depth: Int = 2048, width: Int = 32)

Change the <depth> value to change the size.
```

If you want to change the modules' addresses, number of CPU cores, etc:
```shell
The declarations are in the file:
	src/main/scala/unleashed/DevKitConfigs.scala

But remember to change the addresses on the software as well. These files:
	bootrom/sdboot/include/platform.h
	bootrom/sdboot/linker/memory.lds
	bootrom/freedom-u540-c000-bootloader/sifive/platform.h
	bootrom/freedom-u540-c000-bootloader/memory_vc707.lds
```

*TODO*: script to auto update ROM size, modules' addresses, and number of CPU to software

### I. c) Use with Idea IntelliJ

Guide to install Idea IntelliJ is in [Fresh-Ubuntu-setup](/tutorial/2020/07/23/Fresh-Ubuntu-setup#h-ii-e-idea-intellij).

To import the freedom folder to the **Idea IntelliJ** tool:

 - If the freedom folder wasn't compiled before, go ahead and ```$ make verilog``` for the first time (no need to ```$ make mcs``` though). This act is just for download the dependencies, because the Idea IntelliJ has trouble with dependencies download.
 - **Big note:** when ```$ make verilog```, please notice that there will be one line looks like this, you should copy it for later use:

```shell
java -jar /home/ubuntu/project/freedom/rocket-chip/sbt-launch.jar ++2.12.4 "runMain freechips.rocketchip.system.Generator /home/ubuntu/project/freedom/builds/chip uec.nedo.chip ChipShell uec.nedo.chip ChipDesignTop"
(the content may be differ on your machine)

In the first time 'make', it usually appears near after this line:
	[success] Total time: xxx s, completed xxx, xxx, xx:xx:xx
In the NOT first time 'make', it usually appears right away
```

 - Open the Idea IntelliJ tool, and choose '*Import Project*'
 - Then choose '*sbt*' then hit '*Next*'
 - Tick the '*for imports*' and '*for builds*' options in the ***Use sbt shell*** then hit '*Finish*'
 - Wait for it to sync for the first time. This first time sync will fail
 - After that, go to the tab ***sbt shell*** and type ***++2.12.4***, and then type ***compile***, and wait!
 - After the compile, go to the ***sbt*** tab on the MOST RIGHT EDGE and hit the reload button, it will re-sync for the second time
 - After the second time sync, if it still fail, I have no idea ¯\\_(ツ)_/¯

To debug with the **Idea IntelliJ** tool:

 - Before debugging it, you have to build it first. Go to the ***sbt shell*** tab and type ***++2.12.4*** then type ***compile***
 - Please notice that there might be a task name *Indexing* still running in the background, wait for it to finish.
 - After 'compile' succeed and '*Indexing*' finished, click the ***Add Configuration...*** button right next to the build button (at the top-bar to the right). Then hit the ***+*** button to add a new configuration, and choose the ***JAR Application*** setting
 - Now get back to the " *java -jar* " example note earlier:
```
java -jar /home/ubuntu/project/freedom/rocket-chip/sbt-launch.jar ++2.12.4 "runMain freechips.rocketchip.system.Generator /home/ubuntu/project/freedom/builds/chip uec.nedo.chip ChipShell uec.nedo.chip ChipDesignTop"
```
   The ***/home/ubuntu/project/freedom/rocket-chip/sbt-launch.jar*** part will go to the ***Path to JAR:***
   
   The ***++2.12.4 "runMain freechips.rocketchip.system.Generator /home/ubuntu/project/freedom/builds/chip uec.nedo.chip ChipShell uec.nedo.chip ChipDesignTop"*** part will go to the ***Program arguments:***
   
   Everythiing else just leave as they are, then click '*Apply*' and '*OK*'. Now you can debug with freedom folder.

* * *

## II. Software

### II. a) Without TEE (KeyStone-build)

Original [repository](https://github.com/sifive/freedom-u-sdk). Modified [repository](https://github.com/mcd500/freedom-u-sdk/).

*TODO*: currently, this way uses the prebuilt toolchain of gcc 7. In the future, this need to be upgraded to the current mainstream toolchain of sifive-freedom, gcc 9.2. Then after that, we can avoid to download the prebuilt toolchain again.

#### (i) Git clone

```shell
$ git clone https://github.com/mcd500/freedom-u-sdk.git
$ cd freedom-u-sdk
$ git checkout linux_u500vc707devkit_config   #commit 29fe529f on 12-Apr-2019
$ git submodule update --init --recursive
```

*Note:* sometimes the **riscv-gnu-toolchain** submodule fails to clone. If that happened, we have to git clone it manually:
```shell
$ rm -rf riscv-gnu-toolchain    #first, remove the corrupted folder
$ git clone https://github.com/riscv/riscv-gnu-toolchain.git    #then clone a new
$ cd riscv-gnu-toolchain/
$ git checkout b4dae89
$ git submodule update --init --recursive
$ cd ../    #get back to the top folder of freedom-u-sdk
```

#### (ii) Make the bbl.bin

```shell
$ unset RISCV   #make sure that there is nothing on the RISCV variable

Export your toolchains to the PATH (both the elf & linux toolchains)
$ export PATH=/opt/riscv64gc/bin/:$PATH

Then 'make' with PCIE:
$ make -j`nproc` BOARD=vc707devkit

or 'make' without PCIE:
$ make -j`nproc` BOARD=vc707devkit_nopci
```

#### (iii) Write SD card & boot on

```shell
$ sudo dd if=work/bbl.bin of=/dev/sdX bs=4096 conv=fsync
  where X is the number of the USB device
```

Put in the SD card to the board, program the board, then wait for the board to boot on. Communicate with the board via UART:
```shell
$ sudo minicom -b 115200 -D /dev/ttyUSBx
  where x is the number of connected USB-UART
  login by the id of 'root' and the password of 'sifive'
```

### II. b) SD card with KeyStone

Reference link: [github.com/keystone-enclave](https://github.com/keystone-enclave/keystone) for the KeyStone project.

#### (i) Partition the SD card

Use the **gptfdisk** tool to create 4 partitions in the SD card.

If you don't have the **gptfdisk tool**, then do the followings to install it:
```shell
$ git clone https://github.com/tmagik/gptfdisk.git    #branch master commit 3d6a1587 on 9-Dec-2018
$ cd gptfdisk/
$ make -j`nproc`
```

To use gptfdisk:
```shell
$ cd gptfdisk/            #go to gptfdisk folder
$ sudo ./gdisk /dev/sd?   #point to the sd-card

Some commands:
$ p   #print partitions information
$ d   #delete partition
$ n   #create new partition
$ w   #write partition
```

The partitions after created:
```shell
Number  Start (sector)  End (sector)  Size        Code    Name
1       2048            67583         32.0 MiB    5202    SiFive bare-metal (...
2       264192          15759326      7.4 GiB     8300    Linux filesystem
4       67584           67839         128.0 KiB   5201    SiFive FSBL (first-...
```

#### (ii) Prepare BBL & FSBL

**For the bbl.bin:**

Follow the [instruction](./keystone.md) to make the **bbl.bin** of the Keystone & Keystone demo.

The **bbl.bin** is for the 1st partition of the SD card:
```shell
$ cd <keystone folder>    #cd to your keystone folder
$ sudo dd if=hifive-work/bbl.bin of=/dev/sdX1 bs=4096 conv=fsync
  where the X1 is the 1st partition of the USB device
```

**For the fsbl.bin:**

After the hardware make (section [I. a)](#i-a-build) above), there is a **vc707fsbl.bin** file inside the folder **bootrom/freedom-u540-c000-bootloader/**. That file is for the 4th partition of the SD card:
```shell
$ cd <your freedom folder>
$ cd bootrom/freedom-u540-c000-bootloader/
$ sudo dd if=vc707fsbl.bin of=/dev/sdX4 bs=4096 conv=fsync
  where the X4 is the 4th partition of the USB device
```

#### (iii) Boot on & run the test

Finally, put in the SD card to the board, program the board, then wait for the board to boot on. Communicate with the board via UART:
```shell
$ sudo minicom -b 115200 -D /dev/ttyUSBx
  where x is the number of connected USB-UART
  login by the id of 'root' and the password of 'sifive'
```

To run the keystone test:
```shell
$ insmod keystone-driver.ko           #install driver
$ time ./tests/tests.ke               #okay if the 'Attestation report SIGNATURE is valid' is printed
$ cd keystone-demo/                   #go to the keystone-demo test
$ ./enclave-host.riscv &              #run host in localhost
$ ./trusted_client.riscv localhost    #connect to localhost and test
```
It is okay if the **Attestation signature and enclave hash are valid** is printed.
