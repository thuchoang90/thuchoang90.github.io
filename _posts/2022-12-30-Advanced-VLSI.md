---
layout: post
title: "Advanced VLSI Design"
categories: Teaching
tags: RISC-V Courses VLSI
---

### Core Knowledge

Understand the **V**ery **L**arge-**S**cale **I**ntegration circuit *(VLSI)* design flow.
<br>
Know how to design a Standard Cell (*StdCell*), then complete a StdCell *library* for full digital design flow.
<br>
Know how to integrate various designs, digital or analog alike, into a FullChip frame.

### Course Requirement

Participants <ins>must</ins> have **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.

**About the PDK:**
<br>
UEC students will study with the <ins>ROHM-180nm</ins> process (licensed via <a href="http://www.vdec.u-tokyo.ac.jp/">VDEC</a>).
<br>
Oversea participants will study with the <ins><a href="https://github.com/google/skywater-pdk">skywater-130nm</a></ins> or <ins><a href="https://eda.ncsu.edu/freepdk/freepdk45/">openPDK45</a></ins> processes (open licenses).

**About the design tools:**
<br>
UEC students will practice with a <ins>mixed script</ins> of Cadence, Synopsys, and Mentor Graphic (licensed via <a href="http://www.vdec.u-tokyo.ac.jp/">VDEC</a>).
<br>
For oversea participants, the oversea partner **must** provide the tool's license. Depending on which license the oversea partner has *(Cadence or Synopsys, Mentor Graphic or not)*, we will provide the appropriate script.

### Course List

| Lecture | Title |
|:---:|---|
| 1 | VLSI Introduction |
| 2 | MOSFET and Schematic |
| 3 | Layout with Virtuoso |
| 4 | Standard Cell Library |
| 5 | Characterization and Abstraction |
| 6 | Synthesis |
| 7 | Place and Route |
| 8 | Full Digital Design Flow |
| 9 | Macro Integration |
| 10 | IOs and FullChip Integration |
| 11 | Course Summary |

**Lecture #1:**&nbsp;&nbsp;&nbsp;&nbsp;VLSI Introduction
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the overall VLSI flow and show some VLSI applications. Explain the necessary files when designing circuits. Finally, EDA tools for VLSI design will be introduced.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the overall VLSI flow. Distinguish the differences between designing and manufacturing flows. Understand the steps in digital design. Understand what files we need before designing a circuit.

**Lecture #2:**&nbsp;&nbsp;&nbsp;&nbsp;MOSFET and Schematic
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Briefly review MOSFET characteristics and Boolean functions. Show what needs to be done at the transistor-level optimization. Finally, show how to use tools for schematic design with simulation.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review the basic knowledge about MOSFET and Boolean algebra. Understand how transistor-level optimization is different from logic-gate-level optimization. Know how to use tools for schematic design.

**Lecture #3:**&nbsp;&nbsp;&nbsp;&nbsp;Layout with Virtuoso
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the stick diagram method via examples. Provide a guide on using tools to draw a layout of an inverter circuit. Finally, show how to use a tool for design rules check and then run a post-layout simulation with a script.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Study the usage of stick diagrams in sketching layouts. Know how to use tools for drawing layout. Know how to check design rules and run post-layout simulations.

**Lecture #4:**&nbsp;&nbsp;&nbsp;&nbsp;Standard Cell Library
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the cell-based method and explain the differences between standard and custom cells. Explain the “rules” in standard cell design. Give an example of a standard cell library, then explain each component.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the cell-based method, the “rules” when designing a standard cell, the various components in a standard cell library, and which cell type is for which purpose.

**Lecture #5:**&nbsp;&nbsp;&nbsp;&nbsp;Characterization and Abstraction
- *Description:*
- *Purpose:*

**Lecture #6:**&nbsp;&nbsp;&nbsp;&nbsp;Synthesis
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Guide on how to create various library files from the layouts. Guide on using tool for synthesis. Guide on checking the synthesis results.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know how to create necessary files for a Standard Cell (StdCell) library from the existing layouts. Know how to use tools for synthesis.

**Lecture #7:**&nbsp;&nbsp;&nbsp;&nbsp;Place and Route
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Guide on creating the necessary LEF files. Guide on using tools for Place-and-Route (PnR). Guide on checking the PnR results.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know how to create abstractions (LEF files) for layouts. Know how to use tools for Place-and-Route.

**Lecture #8:**&nbsp;&nbsp;&nbsp;&nbsp;Full Digital Design Flow
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the completed full digital design flow. Guide on using the full-flow digital design template.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the full flow of digital design. Know how to use the full-flow digital design template.

**Lecture #9:**&nbsp;&nbsp;&nbsp;&nbsp;Macro Integration
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the differences between analog/custom and digital design flows. Show how to manually perform the design rules checks, verifications, and post-layout simulation. Provide a guide on creating other necessary files for FullChip integration.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the differences between analog/custom and digital design flows. Know how to manually check the design rules and other verifications on the layout. Finally, know how to create other necessary files for the FullChip integration.

**Lecture #10:**&nbsp;&nbsp;&nbsp;&nbsp;IOs and FullChip Integration
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the FullChip integration task and explain the steps. Guide on using the FullChip integration template.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the task of FullChip integration and its steps. Know how to use the FullChip integration template.

**Lecture #11:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;The CMOS characteristics are briefly reviewed, followed by a guide to the schematic and layout with Virtuoso. Then, review all the steps of making a standard cell library and follow up with the detailed digital design flow and FullChip integration flow.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review all lectures related to Advanced VLSI Design course.
