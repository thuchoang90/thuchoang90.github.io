---
layout: post
title: Fresh Ubuntu machine setup for working with RISC-V
categories: Tutorial
tags: RISC-V
---

## I. Dependencies & Proxy

To make ```vi``` more comfortable:
```shell
$ sudo apt install vim
$ vi ~/.vimrc
```

Then add this two lines below:
```shell
set nocompatible
syntax on
```

Update & upgrade everything:
```shell
If your machine has proxy, replace the **http://[address]:[port]** with your proxy address:
$ echo 'Acquire::http::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf
$ echo 'Acquire::https::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf
$ echo 'Acquire::ftp::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf

$ sudo apt update
$ sudo apt upgrade
$ sudo apt install openjdk-8-jdk
```

Then install dependencies:

```
$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev
$ sudo apt-get install libusb-1.0-0-dev gawk build-essential bison flex texinfo gperf libtool libssl-dev
$ sudo apt-get install libpixman-1-dev patchutils bc zlib1g-dev libglib2.0-dev binutils-dev libboost-all-dev
$ sudo apt-get install device-tree-compiler pkg-config libexpat-dev python libpython3-dev python-pip-whl
$ sudo apt-get install python-capstone virtualenv git make g++ libusb-1.0.0-dev libusb-dev libyaml-dev xorg-dev
$ sudo apt-get install libudev-dev libts-dev libgl1-mesa-dev libglu1-mesa-dev libasound2-dev libpulse-dev
$ sudo apt-get install libopenal-dev libogg-dev libvorbis-dev libaudiofile-dev libfreetype6-dev libdbus-1-dev
$ sudo apt-get install libdirectfb-dev libsdl2-dev ninja-build dialog
$ sudo apt-get install libncurses5 libncurses5-dev libncursesw5 libncursesw5-dev libtinfo5 libtinfo-dev
```

And other dependencies:

```
$ sudo apt install gnutls-bin uuid-dev libpopt-dev libncurses5-dev libncursesw5-dev unzip expat gcc tmux wget
$ sudo apt install bzip2 patch vim-common lbzip2 expect makeself patch npm libexpat1-dev device-tree-compiler
$ sudo apt install cpio rsync cmake llvm-9-dev clang-9 libclang-9-dev
```
	
And the final dependency:
```shell
For Ubuntu version > 16.04:
$ sudo apt-get install libpng-dev

For Ubuntu version < or = 16.04:
$ sudo apt-get install libpng12-dev
```

Update proxy if your machine has proxy:
```shell
Replace the **http://[address]:[port]** with your proxy address:

for wget
$ echo 'http_proxy = http://[address]:[port]/' | sudo tee -a /etc/wgetrc
$ echo 'https_proxy = http://[address]:[port]/' | sudo tee -a /etc/wgetrc
$ echo 'ftp_proxy = http://[address]:[port]/' | sudo tee -a /etc/wgetrc

for git
$ git config --global https.proxy http://[address]:[port]
$ git config --global http.proxy http://[address]:[port]
$ git config --global ftp.proxy http://[address]:[port]

for npm
$ npm config set proxy http://[address]:[port]/
$ npm config set https-proxy http://[address]:[port]/
$ npm config set ftp-proxy http://[address]:[port]/

for curl
$ echo 'proxy = "http://[address]:[port]"' | sudo tee -a ~/.curlrc
```

Finally, reboot the machine.

* * *

## II. RISC-V Tools

### II. a) Github

Some tips for using Github:

To git clone
```shell
$ git clone <link>          #clone and keep the original name for the cloned folder
$ git clone <link> <name>   #clone and change the name for the cloned folder
```

To track your changes
```shell
$ git diff                                        #list the differences of your folder
$ git diff <branch-name>                          #list the differences of your folder compare to another branch
$ git diff <src-branch>..<des-branch>             #list the differences between two branches
$ git diff <commit-hash>                          #list the differences of your folder compare to the old commit
$ git diff <src-commit-hash>..<des-commit-hash>   #list the differences between two commits
```

To update your folder FROM github
```shell
$ git pull                  #pull from the current branch
$ git pull <branch-name>    #pull from another branch
```

To update your folder TO github
```shell
$ git status                          #to see changes for commit
$ git add <file-name> <folder-name>   #first, add every changes of yours
$ git commit -m "<some message>"      #make a commit with <some message> attached
$ git push                            #this one will push to the current branch, OR
$ git push <branch-name>              #push to another branch
```

To switch to another branch and commit
```shell
$ git checkout <branch-name>                    #switch to another branch
$ git checkout <commit-hash>                    #rollback to the old commit in the same branch
$ git checkout -b <branch-name> <commit-hash>   #switch to another branch and rollback to the old commit of that branch
```

