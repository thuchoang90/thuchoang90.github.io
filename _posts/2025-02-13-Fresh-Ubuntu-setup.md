---
layout: post
title: Fresh Ubuntu (24.04) setup for working with RISC-V
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

If your machine needs proxy, replace the **http://[address]:[port]** with your proxy address: (don't do this if you don't have proxy)
```shell
$ echo 'Acquire::http::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf
$ echo 'Acquire::https::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf
$ echo 'Acquire::ftp::proxy "http://[address]:[port]";' | sudo tee -a /etc/apt/apt.conf
```

Update & upgrade everything:
```shell
$ sudo apt update
$ sudo apt upgrade
```

Install dependencies:
```shell
$ sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip \
python3-tomli libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex \
texinfo gperf libtool patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake \
libglib2.0-dev libslirp-dev minicom npm perl make g++ ccache net-tools wget gcc \
patch vim-common device-tree-compiler uuid-dev unzip cpio rsync expat screen expect \
makeself libusb-dev libyaml-dev libftdi-dev pkg-config llvm clang verilator libusb-1.0-0-dev
```

If your machine needs proxy, replace the **http://[address]:[port]** with your proxy address: (don't do this if you don't have proxy)
```shell
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

When working with RISC-V, you will be using Github all the times. These are some tips for using Github:

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
Sbt will compile Scala to Java. Then, executing Java will give us FIRRTL. And finally, a FIRRTL compiler will compile FIRRTL to the actual Verilog code.

In short: Scala -> Java -> FIRRTL -> Verilog (1st arrow is done by SBT, 2nd arrow is done by Java, and 3rd arrows is done by FIRRTL compiler)

Now we need to install sbt. Follow the [scala-sbt.org](https://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html) to install.

### II. c) QEMU

QEMU is an emulation tool, not a simulation tool. It does not simulate anything (.v codes, .scala codes, or .c codes, etc.).
It emulates the behavioral that a correct CPU should behave.
Reference link: [github](https://github.com/qemu/qemu) and [wiki](https://wiki.qemu.org/Documentation/Platforms/RISCV).

To install the RISC-V QEMU:
```shell
stand where you want to install RISC-V QEMU
$ git clone https://github.com/qemu/qemu.git riscv-qemu
$ cd riscv-qemu/
$ git checkout stable-9.2   #commit cac3fb44 on 8-Feb-2025
$ git submodule update --init --recursive
$ mkdir build
$ cd build
$ ../configure --target-list=riscv64-softmmu
$ make -j`nproc`
```

### II. d) Visual Studio Code

Let's download a GUI for our programming.
Just follow the guide from [code.visualstudio.com](https://code.visualstudio.com/docs/setup/linux).

### II. e) OpenOCD

Open OCD (OCD: On-Chip Debugger) is a tool to control a CPU via a debugger, thus allowing us to load a program, and run or debug that program.

To install & make OpenOCD:
```shell
$ git clone https://github.com/riscv/riscv-openocd.git    #branch riscv commit 8f595704 on 31-Jan-2025
$ cd riscv-openocd/
$ git submodule update --init --recursive
$ cd jimtcl/
$ ./configure
$ make -j`nproc`
$ sudo make install
$ cd ../
$ ./bootstrap
$ ./configure --enable-ftdi --enable-dummy
$ make -j`nproc`
$ sudo make install
```

Configuration files for RISC-V CPU: [riscv-openocd](/assets/sources/other/riscv-openocd.cfg)
You should download them and put them under the ```riscv-openocd/``` folder.

### II. f) Vivado

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

First, download the Vivado for Linux from [xilinx.com](https://www.xilinx.com/support/download.html) (linux .bin file self extract). Then, cd to the downloaded .bin file and run:
```shell
$ chmod +x FPGAs_....bin
$ ./FPGAs_....bin
```

The GUI for installation will be load. Choose to install the **Vivado** and then **Vivado ML Standard** and wait for the installer to complete.

**Install cable driver:**
```shell
cd to Vivado installed folder:
$ cd ...Xilinx/Vivado/2024.2/data/xicom/cable_drivers/lin64/install_script/install_drivers/
$ sudo ./install_drivers
```

### II. g) Quartus

Just download from the [fpgasoftware.intel.com](http://fpgasoftware.intel.com/?edition=standard&platform=linux&download_manager=direct) and install.
Choose to download the **Quartus Prime Standard Edition**.
Similarly, cd to the downloaded .bin file and run:
```shell
$ chmod +x qinst-....bin
$ ./qinst-....bin
```

The Quartus execution file is located at ```intelFPGA/23.1std/quartus/bin/quartus```

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

Current mainstream is gcc 14.2.
If you want to use older gcc (recommend 8.2), just check out that version.
```shell
GCC 14.2:   $ git checkout 795267df36fcf1269f2bd596ac42e0e91ad9cfd3
GCC 13.2:   $ git checkout 0e53b8d56232236dd74b586c1568295a2985910e
GCC 12.2:   $ git checkout 9f0c0979e205c580ced4a06fb10ddf9095cfd400
GCC 11.1:   $ git checkout 52735e2177f762388cdc6212680e6bf4c0c2f899
GCC 10.2:   $ git checkout a838c5dfe91c3ef29218747fa266ce24ae2cf052
GCC 9.2:    $ git checkout 41775b55a038d10068664e819628a15e45f60055
GCC 8.3:    $ git checkout afcc8bc655d30cf6af054ac1d3f5f89d0627aa79
GCC 8.2:    $ git checkout 7d6d68fb1d1c553dd0ee8b48352667032d389f61
GCC 7.1:    $ git checkout 4e51f2641f21f1f37640c788b7f438d2f0968a3c
GCC 6.1:    $ git checkout 7fb29464d64c6fcac83ef6b2346db0f0c6c01c23
GCC 5.3:    $ git checkout 105ffc3043c234d82b792b7e6950f286ff2bc65d
GCC 4.9:    $ git checkout 1743584a9ee845e4dd507bcbe18a83cb1c2a7579
```

Finally:
```shell
$ git submodule update --init --recursive
```

Note: if it prints:
```shell
   fatal: clone of 'git://...
   Failed to clone ... Retry scheduled
```

Then:
```shell
$ git config --global url."https://github.com/qemu".insteadOf git://git.qemu-project.org
$ git config --global url."https://gitlab.freedesktop.org/pixman/pixman".insteadOf git://anongit.freedesktop.org/pixman
$ git config --global url."https://".insteadOf git://
$ git submodule update --init --recursive
```

### III. b) Config & Make

The configuration command format:
```shell
$ ./configure --prefix=[path] --enable-multilib

For example:
$ ./configure --prefix=/opt/riscv --enable-multilib
```
For other configurations, follow: https://github.com/riscv-collab/riscv-gnu-toolchain

Now you can ```$ make``` the toolchain by:
```shell
for elf-toolchain (or baremetal toolchain) to run directly on the CPU (like MCU):
$ sudo make -j`nproc`

for linux-toolchain to run on the Linux that run on the CPU (like OS app):
$ sudo make linux -j`nproc`
```

*Note*: to re-make another configuration, it is better to ```$ sudo make clean``` beforehand.
