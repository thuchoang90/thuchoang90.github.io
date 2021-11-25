---
layout: post
title: "Keystone 32-bit build using Makefile"
categories: Project
tags: RISC-V TEE
---

## I. Keystone

*Note:* because their prebuilt toolchain is ```RV64GC```, so for the ```RV32GC``` or ```RV32IMAC``` build we'll using our local-toolchain only.

Git clone:
```shell
If build for RV32GC:
$ git clone -b dev-rv32 https://github.com/thuchoang90/keystone.git keystone-rv32gc
$ cd keystone-rv32gc/

If build for RV32IMAC:
$ git clone -b dev-rv32 https://github.com/thuchoang90/keystone.git keystone-rv32imac
$ cd keystone-rv32imac/
```

Check PATH:
```shell
$ echo ${PATH}    #check if our toolchain is on the PATH or not

If not then export it to PATH:
If build for RV32GC:      $ export RISCV=/opt/GCC8/riscv32gc
If build for RV32IMAC:    $ export RISCV=/opt/GCC8/riscv32imac

Finally:
$ export PATH=$RISCV/bin:$PATH
$ export KEYSTONE_DIR=`pwd`
$ export KEYSTONE_SDK_DIR=`pwd`/sdk
```

Update submodule:
```shell
$ ./fast-setup.sh
```

Do the following if build for ```RV32IMAC```, skip if build for ```RV32GC```:
```
$ patch -p1 < patches/rv32imac.patch
```

Finally, make:
```shell
$ make -j`nproc`

$ make -C sdk   #make sdk
$ export EYRIE_DIR=`pwd`/sdk/rts/eyrie
$ ./sdk/scripts/init.sh --runtime eyrie --force
```

Build the keystone-test:
```shell
$ sed -i 's/size_t\sfreemem_size\s=\s48\*1024\*1024/size_t freemem_size = 2*1024*1024/g' ./sdk/examples/tests/test-runner.cpp
  #this line is for FPGA board, because usually there is only 1GB of memory on the board
$ ./sdk/examples/tests/vault.sh
$ make -j`nproc`    #after this, a bbl.bin file is generated in hifive-work/bbl.bin
```

* * *

## II. Keystone-demo

Check PATH:
```shell
#go to your keystone folder
      $ cd keystone-rv32gc/
Or:   $ cd keystone-rv32imac/

$ echo ${PATH}    #check if our toolchain is on the PATH or not

If not then export it to PATH:
If build for RV32GC:      $ export RISCV=/opt/GCC8/riscv32gc      #point to RV32GC toolchain
If build for RV32IMAC:    $ export RISCV=/opt/GCC8/riscv32imac    #point to RV32IMAC toolchain

Finally:
$ export PATH=$RISCV/bin:$PATH
$ export KEYSTONE_DIR=`pwd`
$ export KEYSTONE_SDK_DIR=`pwd`/sdk
```

Git clone:
```shell
$ cd ../    #go back outside
$ git clone -b dev-rv32 https://github.com/thuchoang90/keystone-demo.git keystone-demo-rv32
```

Make:
```shell
$ cd keystone-demo-rv32/
$ . source.sh
$ ./quick-start.sh    #type Y when asked
  #after this step, a new app is generated and coppied to the keystone directory
```

Update keystone-demo to the ```keystone/``` folder:
```shell
$ cd ${KEYSTONE_DIR}    #now go back to the keystone folder
$ make -j`nproc`        #and update the bbl.bin there
```

However, it will be a false attestation. To update the new hash value, do the followings:
```shell
$ cd ../keystone-demo-rv32/   #first, cd back to the keystone-demo directory
$ make getandsethash
$ rm trusted_client.riscv
$ make trusted_client.riscv
$ make copybins
  #after this step, the app is updated with the correct hash value and coppied to the keystone directory

$ cd ${KEYSTONE_DIR}    #now go back to the keystone folder
$ make -j`nproc`        #and update the bbl.bin there
```

* * *

## III. Run Test on QEMU

```shell
$ cd <keystone folder>        #go to your keystone folder
$ ./scripts/run-qemu.sh       #login by the id of 'root' and the password of 'sifive'

$ insmod keystone-driver.ko   #install driver
```

To do the initial test:
```shell
$ time ./tests/tests.ke
```
It is okay if the **Attestation report SIGNATURE is valid** is printed

To do the keystone-demo test:
```shell
$ cd keystone-demo/                   #go to the keystone-demo test
$ ./enclave-host.riscv &              #run host in localhost
$ ./trusted_client.riscv localhost    #connect to localhost and test
```
It is okay if the **Attestation signature and enclave hash are valid** is printed.
Exit the security monitor by: ```$ q```. And exit the QEMU by:  ```$ poweroff```.