To patch file
```shell
$ git diff > patch-file     #export current changes into a patch-file
$ git format-patch <src branch or commit>..<des branch or commit> --stdout > patch-file
                            #export a patch-file from <src branch or commit> to <des branch or commit>
$ patch -p1 < patch-file    #update your folder with the patch-file
```

To see the status of repo
```shell
$ git log
$ git log --oneline
$ git log --all --decorate --oneline --graph
```

### II. b) Scala & sbt:

The source code for hardware is written in the Scala language.

Scala is a language, Chisel is a library.
Scala itself is not originally designed for "hardware coding." But with the Chisel library attached to it, then we have a new way for "hardware coding."

Sbt is a Scala compiler.
Sbt will compile Scala to Java. Then, a generator script will compile Java to FIRRTL. And finally, another generator script will compile FIRRTL to the actual Verilog code.

In short: Scala -> Java -> FIRRTL -> Verilog (1st arrow is done by SBT, 2nd & 3rd arrows are done by Java)

Now we need to install Scala and sbt.
For Scala, follow the [scala-lang.org](https://www.scala-lang.org/download/) to install.
For sbt, follow the [scala-sbt.org](https://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html) to install.

### II. c) Verilator

Verilator is a cycle-accurate behavioral model, and it is used to simulate the Verilog codes at cycle level (like ModelSim).

To install the Verilator:
```shell
stand where you want to install Verilator
$ git clone http://git.veripool.org/git/verilator
$ cd verilator/
$ git checkout stable
$ unset VERILATOR_ROOT    #For bash, unsetenv for csh
$ autoconf                #this is to create the ./configure script
$ ./configure             #then run the script
$ make -j`nproc`
$ sudo make install
```
In general, follows the guide here to install: https://verilator.org/guide/latest/install.html

### II. d) QEMU

QEMU is an emulation tool, not a simulation tool. It does not simulate anything (.v codes, .scala codes, or .c codes, etc.).
It emulates the behavioral that a correct CPU should behave.
Reference link: [github](https://github.com/qemu/qemu) and [wiki](https://wiki.qemu.org/Documentation/Platforms/RISCV).

To install the RISC-V QEMU:
```shell
stand where you want to install RISC-V QEMU
$ git clone https://github.com/qemu/qemu.git riscv-qemu
$ cd riscv-qemu/
$ git checkout stable-5.0   #commit 386b2a57 on 15-Sep-2020
$ git submodule update --init --recursive
$ mkdir build
$ cd build
$ ../configure --target-list=riscv64-softmmu --disable-werror
$ make -j`nproc`
```

### II. e) Idea IntelliJ

**Idea IntelliJ** is a GUI for sbt (which is a scala compiler).
After download the **Idea IntelliJ** from [jetbrains.com](https://www.jetbrains.com/idea/), extract it and run it by ```./idea.sh```

### II. f) Eclipse

Eclipse is an open-source IDE (mostly for C/C++) to build, to run, and to debug a software.

Download the gnu-mcu-eclipse (linux version) from the [website](https://github.com/gnu-mcu-eclipse/org.eclipse.epp.packages/releases).
Then extract it and copy the folder to any place you want. The execution file is at: ```[Eclipse folder]/eclipse/eclipse```

### II. g) OpenOCD

Open OCD (OCD: On-Chip Debugger) is a tool to control a CPU via a debugger, thus allowing us to load a program, and run or debug that program.

To install & make OpenOCD:
```shell
$ git clone https://github.com/riscv/riscv-openocd.git    #branch riscv commit 54e5d253 on 5-Mar-2020
$ cd riscv-openocd/
$ git submodule update --init --recursive
$ ./bootstrap
$ ./configure --enable-ftdi --enable-dummy
$ make -j`nproc`
$ sudo make install -j`nproc`
```

Configuration files for RISC-V CPU: [riscv-openocd](/assets/sources/other/riscv-openocd.cfg)
You should download them and put them under the ```riscv-openocd/``` folder.

### II. h) Vivado 2016.4

(because the VC707 project now can compatible only with the 2016.4 version of Vivado)

**Check your eth0 interface:**

Type ```$ ifconfig -a``` to make sure that the network interface name is ```eth0```.
If not, the Vivado cannot recognize the license from the NAT interface.
Then, the network interface name must be rename by:
```shell
$ sudo vi /etc/default/grub

Then add this line beneath those GRUB... lines:
    GRUB_CMDLINE_LINUX="net.ifnames=0 biosdevname=0"

Then:
$ sudo grub-mkconfig -o /boot/grub/grub.cfg
```

Finally, reboot again for the computer to update the new ethernet interface.

**Download and Install:**

First, download the Vivado 2016.4 from [xilinx.com](https://www.xilinx.com/support/download/index.html/content/xilinx/en/downloadNav/vivado-design-tools/archive.html) (linux .bin file self extract). Then, cd to the downloaded .bin file and run:
```shell
$ chmod +x Xilinx_....bin
$ sudo ./Xilinx_....bin
```

The GUI for installation will be load. Choose to install the Vivado HL Design Edition and wait for the installer to complete.

**Install cable driver:**
```shell
cd to Vivado installed folder:
$ cd ...Xilinx/Vivado/2016.4/data/xicom/cable_drivers/lin64/install_script/install_drivers/
$ sudo ./install_drivers
```

### II. i) Quartus

Just download from the [fpgasoftware.intel.com](http://fpgasoftware.intel.com/?edition=standard&platform=linux&download_manager=direct) and install.
Choose the version you want to download, then from Ubuntu just click and install
(In this tutorial, the chosen Quartus version is Quartus Prime Standard 18.1).
The Quartus execution file is located at ```intelFPGA/18.1/quartus/bin/```

Note: if running Quartus fail due to ```libpng12``` error, then you need to install it manually (just download & install):
for [32-bit](https://launchpad.net/~ubuntu-security/+archive/ubuntu/ppa/+build/15108507/+files/libpng12-dev_1.2.54-1ubuntu1.1_i386.deb),
for [64-bit](https://launchpad.net/~ubuntu-security/+archive/ubuntu/ppa/+build/15108504/+files/libpng12-0_1.2.54-1ubuntu1.1_amd64.deb).

**Install cable driver:**

Create two 51- and 52- files:
```shell
$ sudo vi /etc/udev/rules.d/51-usbblaster.rules
$ sudo vi /etc/udev/rules.d/52-usbblaster.rules
```

And add these lines on both files:
```shell
# USB-Blaster
BUS=="usb", SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6001", MODE="0666"
BUS=="usb", SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6002", MODE="0666" 
BUS=="usb", SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6003", MODE="0666"   

# USB-Blaster II
BUS=="usb", SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6010", MODE="0666"
BUS=="usb", SYSFS{idVendor}=="09fb", SYSFS{idProduct}=="6810", MODE="0666"
```

After that, you may:
```shell
$ sudo service udev restart
```

Or even reboot the computer if it's still not recognize the cable.
	
* * *

## III. RISC-V Toolchain

Toolchain for RISC-V CPU. Reference [link](https://github.com/riscv/riscv-gnu-toolchain).

### III. a) Git clone

Git clone the toolchain-making on github:
```shell
$ git clone https://github.com/riscv/riscv-gnu-toolchain
$ cd riscv-gnu-toolchain/
```

Current mainstream is gcc 11.1
If you want to use older gcc (recommend 8.2 version):
```shell
GCC 11.1:   $ git checkout 995778bd3315faddd709948190ca76fb10b43188
GCC 10.2:   $ git checkout a838c5dfe91c3ef29218747fa266ce24ae2cf052
GCC 10.1:   $ git checkout f13b418e9a2e90308b3881adc13413c933d363ee
GCC 9.2:    $ git checkout 345f419e1f783139dd3353eb09bb3efaa000bad9
GCC 8.3:    $ git checkout afcc8bc655d30cf6af054ac1d3f5f89d0627aa79
GCC 8.2:    $ git checkout fa1fcaba7f883b20e14f1613bf4bb1028bec6e43
GCC 8.1:    $ git checkout af5aa9f3fad527c14b3a8d3885d05d06931070ae
GCC 7.2:    $ git checkout 686320c1fee0519f12117d0b6c9ef22b5fa4db16
GCC 7.1:    $ git checkout dcda255e1f3d114e8d12b23c80b80382b51109d6
GCC 6.1:    $ git checkout 39fb67144cd7228f72c00be330bc80e649105878
GCC 5.3:    $ git checkout 105ffc3043c234d82b792b7e6950f286ff2bc65d
GCC 5.2:    $ git checkout 28fccff586e77d73d1ef58d0e3f2d167065513b0
GCC 5.1:    $ git checkout add1510c7b0f9cdf7e55ebd60d9744d2c740fe24
GCC 4.9:    $ git checkout fe4c7d9583a3c06df08a7f013a901fd6a3456bfd
```

Finally:
```shell
$ git submodule update --init --recursive
```

### III. b) Config & Make

The configuration command format:
```shell
$ ./configure --prefix=[path] --enable-multilib

For example:
$ ./configure --prefix=/opt/riscv --enable-multilib
```
For details on configuration, follows the guide in: https://github.com/riscv-collab/riscv-gnu-toolchain

After install the dependencies, clone the toolchain-making folder, and set the configurations, now you can ```$ make``` the toolchain by:
```shell
for elf-toolchain (or baremetal toolchain) to run directly on the CPU (like MCU):
$ sudo make -j`nproc`

for linux-toolchain to run on the Linux that run on the CPU (like OS app):
$ sudo make linux -j`nproc`
```

*Note*: to re-make again, it is better to ```$ sudo make clean``` beforehand.
