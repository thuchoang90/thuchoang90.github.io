---
layout: post
title: "SiFive Freedom: chisel code structure"
categories: Project
tags: RISC-V
---

## I. Introduction

Reference link for SiFive Freedom: [sifive/freedom](https://github.com/sifive/freedom)

### I. a) Important files

They have two main series of CPU called **E300** (rv32gc) and **U500** (rv64gc).
The way they structured them are similar.
They used three kind of scala files, i.e., *Shell* file, *Configs* file, and *Design* file, to create a system.

<table>
  <tr>
    <th>File</th>
    <th>Description</th>
    <th>Example file</th>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Configs file</span></td>
    <td>Is used as a configuration file for the CPU, and it's usually fixed for multiple designs.</td>
    <td>src/main/scala/unleashed/ DevKitConfigs.scala</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Design file</span></td>
    <td>Is an extension upon the <i>Configs</i> file. In the <i>Design</i> file, all of the modules are called and connected. The <i>Design</i> file is also usually fixed for multiple platforms.</td>
    <td>src/main/scala/unleashed/ DevKitFPGADesign.scala</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">Shell file</span></td>
    <td>Is like a top file where all of the IOs are declared. They usually have one <i>Shell</i> file for each platform.</td>
    <td>fpga-shells/src/main/scala/ shell/xilinx/VC707NewShell.scala</td>
  </tr>
</table>

### I. b) Build procedure

**1: from Makefile -> to sbt**

When ```$ make verilog``` in the **freedom** top folder, the job of the Makefiles is just to pass the arguments into the **sbt** tool.

**2: sbt: from .scala -> to .fir**

The **sbt** tool is a tool to compile the scala codes into java executable files. Then, subsequently, create the **.fir** files from those java executives.

The actual command to create **.fir** file from scala codes:
```makefile
java -jar $(rocketchip_dir)/sbt-launch.jar ++2.12.4 "runMain freechips.rocketchip.system.Generator $(BUILD_DIR) $(PROJECT) $(MODEL) $(CONFIG_PROJECT) $(CONFIG)"
```
where:
 - ```$(BUILD_DIR)``` is the folder that you want to generate your *.fir* file into
 - ```$(PROJECT)``` is the package that contains the ```$(MODEL)```
 - ```$(MODEL)``` is the name of the top *Shell* in scala codes
 - ```$(CONFIG_PROJECT)``` is the package that contains the ```$(CONFIG)```
 - ```$(CONFIG)``` is the name of the top *Design* in scala codes

**3: from .fir -> to .v**

After we have the **.fir** file, this is the command to create the verilog codes from the **.fir** file: (the verilog codes are generated into just one **.v** file)
```makefile
java -Xmx2G -Xss8M -XX:MaxPermSize=256M -cp $(FIRRTL_JAR) firrtl.Driver -i <path to .fir file> -o <path to .v file> -X verilog
```
where ```$(FIRRTL_JAR)``` is the path that point to ```$(rocketchip_dir)/firrtl/utils/bin/firrtl.jar```

* * *

## II. Shell File

This file is like a top file with the main purpose of IOs declaration.

This file doesn't call the *Design* file or *Config* file. When ```$ make``` by the sbt, this file and the *Design* file are called together by a single sbt command-line. The *Shell* file and the *Design* file 'talk' with each other by *Overlays*.

SiFive Freedom codes are relied on extending the ***LazyModule*** which relied on ***lazy val*** declaration. Because of the ***lazy*** property, if a group of IOs isn't declared in the top *Shell*, the corresponding ***LazyModule*** won't be instantiated, thus leading to the removal of the relevant modules in the actual implementation.

For example: in the ***fpga-shells/src/main/scala/shell/xilinx/VC707NewShell.scala***
```scala
abstract class VC707Shell()(implicit p: Parameters) extends Series7Shell
{
  . . .
  val led       = Overlay(LEDOverlayKey)       (new LEDVC707Overlay     (_, _, _))
  val switch    = Overlay(SwitchOverlayKey)    (new SwitchVC707Overlay  (_, _, _))
  . . .
}
```
If we just ```//``` the ```val led``` and ```val switch```, like this:
```scala
abstract class VC707Shell()(implicit p: Parameters) extends Series7Shell
{
  . . .
  //val led       = Overlay(LEDOverlayKey)       (new LEDVC707Overlay     (_, _, _))
  //val switch    = Overlay(SwitchOverlayKey)    (new SwitchVC707Overlay  (_, _, _))
  . . .
}
```
Then the IOs of leds & switches won't be declared, thus the GPIOs module won't be instantiated in the design, and there will be no GPIOs module in the final verilog code.

* * *

## III. Configs File

This file is the configuration file for the CPUs and internal bus systems.

This file is later called by the *Design* file.

* * *

## IV. Design File 

This file carries out the actual implementation of the design, with all of the modules and how they are connected.

This file calls and extends (or even overrides) the *Configs* file.

* * *
