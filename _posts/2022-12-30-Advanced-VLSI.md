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
| 2 | Review MOSFET and Schematic |
| 3 | Layout with Virtuoso |
| 4 | Standard Cell Library |
| 5 | Back-end Synthesis |
| 6 | Back-end Place-and-Route |
| 7 | Full Digital Design Flow |
| 8 | Analog Design Flow |
| 9 | IO-cell and FullChip Integration |
| 10 | Course Summary |

**Lecture #1:**&nbsp;&nbsp;&nbsp;&nbsp;VLSI Introduction
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the overall VLSI flow and show some VLSI applications. Explain digital design flow with an example. Explain necessary files when we design circuits. Finally, introduce EDA tools for VLSI design.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the overall VLSI flow. Distinguish between designing flow and manufacturing flow. Understand steps in digital design flow. Understand what files we need before designing circuits.

**Lecture #2:**&nbsp;&nbsp;&nbsp;&nbsp;Review MOSFET and Schematic
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Briefly review MOSFET characteristics and Boolean functions. Show what needs to be done at the transistor-level optimization. Finally, show how to use tool for schematic design with simulation.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review the basic knowledge about MOSFET and Boolean algebra. Understand how transistor-level optimization is different with logic-gate-level optimization. Know how to use tool for schematic design.

**Lecture #3:**&nbsp;&nbsp;&nbsp;&nbsp;Layout with Virtuoso
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce stick diagram via examples, and then show how to planning with it. Guide on using tool for drawing layout of an inverter circuit. Finally, show how to use tool for design rules check, and then run post-layout simulation with script.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Study about the usage of stick diagram in sketching layouts. Know how to use tool for drawing layout. Know how to check design rules and run post-layout simulation.

**Lecture #4:**&nbsp;&nbsp;&nbsp;&nbsp;Standard Cell Library
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the cell-based method and explain the differences between standard and
custom cells. Explain the “rules” in standard cell design. Give an example of a standard cell library, then explain each component.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the cell-based method. Understand the “rules” when designing a standard cell. Distinguish different components in a standard cell library, and understand which cell-type is for which purpose.

**Lecture #5:**&nbsp;&nbsp;&nbsp;&nbsp;Back-end Synthesis
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Guide on how to create various library files from the layouts. Guide on using tool for synthesis. Guide on checking the synthesis results.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know how to create necessary files for a Standard Cell (StdCell) library from the existing layouts. Know how to use tool for synthesis.

**Lecture #6:**&nbsp;&nbsp;&nbsp;&nbsp;Back-end Place-and-Route
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Guide on creating the necessary LEF files. Guide on using tool for Place-and-Route (PnR). Guide on checking the PnR results.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Know how to create abstractions (LEF files) for layouts. Know how to use tool for Place-and-Route.

**Lecture #7:**&nbsp;&nbsp;&nbsp;&nbsp;Full Digital Design Flow
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the completed full digital design flow. Guide on using the full flow digital design template.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the full flow of digital design. Know how to use the full flow digital design template.

**Lecture #8:**&nbsp;&nbsp;&nbsp;&nbsp;Analog Design Flow
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the differences between analog and digital design flows. Show how to do the design rules checks, verifications, and post-layout simulation manually. Guide on creating other necessary files for FullChip integration.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the differences between analog and digital design flows. Know how to do the design rules check and other verifications manually on the layout. Finally, know how to create other necessary files for the FullChip integration.

**Lecture #9:**&nbsp;&nbsp;&nbsp;&nbsp;IO-cell and FullChip Integration
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the FullChip integration task and explain the steps. Guide on using the FullChip integration template.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the task of FullChip integration and its steps. Know how to use the FullChip integration template.

**Lecture #10:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;The CMOS characteristics are briefly reviewed and followed up with a guide to the schematic and layout with Virtuoso. Then, review all the steps of making a standard cell library and follow up with the detailed digital design flow and FullChip integration flow
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Review all lectures related to VLSI design flow.
