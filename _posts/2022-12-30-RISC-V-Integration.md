---
layout: post
title: "RISC-V Computer System Integration"
categories: Teaching
tags: RISC-V Courses FPGA
---

### Core Knowledge

Learn how to add your **custom hardware** *(written in Verilog or VHDL)* to an existing RISC-V computer system.
<br>
Learn how to control and debug your custom hardware in <ins>software</ins> after regenerating the system.

### Course Requirement

Participants <ins>must</ins> have **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.
<br>
Participants <ins>don't need</ins> to know the **Scala-CHISEL** language to learn this course.

Exercises in this course use the <a href="https://digilent.com/reference/programmable-logic/arty-a7/start">Arty-A7</a> FPGA board. Participants need to have an Arty-A7 to learn this course.
<br>
*Note:* both 35T and 100T versions of the FPGA are ok.

### Course List

| Lecture | Title |
|:---:|---|
| 1 | RISC-V Introduction |
| 2 | Chipyard Design Framework |
| 3 | Rocket Computer System |
| 4 | Boot Sequence and Software |
| 5 | Custom Hardware on Peripheral |
| 6 | Custom Hardware in ROCC |
| 7 | Course Summary |

**Lecture #1:**&nbsp;&nbsp;&nbsp;&nbsp;**RISC-V Introduction**<br>
Explain the structure of a typical computer system. Introduce RISC-V and RISC-V ISA. Giving materials and some RISC-V news.

**Lecture #2:**&nbsp;&nbsp;&nbsp;&nbsp;**Chipyard Design Framework**<br>
Introduce the Chipyard library and explain its structure. Show how to git clone and make. Learn how to create a new Chisel project using this Chipyard library as a template.

**Lecture #3:**&nbsp;&nbsp;&nbsp;&nbsp;**Rocket Computer System**<br>
Introduce the RISC-V computer system. Learn how to Git clone and make the system. Learn how to program with the Arty-A7 FPGA board. Learn how to change some of the system configurations.

**Lecture #4:**&nbsp;&nbsp;&nbsp;&nbsp;**Boot Sequence and Software**<br>
Describe the typical boot flow of computer systems. Describe our system's boot sequence using the default software. Learn how to change the default program with your custom code.

**Lecture #5:**&nbsp;&nbsp;&nbsp;&nbsp;**Custom Hardware on Peripheral**<br>
Explain the TileLink bus protocol and the peripheral's memory-mapped communication. Explain the GCD circuit and how to write a Scala wrapper for that circuit. Finally, learn how to write software to control the new hardware.

**Lecture #6:**&nbsp;&nbsp;&nbsp;&nbsp;**Custom Hardware in ROCC**<br>
Explain the ROCC. Reuse the GCD circuit, but this time attach it to the ROCC instead of the peripheral. Finally, learn how to control the ROCC module with software.

**Lecture #7:**&nbsp;&nbsp;&nbsp;&nbsp;**Course Summary**<br>
A top-down review from ISA to software and hardware.
