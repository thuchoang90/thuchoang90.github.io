---
layout: post
title: "RISC-V Computer System Integration"
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
Participants <ins>don't need</ins> to know the **Scala-CHISEL** language to learn this course.

Exercises in this course use the <a href="https://digilent.com/reference/programmable-logic/arty-a7/start">Arty-A7</a> FPGA board. Participants need to have an Arty-A7 to learn this course.
<br>
*Note:* both 35T and 100T versions of the FPGA are ok.

### Course List

| Lecture | Title |
|:---:|---|
| 1 | RISC-V Introduction |
| 2 | Creating Project with Chipyard |
| 3 | Computer System on Arty-A7 |
| 4 | Boot Sequence and Software |
| 5 | Custom Hardware on Peripheral |
| 6 | Custom Hardware in ROCC |
| 7 | Course Summary |

**Lecture #1:**&nbsp;&nbsp;&nbsp;&nbsp;RISC-V Introduction
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the structure of a typical computer system. Introduce RISC-V and RISC-V ISA. Giving materials and some RISC-V news.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;To learn what is a computer system in general. To learn the idea of RISC-V and ISA. To know what RISC-V is capable of and what we can do with RISC-V.

**Lecture #2:**&nbsp;&nbsp;&nbsp;&nbsp;Creating Project with Chipyard
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce Chipyard library and explain its structure. Show how to git clone and make. Learn how to create a new Chisel project using this Chipyard library as a template.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know how to use the Chipyard library. Know how to create a new Chisel project using Chipyard template.

**Lecture #3:**&nbsp;&nbsp;&nbsp;&nbsp;Computer System on Arty-A7
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the RISC-V computer system. Learn how to Git clone and make the system. Learn how to program with the Arty-A7 FPGA board. Learn how to change some of the system configurations.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Get familiar with a complex RISC-V folder structure using Chipyard. Get used to the Arty-A7 FPGA board. Learn about system details and how to change some of the configurations.

**Lecture #4:**&nbsp;&nbsp;&nbsp;&nbsp;Boot Sequence and Software
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Describe the typical boot flow of computer systems. Describe our system's boot sequence with the default software. Learn how to change the default program with your custom codes.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Learn the typical boot flow of computer systems. Understand the boot flow of our computer system. Learn how to make a custom program for our computer system.

**Lecture #5:**&nbsp;&nbsp;&nbsp;&nbsp;Custom Hardware on Peripheral
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the TileLink bus protocol and the peripheral's memory-mapped communication. Explain the GCD circuit and how to write a Scala wrapper for that circuit. Finally, learn how to write software to control the new hardware.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know about the TitleLink protocol. Understand the memory-mapped communication in a computer system. Learn how to write a Scala wrapper for custom hardware. Learn how to control the custom hardware in software.

**Lecture #6:**&nbsp;&nbsp;&nbsp;&nbsp;Custom Hardware in ROCC
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the ROCC. Reuse the GCD circuit, but this time attach it to the ROCC instead of the peripheral. Finally, learn how to control the ROCC module with software.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand that there are options for putting in custom hardware: peripheral or ROCC, each with a different purpose. Know how to do ROCC and control it with software.

**Lecture #7:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;A top-down review from ISA to software and hardware.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review all lectures related to RISC-V computer system.
