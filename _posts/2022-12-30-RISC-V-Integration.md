---
layout: post
title: "01: RISC-V Computer System Integration"
categories: Teaching
tags: RISC-V-Courses
---

### Core Knowledge

Learn how to add your **custom hardware** *(written in Verilog or VHDL)* to an existing RISC-V computer system.
<br>
Then, learn how to control and debug your module in <ins>software</ins> after regenerating the hardware system.

### Course Requirement

Participants must have prior **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.
<br>
Participants <ins>don't</ins> need to know **Scala-CHISEL** to learn this course.

### Course List

| Week | Title |
|:---:|---|
| 1 | RISC-V Introduction |
| 2 | VexRiscv: a Simple 32-bit MCU |
| 3 | Computer System with Rocket: Introduction and System Modifications |
| 4 | Computer System with Rocket: Boot Sequence and Software |
| 5 | Computer System with Rocket: Making a Custom Hardware |
| 6 | Computer System with Rocket: Custom Hardware with External IOs |
| 7 | Course Summary |

**Week #1:**&nbsp;&nbsp;&nbsp;&nbsp;RISC-V Introduction
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce ISA, RISC-V, and what you can learn after the course.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For participants to learn the idea of RISC-V, ISA, and what is a computer system in general.

**Week #2:**&nbsp;&nbsp;&nbsp;&nbsp;VexRiscv: a Simple 32-bit MCU
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Study about VexRiscv, how to make hardware, compile software, and debug *(on Verilator)*.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get familiar with "$ make" in a Unix system when working with RISC-V.

**Week #3:**&nbsp;&nbsp;&nbsp;&nbsp;Computer System with Rocket: Introduction and System Modifications
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the Chipyard library, Rocket core, hardware architecture, and the Makefile system. Learn how to Git clone, make, and program the system with the Arty-A7 FPGA. Finally, learn how to change some of the configurations in the system and the core processor.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get familiar with a complex RISC-V folder structure using the Chipyard setup. Get used to the Arty-A7 FPGA board. Learn about system details and how to change some of the configurations.

**Week #4:**&nbsp;&nbsp;&nbsp;&nbsp;Computer System with Rocket: Boot Sequence and Software
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Describe the system's boot sequence with the default software. Then, learn to change the default program with your custom codes.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Learn how a computer system boots from a boot ROM to a hard drive *(such as an SD card)* and, finally, to RAM. Learn about making a custom program for that computer system.

**Week #5:**&nbsp;&nbsp;&nbsp;&nbsp;Computer System with Rocket: Making a Custom Hardware
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the TileLink bus protocol and the peripheral's memory-mapped communication. Make a custom Verilog hardware *(GCD circuit)* and test it by simulation. Then, learn how to write a Scala wrapper and attach that GCD circuit as a black box. Finally, generate the system with the new peripheral and write software to control it.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know about the TitleLink protocol. Understand the memory-mapped communication in a computer system. Learn how to write a Scala wrapper for your custom hardware. Finally, learn how to control your custom hardware in software via the memory-mapped structure.

**Week #6:**&nbsp;&nbsp;&nbsp;&nbsp;Computer System with Rocket: Custom Hardware with External IOs
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;

**Week #7:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
