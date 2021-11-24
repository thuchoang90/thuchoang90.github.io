---
layout: post
title: Fresh Ubuntu machine setup for working with RISC-V
categories: Tutorial
tags: RISC-V
---

## I. Dependencies & Proxy

To make **vi** more comfortable:
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
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt install openjdk-8-jdk
```

Then install dependencies:

```$ sudo apt-get install autoconf automake autotools-dev curl libmpc-dev libmpfr-dev libgmp-dev libusb-1.0-0-dev gawk build-essential bison flex texinfo gperf libtool libssl-dev libpixman-1-dev patchutils bc zlib1g-dev libglib2.0-dev binutils-dev libboost-all-dev device-tree-compiler pkg-config libexpat-dev python libpython-dev python-pip python-capstone virtualenv git make g++ libusb-1.0.0-dev libusb-dev libyaml-dev xorg-dev libudev-dev libts-dev libgl1-mesa-dev libglu1-mesa-dev libasound2-dev libpulse-dev libopenal-dev libogg-dev libvorbis-dev libaudiofile-dev libfreetype6-dev libdbus-1-dev libdirectfb-dev libsdl2-dev```

And other dependencies:

```$ sudo apt install gnutls-bin uuid-dev libpopt-dev libncurses5-dev libncursesw5-dev unzip glib2.0 expat gcc tmux wget bzip2 patch vim-common lbzip2 expect makeself patch npm libexpat1-dev device-tree-compiler cpio rsync cmake llvm-9-dev clang-9 libclang-9-dev```
	
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

The source code for hardware is written in scala language by using the Chisel library.
The sbt is the tool to compile the scala codes.
Sbt is used to generate java codes from the scala codes, then later on, java generates firrtl codes from the java codes,
and finally, from firrtl codes to the actual verilog codes.

First, we need to install the scala.
You can follow the [scala-lang.org](https://www.scala-lang.org/download/) to download the deb file and install
(recommend to install at least the 2.12.4 version).

Then download the sbt tool according to the [scala-sbt.org](https://www.scala-sbt.org/release/docs/Installing-sbt-on-Linux.html).
Download the deb file and install (recommend to install at least the 1.2.8 version).

### II. c) Verilator

Verilator is a cycle-accurate behavioral model, and it is used to simulate the Verilog codes at cycle level (like ModelSim).

To install the Verilator:
```shell
stand where you want to install Verilator
$ git clone http://git.veripool.org/git/verilator
$ cd verilator/
$ git checkout v4.032
$ unset VERILATOR_ROOT    #For bash, unsetenv for csh
$ autoconf                #this is to create the ./configure script
$ ./configure             #then run the script
$ make -j`nproc`
$ sudo make install
```

### II. d) QEMU

QEMU is an emulation tool, not a simulation tool. It does not simulate anything (.v codes, .scala codes, or .c codes, etc.).
It emulates the behavioral that a correct CPU should behave. Reference [link](https://github.com/riscv/riscv-qemu/tree/riscv-qemu-4.0.0).

To install the RISC-V QEMU:
```shell
stand where you want to install RISC-V QEMU
$ git clone https://github.com/riscv/riscv-qemu.git
$ cd riscv-qemu/
$ git checkout riscv-qemu-4.0.0   #commit 62a172e on 19-Mar-2019
$ git submodule update --init --recursive
$ mkdir build
$ cd build
$ ../configure
$ make -j`nproc`
```

### II. e) Idea IntelliJ

**Idea IntelliJ** is a tool for compiling scala codes. It much more like a GUI for the SBT tool.
After download the **Idea IntelliJ** from [jetbrains.com](https://www.jetbrains.com/idea/), extract it and run it by **./idea.sh**

### II. f) Eclipse

Eclipse is the tool for writing software codes (C/C++), to build, to run, and to debug the software.

Download the gnu-mcu-eclipse (linux version) from the [website](https://github.com/gnu-mcu-eclipse/org.eclipse.epp.packages/releases).
Then extract it and copy the folder to any place you want. The execution file is at: ***\[Eclipse folder\]/eclipse/eclipse***

You will be aksed to install plugins at the first launch of the program, remember to choose install the Scala language support.

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
You should download them and put them under the riscv-openocd/ folder.
