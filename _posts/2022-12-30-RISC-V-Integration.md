---
layout: post
title: "01: RISC-V Computer System Integration"
categories: Teaching
tags: RISC-V-Courses
---

### Core Knowledge

Learn how to add your **custom hardware** *(written in Verilog or VHDL)* to an existing RISC-V computer system.
<br>
Learn how to control and debug your custom hardware in <ins>software</ins> after regenerating the system.

### Course Requirement

Participants <ins>must</ins> have **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.
<br>
Participants <ins>don't</ins> need to know the **Scala-CHISEL** language to learn this course.

Exercises in this course use the Arty-A7 FPGA board. Participants need to have an Arty-A7 to learn this course.
<br>
*Note:* both 35T and 100T versions of the FPGA are ok.

### Course List

| Week | Title |
|:---:|---|
| 1 | RISC-V Introduction |
| 2 | VexRiscv: a Simple 32-bit MCU |
| 3 | Rocket Computer System: Introduction and System Modification |
| 4 | Rocket Computer System: Boot Sequence and Software |
| 5 | Rocket Computer System: Making a Custom Hardware |
| 6 | Rocket Computer System: Custom Hardware with External IOs |
| 7 | Course Summary |

**Week #1:**&nbsp;&nbsp;&nbsp;&nbsp;RISC-V Introduction
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce ISA, RISC-V, and what you can do after the course.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;For participants to learn the idea of RISC-V, ISA, and what is a computer system in general.

**Week #2:**&nbsp;&nbsp;&nbsp;&nbsp;VexRiscv: a Simple 32-bit MCU
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Study about VexRiscv, how to make hardware, compile software, and debug *(on Verilator)*.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get familiar with "$ make" in a Unix system when working with RISC-V.

**Week #3:**&nbsp;&nbsp;&nbsp;&nbsp;Rocket Computer System: Introduction and System Modification
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the Chipyard library, Rocket core, hardware architecture, and the Makefile system. Learn how to Git clone, make, and program the system with the Arty-A7 FPGA. Finally, learn how to change some of the configurations in the system and the core processor.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get familiar with a complex RISC-V folder structure using the Chipyard setup. Get used to the Arty-A7 FPGA board. Learn about system details and how to change some of the configurations.

**Week #4:**&nbsp;&nbsp;&nbsp;&nbsp;Rocket Computer System: Boot Sequence and Software
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Describe the system's boot sequence with the default software. Then, learn to change the default program with your custom codes.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Learn how a computer system boots from a boot ROM to a hard drive *(such as an SD card)* and, finally, to RAM. Learn about making a custom program for that computer system.

**Week #5:**&nbsp;&nbsp;&nbsp;&nbsp;Rocket Computer System: Making a Custom Hardware
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the TileLink bus protocol and the peripheral's memory-mapped communication. Make a custom Verilog hardware *(GCD circuit)* and test it by simulation. Then, learn how to write a Scala wrapper and attach that Verilog hardware as a black box. Finally, generate the system with the new peripheral and write software to control it.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know about the TitleLink protocol. Understand the memory-mapped communication in a computer system. Learn how to write a Scala wrapper for your custom hardware. Finally, learn how to control your custom hardware in software via the memory-mapped structure.

**Week #6:**&nbsp;&nbsp;&nbsp;&nbsp;Rocket Computer System: Custom Hardware with External IOs
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;A mini-review for the previous week. Repeat the previous work with custom hardware with external IOs/pins.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Mostly re-do the work of the previous week. This time, learn to use external IOs/pins with your custom hardware.

**Week #7:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Review from soft to hard (top-down): software and boot flow, device tree, toolchain and ISA, hardware and system architecture, Makefile system, and system (Scala) modification. Then, review how to add custom hardware to the system and control it in software after boot.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reviewing all the knowledge and concluding what students have learned.
