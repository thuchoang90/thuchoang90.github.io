---
layout: post
title: "Advanced VLSI Design"
categories: Teaching
tags: RISC-V Courses VLSI
---

### Core Knowledge

Understand the **V**ery **L**arge-**S**cale **I**ntegration circuit *(VLSI)* digital design flow.
<br>
Know how to design a Standard Cell (*StdCell*) *library*.
<br>
Know how to integrate various digital or analog designs into a FullChip frame.
<br>
Working with industrial-grade or open-source EDA tools.

### Course Requirement

Participants <ins>must</ins> have **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.

### Course List

| Lecture | Title |
|:---:|---|
| 1 | VLSI Introduction |
| 2 | MOSFET, CMOS, and Logic |
| 3 | Delay and Power Models |
| 4 | SPICE and Schematic |
| 5 | Interconnect and Layout |
| 6 | Standard Cell Library |
| 7 | Characterization |
| 8 | Synthesis |
| 9 | Timing Analysis |
| 10 | Place and Route |
| 11 | Verification |
| 12 | Macro Integration |
| 13 | IOs and FullChip |
| 14 | Advanced Topics |
| 15 | Course Summary |

**Lecture #1:&nbsp;&nbsp;&nbsp;&nbsp;VLSI Introduction**<br>
Introduce the overall VLSI flow and show some VLSI applications. Explain the necessary files when designing circuits. Finally, EDA tools for VLSI design will be introduced.

**Lecture #2:&nbsp;&nbsp;&nbsp;&nbsp;MOSFET, CMOS, and Logic**<br>
Briefly review MOSFET characteristics and Boolean functions. Show what needs to be done at the transistor-level optimization. Review the basics of logic design using CMOS. Showing how to make an optimization schematic given a Boolean function.

**Lecture #3:&nbsp;&nbsp;&nbsp;&nbsp;Delay and Power Models**<br>
Explain the non-restoring element in schematic design. Explain the RC delay model used in the multi-stage schematic optimization. Several examples of the RC delay model are given. Explain the power model used in VLSI circuits, including static power and dynamic power examples.

**Lecture #4:&nbsp;&nbsp;&nbsp;&nbsp;SPICE and Schematic**<br>
Explain the SPICE language. Explain how to use SPICE for transistor-level circuit simulation with examples. Finally, show how to use tools for schematic design with simulation.

**Lecture #5:&nbsp;&nbsp;&nbsp;&nbsp;Interconnect and Layout**<br>
Introduce the stick diagram method via examples. Provide a guide on using tools to draw a layout of an inverter circuit. Finally, show how to use a tool for design rules check and then run a post-layout simulation with a script.

**Lecture #6:&nbsp;&nbsp;&nbsp;&nbsp;Standard Cell Library**<br>
Introduce the cell-based method and explain the differences between standard and custom cells. Explain the "rules" in standard cell design. Give an example of a standard cell library, then explain each component.

**Lecture #7:&nbsp;&nbsp;&nbsp;&nbsp;Characterization**<br>
Explain how to create various library files from the original layout. Guide on creating library files using a characterization tool and an abstraction tool.

**Lecture #8:&nbsp;&nbsp;&nbsp;&nbsp;Synthesis**<br>
Guide on using the tool for synthesis. Guide on checking the synthesis results and doing the post-synthesis netlist simulation.

**Lecture #9:&nbsp;&nbsp;&nbsp;&nbsp;Timing Analysis**<br>
Explain the latch and flip-flop designs. Explain the timing requirements in circuit design. Show how to write an SDC constraint. Finally, show how to check timing for the given synthesized netlist.

**Lecture #10:&nbsp;&nbsp;&nbsp;&nbsp;Place and Route**<br>
Guide on using tools for Place-and-Route (PnR). Guide on checking the PnR results and doing the post-layout netlist simulation.

**Lecture #11:&nbsp;&nbsp;&nbsp;&nbsp;Verification**<br>
Explain the formal verification and physical verification. Explain the reason for antenna and metal density checking. Explain the completed full digital design flow. Finally, a guide on using the full-flow digital design template.

**Lecture #12:&nbsp;&nbsp;&nbsp;&nbsp;Macro Integration**<br>
Explain the differences between analog/custom and digital design flows. Show how to manually perform the design rules checks, verifications, and post-layout simulation. Provide a guide on creating other necessary files for FullChip integration.

**Lecture #13:&nbsp;&nbsp;&nbsp;&nbsp;IOs and FullChip**<br>
Explain the latchup and ESD phenomenon. Introduce the IO designs, frame, and package. Introduce the FullChip integration task and explain the steps. Guide on using the FullChip integration template.

**Lecture #14:&nbsp;&nbsp;&nbsp;&nbsp;Advanced Topics**<br>
Give an explanation of several advanced topics such as synchronizer, FinFet vs. SOI, design for test, and clock gating.

**Lecture #15:&nbsp;&nbsp;&nbsp;&nbsp;Course Summary**<br>
Review all lectures related to the Advanced VLSI Design course.
