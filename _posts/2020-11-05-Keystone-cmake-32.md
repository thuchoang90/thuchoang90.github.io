---
layout: post
title: "Keystone 32-bit build using CMake"
categories: Project
tags: RISC-V TEE Linux
---

## I. Keystone

*Note:* because their prebuilt toolchain is ```RV64GC```, so for the ```RV32GC``` or ```RV32IMAC``` build we'll using our local toolchain only.

Git clone:
```shell
If build for RV32GC:
$ git clone -b dev-rv32-cmake https://github.com/thuchoang90/keystone.git keystone-rv32gc
$ cd keystone-rv32gc/

If build for RV32IMAC:
$ git clone -b dev-rv32-cmake https://github.com/thuchoang90/keystone.git keystone-rv32imac
$ cd keystone-rv32imac/
```

Check PATH:
```shell
$ echo ${PATH}    #check if our toolchain is on the PATH or not

If not then export it to PATH:
If build for RV32GC:      $ export RISCV=/opt/GCC8/riscv32gc      #point to RV32GC toolchain
If build for RV32IMAC:    $ export RISCV=/opt/GCC8/riscv32imac    #point to RV32IMAC toolchain

Finally:
$ export PATH=$RISCV/bin/:$PATH
$ export KEYSTONE_DIR=`pwd`
$ export KEYSTONE_SDK_DIR=`pwd`/sdk
```

Update submodule:
```shell
$ ./fast-setup.sh   #this time, it won't download the prebuilt toolchain, just update the submodule

$ make -C sdk       #make sdk
$ export EYRIE_DIR=`pwd`/sdk/rts/eyrie
$ ./sdk/scripts/init.sh --runtime eyrie --force
```

Create build folder:
```shell
$ mkdir build
$ cd build/
```

Make:
```shell
$ cmake .. -DRISCV32=y
$ make -j`nproc`
```

Build the keystone-test:
```shell
$ sed -i 's/size_t\sfreemem_size\s=\s48\*1024\*1024/size_t freemem_size = 2*1024*1024/g' ../sdk/examples/tests/test-runner.cpp
  #this line is for FPGA board, because usually there is only 1GB of memory on the board
$ make run-tests    #after this, a bbl.bin file is generated
```
