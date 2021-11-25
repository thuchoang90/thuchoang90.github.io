---
layout: post
title: "TEE-HW with cryptographic accelerators"
categories: Project
---

Based on the [Chipyard](https://github.com/ucb-bar/chipyard), this hardware dedicates to accelerating the Trusted Execution Environment (TEE).
The TEE-HW has demos on VC707, VCU118, DE4, and TR4 FPGA boards.
The core processors can be configured to use [Rocket-chip](https://github.com/chipsalliance/rocket-chip), [BOOM](https://github.com/riscv-boom/riscv-boom) cores, or both.

## I. Hardware: Make & Build FPGA

Git clone:
```shell
$ git clone -b dev-thuc https://github.com/uec-hanken/tee-hardware.git
$ cd tee-hardware/

Update with firesim:      $ . update.sh
Update without firesim:   $ . update_nosim.sh
```

### I. a) Make (verilog sources)

Export appropriate toolchain to your PATH:
```shell
#check PATH:
$ echo ${PATH}    #check the toolchain is on the PATH or not	

If not, then:
$ export PATH=/opt/riscv64gc/bin/:${PATH}
```

To make for each demo:
```shell
$ cd <to your tee-hardware folder>

For VC707:    $ cd fpga/Xilinx/VC707/
For DE4:      $ cd fpga/Altera/DE4/
For TR4:      $ cd fpga/Altera/TR4/

Finally:
$ make
```

### I. b) Makefile variables

In the **Makefile** of each folder (i.e., *fpga/Xilinx/VC707*, *fpga/Altera/DE4*, and *fpga/Altera/TR4*), these options are available:

| Variable | Availabe option | Description |
| -------- | --------------- | ----------- |
| ISACONF  | - RV64GC<br />- RV64IMAC<br />- RV32GC<br />- RV32IMAC | Select the ISA |
| BOOTSRC  | - BOOTROM<br />- QSPI | Select the boot sources |
| PCIE     | - WPCIe<br />- WoPCIe | Enable/Disable PCIe |
| DDRCLK   | - WSepaDDRClk<br />- WoSepaDDRClk | - Separate system-clock and DDR-clock<br />- Not separate, using the same system-clock |
| HYBRID   | - Rocket<br />- Boom<br />- RocketBoom<br />- BoomRocet | - Dual-core Rocket<br />- Dual-core BOOM<br />- Dual-core hybrid: Rocket 1st, BOOM 2nd<br />- Dual-core hybrid: BOOM 1st, Rocket 2nd |

**About the BOOTSRC**

In the ```BOOTSRC=BOOTROM``` scenario, the **ZSBL** is stored in the **BootROM** inside the FPGA, the **FSBL** & **BBL** are stored outside in the **SD-card** (by different partitions).

In the ```BOOTSRC=QSPI``` scenario, the **ZSBL** is stored in the **Flash** (via QSPI) outside the FPGA, the **BootROM** inside the FPGA now contains just a simple jump instruction that jumps directly to the **Flash** outside. And the **FSBL** & **BBL** are still stored in the **SD-card** as same as before.

**About VC707 demo**

VC707 doesn't have enough GPIOs for QSPI and USB1.1, so the ```BOOTSRC``` variable always equal **BOOTROM** even selected as **QSPI**, and the USB1.1 module is deactivated in the VC707 demo.

**About DE4 & TR4 demos**

Currently, DE4 and TR4 demos don't support PCIE. So in DE4 and TR4 demos, the ```PCIE``` variable always point to without PCIE.

**About the 32-bit Boom**

The 32bit Boom doesn't support FPU, so the ```ISACONF=RV32GC``` with ```HYBRID=Boom``` is an invalid configuration.
Furthermore, 32bit Boom currently got bug and cannot perform in FPGA, so please don't use 32bit Boom *(32/64bit Rocket and 64bit Boom are okay!)*

### I. c) Build FPGA (make .bit or .sof)

**For demo on VC707:**

- Open the Vivado tool, select the '*Open Project*'
- Point to '*tee-hardware/fpga/Xilinx/VC707/VC707.xpr*', then click '*OK*'
- From the top-menu or in the Flow Navigation on the left, click the '*Generate Bitstream*' (at 1st time run, it will pop-up dialog and ask about synthesys & implementation -> just tick '*Don't show this dialog again*' and hit Yes)
- It will build sysnthesys, then implementation, then generate bitstream sequentially. When it's done, another dialog will appear and ask about '*Generate Memory Configuration*'. If you don't want to generate the files for flash programming, just skip this then you're done.

But if you do want to program the flash, then choose the '*Generate Memory Configuration File*' then click '*OK*'. A new dialog will appear:
- Format: select '*MCS*'
- On the '*Memory Part*': browse to the one with the allias name of '*28f00ag18f*' (scroll down from the top, it is the first item on the list that has an alias name)
- On the '*Filename*': browse to '*tee-hardware/fpga/Xilinx/VC707/VC707.runs/impl_1/*' folder and name the file '*FPGAVC707.mcs*'
- Tick the '*Load bitstream files*': start address keep at 0x0, direction is '*up*', and the '*Bitfile*' browse to the '*VC707/VC707.runs/impl_1/FPGAVC707.bit*'
- Finally, click '*OK*' to finish.

Built files are under '*tee-hardware/fpga/Xilinx/VC707/VC707.runs/impl_1/*'
- .bit: bitstream file for direct programming
- .mcs and .prm: two files for flash programming

**Tip:** when build Vivado, you can set multithread by:
- Go to the '*Tcl Console*' tab (usually at the bottom) and type '*$ set_param general.maxThreads 18*' (set for 18 cores for example)
- Open the '*Settings*' (from Flow Navigator or in the Tools -> Settings) -> in the '*Project Settings*' on the left choose the '*Implementation*' -> in the '*Settings*' on the right scroll down to the '*Route Design (route_design)*' -> at the '*More Options*' type this in : *-ultrathreads*

**Tip:** sometimes Vivado build gets stuck at **\[Phase 4.0 Global Route Iteration 0\]** *(and eventually it will fail)* due to congestion error. Then you can set these settings *(Vivado will take longer time but the build will success)*:
- Open the '*Settings*' (from Flow Navigator or in the Tools -> Settings) -> in the '*Project Settings*' on the left choose the '*Synthesis*' -> in the '*Settings*' on the right, at the '*Strategy*' option, choose '*Flow_AlternateRoutability*'
- Then on the '*Project Settings*' on the left, now choose '*Implementation*' -> in the '*Settings*' on the right, at the '*Strategy*' option, choose '*Congestion_SpreadLogic_high*'
- '*Apply*' then '*OK*'. Now you can re-build the Vivado again.

**For demo on DE4 & TR4:**

- Open the Quartus tool, select '*File*' then '*Open Project*'
- Point to '*tee-hardware/fpga/Altera/DE4/DE4.qpf*' if DE4; '*tee-hardware/fpga/Altera/TR4/TR4.qpf*' if TR4. Then click '*Open*'
- Click the '*Tools*' then '*Platform Designer*', choose the '*main.qsys*' then '*Open*'
- Click the '*Generate HDL*' button then '*Generate*', and wait for its done
- When it's done, hit '*Close*' then '*Finish*' to close the Platform Designer's window
- On the Quartus's window, click the '*Compilation*' button or *Ctrl+L*, and wait for it to finish.

Built files are under '*tee-hardware/fpga/Altera/DE4/output_files/*' if DE4; '*tee-hardware/fpga/Altera/TR4/output_files/*' if TR4
- .sof: bitstream file for direct programming

**About the program & debug**

Guide for program & debug on VC707, DE4, and TR4 can be found here: [VC707 program and debug guide](/project/2020/07/24/vc707-program-debug).

* * *

# II. Hardware: Use with Idea IntelliJ

Guide to install Idea IntelliJ is in [Initial Setup: II.e)](./init.md#ii-e-idea-intellij).

## II. a) To import project

To import the tee-hardware folder to the **Idea IntelliJ** tool:

 - If the tee-hardware folder wasn't compiled before, go ahead and 'make' for the first time. This act is just for download the dependencies, because the Idea IntelliJ has trouble with dependencies download.
 - **Big note:** when 'make', please notice that there will be one line looks like this, you should copy it for later use *(it usually appears right before the creation of the device tree)*:

```
cd /home/ubuntu/Projects/TEE-HW/tee-hardware && java -Xmx8G -Xss8M -XX:MaxPermSize=256M -jar /home/ubuntu/Projects/TEE-HW/tee-hardware/hardware/chipyard/generators/rocket-chip/sbt-launch.jar ++2.12.4 "project teehardware" "runMain uec.teehardware.exampletop.Generator /home/ubuntu/Projects/TEE-HW/tee-hardware/fpga/Altera/DE4/src uec.teehardware FPGADE4 uec.teehardware DE4ConfigRV64GC"
(the content may be differ on your machine)
```

 - Open the Idea IntelliJ tool, and choose '*Import Project*'
 - Then choose '*sbt*' then hit '*Next*'
 - Tick the '*for imports*' and '*for builds*' options in the ***Use sbt shell*** then hit '*Finish*'
 - Wait for it to sync for the first time.

## II. b) To debug project

To debug with the **Idea IntelliJ** tool:

 - Click the ***Add Configuration...*** button right next to the build button (at the top-bar to the right). Then hit the ***+*** button to add a new configuration, and choose the ***JAR Application*** setting
 - Now get back to the " *java -jar* " example note earlier:
```
cd /home/ubuntu/Projects/TEE-HW/tee-hardware && java -Xmx8G -Xss8M -XX:MaxPermSize=256M -jar /home/ubuntu/Projects/TEE-HW/tee-hardware/hardware/chipyard/generators/rocket-chip/sbt-launch.jar ++2.12.4 "project teehardware" "runMain uec.teehardware.exampletop.Generator /home/ubuntu/Projects/TEE-HW/tee-hardware/fpga/Altera/DE4/src uec.teehardware FPGADE4 uec.teehardware DE4ConfigRV64GC"
```
   The ***/home/ubuntu/Projects/TEE-HW/tee-hardware/hardware/chipyard/generators/rocket-chip/sbt-launch.jar*** part will go to the ***Path to JAR:***
   
   The ***++2.12.4 "project teehardware" "runMain uec.teehardware.exampletop.Generator /home/ubuntu/Projects/TEE-HW/tee-hardware/fpga/Altera/DE4/src uec.teehardware FPGADE4 uec.teehardware DE4ConfigRV64GC"*** part will go to the ***Program arguments:***
   
   Everything else just leave as they are, then click '*Apply*' and '*OK*'. Now you can debug with freedom folder.

* * *

# III. Software (with Keystone)

Ref [link](https://github.com/keystone-enclave/keystone) for the KeyStone project.

## III. a) Prepare the SD card

Use the **gptfdisk** tool to create 4 partitions in the SD card.

If you don't have the **gptfdisk tool**, then do the followings to install it:
```
$ git clone https://github.com/tmagik/gptfdisk.git	#branch master commit 3d6a1587 on 9-Dec-2018
$ cd gptfdisk/
$ make -j`nproc`
```

To use gptfdisk:
```
$ cd gptfdisk/	#go to gptfdisk folder
$ sudo ./gdisk /dev/sd?	#point to the sd-card

Some commands:
$ p	# print partitions information
$ d	# delete partition
$ n	# create new partition
$ w	# write partition
```

The sd-card after created:
```
Number	Start (sector)	End (sector)	Size			Code	Name
1		2048		67583		32.0 MiB		5202	SiFive bare-metal (...
2		264192		15759326	7.4 GiB		8300	Linux filesystem
4		67584		67839		128.0 KiB	5201	SiFive FSBL (first-...
```

## III. b) Prepare BBL & FSBL

#### For the bbl.bin:

Follow the instruction of [Keystone RV64](./keystone-makefile-64.md) or [Keystone RV32](./keystone-makefile-32.md) to make the **bbl.bin** of the Keystone & Keystone-demo.

The **bbl.bin** is for the 1st partition of the SD card:
```
$ cd <keystone folder>				#cd to your keystone folder
$ sudo dd if=hifive-work/bbl.bin of=/dev/sdX1 bs=4096 conv=fsync
where the X1 is the 1st partition of the USB device
```

#### For the fsbl.bin:

After the hardware make (section [I. a)](#i-a-make-verilog-sources) above), there is a **fsbl.bin** file inside the folder **software/freedom-u540-c000-bootloader/**. That file is for the 4th partition of the SD card:
```
$ cd <your tee-hardware folder>
$ cd software/freedom-u540-c000-bootloader/
$ sudo dd if=vc707fsbl.bin of=/dev/sdX4 bs=4096 conv=fsync
where the X4 is the 4th partition of the USB device
```

## III. c) If using QSPI (Flash)

If you're using the QSPI option in the DE4 & TR4 demos (VC707 demo doesn't support QSPI), then you have to copy the ZSBL to the Flash outside. Below is the instruction of how to program the Flash via QSPI.

We are going to program the Flash via JTAG by using the RISC-V CPU itself:
- Turn on & program the board, connect the JTAG & UART as usual, also remember to connect the Flash to the board.
- On a terminal, run the OpenOCD: *(guide on installing the OpenOCD is at [Initial Setup / II. g) OpenOCD](./init.md#ii-g-openocd))*
```
$ cd <your riscv-openocd folder>
$ openocd -f riscv-openocd-flash.cfg
```
- If the debugger connection is success, then open a new terminal for GDB:
```
$ cd <your tee-hardware folder>
$ cd software/freedom-u540-c000-bootloader	# go to bootloader folder
$ export PATH=/opt/riscv64gc/bin/:$PATH		# export toolchain if it's not there yet (choose the toolchain that you want)
$ riscv64-unknown-elf-gdb FPGAzsbl.elf		# program the FPGAzsbl.elf to the flash
$ target extended-remote localhost:3333
$ load	#after a while it will be done
```
- Now the flash is programmed, you can:
```
$ monitor reset halt				# this will reset the CPUs
$ c						# this will continue the CPUs
```
or just quit the GDB/OpenOCD then hit reset on the board.

## III. d) Boot on & run the test

Finally, put in the SD card to the board, program the board, then wait for the board to boot on. Communicate with the board via UART:
```
$ sudo minicom -b 115200 -D /dev/ttyUSBx
where x is the number of connected USB-UART
Login by the id of 'root' and the password of 'sifive'.
```

To run the keystone test:
```
$ insmod keystone-driver.ko		#install driver
$ time ./tests/tests.ke 			#okay if the 'Attestation report SIGNATURE is valid' is printed
$ cd keystone-demo/			#go to the keystone-demo test
$ ./enclave-host.riscv &			#run host in localhost
$ ./trusted_client.riscv localhost	#connect to localhost and test
okay if the 'Attestation signature and enclave hash are valid' is printed
```
