---
layout: post
title: "Advanced VLSI Design"
categories: Teaching
tags: RISC-V-Courses
---

### Core Knowledge

Understand the **V**ery **L**arge-**S**cale **I**ntegration circuit *(VLSI)* design flow with complex digital systems.
<br>
Practice with System-on-Chip *(SoC)*: flat layout for a simple system and hierarchy layout for a complex system.

### Course Requirement

Participants <ins>must</ins> have **digital design** knowledge and know how to use **Verilog** *(or VHDL)* language.

**About the PDK:**
<br>
UEC students will study with the <ins>ROHM-180nm</ins> process (licensed via <a href="http://www.vdec.u-tokyo.ac.jp/">VDEC</a>).
<br>
Oversea participants will study with the <ins><a href="https://github.com/google/skywater-pdk">skywater-130nm</a></ins> process (open license).

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
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Introduce the VLSI flow and the template's folder structure.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the VLSI flow and basic steps in making a chip. Get introduced to the template (make-script) folder structure.

**Lecture #2:**&nbsp;&nbsp;&nbsp;&nbsp;Review MOSFET and Schematic
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Review basic knowledge of logic gates, transistor schematics, MOSFET architecture, modeling, digital standard cells, and design rules.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Make sure that everybody shares the same common knowledge, including MOSFET architecture, how logic gates are translated to transistors, the importance of modeling, and why standard cells are needed in digital design.

**Lecture #3:**&nbsp;&nbsp;&nbsp;&nbsp;Layout with Virtuoso
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;N/A
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N/A

**Lecture #4:**&nbsp;&nbsp;&nbsp;&nbsp;Standard Cell Library
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;N/A
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N/A

**Lecture #5:**&nbsp;&nbsp;&nbsp;&nbsp;Back-end Synthesis
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;N/A
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N/A

**Lecture #6:**&nbsp;&nbsp;&nbsp;&nbsp;Back-end Place-and-Route
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;N/A
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N/A

**Lecture #7:**&nbsp;&nbsp;&nbsp;&nbsp;Full Digital Design Flow
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Run the flat layout template with the CPU-and-RAM design. Then, practice with the VexRiscv SoC.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understand the difficulties in making a huge digital circuit.

**Lecture #8:**&nbsp;&nbsp;&nbsp;&nbsp;Analog Design Flow
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;N/a
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;N/A

**Lecture #9:**&nbsp;&nbsp;&nbsp;&nbsp;IO-cell and FullChip Integration
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Explain the packaging and socket, and then introduce the Fullchip script. Finally, make a frame integration with VexRiscv and Rocket cores. Repeat the fullchip integration process with multiple power supplies instead of one.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Understanding the packaging and fullchip integration process. Practice it with the two layouts of VexRiscv and Rocket in lectures 3 and 4. Understand that the packaging with multiple cores needs multiple separate power supplies.

**Lecture #10:**&nbsp;&nbsp;&nbsp;&nbsp;Course Summary
- *Description:*&nbsp;&nbsp;&nbsp;&nbsp;Review everything from the beginning to the end: VLSI flow, logic gates and transistors, standard cells, backend design flow, how to do a hierarchy layout, and finally, how to put everything into a frame.
- *Purpose:*&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reviewing all the knowledge and concluding what students have learned.
