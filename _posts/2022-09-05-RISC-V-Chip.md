---
layout: post
title: "RISC-V Chip Collection"
categories: Project
tags: Chips VLSI RISC-V
---

<style>
  .chipimg {
    float:center;
    height:auto;
    width:100%;
    max-width:650px;
  }
  .table {
    border-collapse: collapse;
    width: 100%;
  }
  .td {
    text-align: center;
  }
</style>

## IV. Crypto Processor (CryPro) Chips

### IV.1) CryPro Single-core Rocket-chip with TLS-1.3 Compatible Crypto-cores

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Feb. 2022</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV32IMAC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>1)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES-GCM, ChaCha20, Poly1305, AEAD, Ed/EC-DSA, HMAC-SHA2, RSA-1024, SHA3-512, and TRNG</td>
  </tr>
  <tr>
    <td><b>Secure Boot</b></td>
    <td>MCU as sub-system with IBex core (RV32IMC)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Floorplan</font></b></p>

<img src="/assets/sources/ChipCollection/CryPro-22-02-floorplan.jpg" class="chipimg">

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/CryPro-22-02-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/CryPro-22-02-chip.jpg" class="chipimg">

## III. Trusted Execution Environment (TEE) Hardware Chips

### III.6) TEEHW 64-bit Dual-core Rocket-Boom with Secure Boot Sub-system, Crypto-cores, and TRNG

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>7.5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jun. 2021</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV64GC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>1) + Boom (<span>&#215;</span>1)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, Ed25519, and TRNG</td>
  </tr>
  <tr>
    <td><b>Secure Boot</b></td>
    <td>MCU as sub-system with IBex core (RV32IMC)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Floorplan</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4253-floorplan.jpg" class="chipimg">

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4253-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4253-chip.jpg" class="chipimg">

### III.5) TEEHW 32-bit Dual-core Rocket-Boom with Secure Boot Sub-system, Crypto-cores, and TRNG

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jun. 2021</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV32IMAC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>1) + Boom (<span>&#215;</span>1)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, and TRNG</td>
  </tr>
  <tr>
    <td><b>Secure Boot</b></td>
    <td>MCU as sub-system with IBex core (RV32IMC)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Floorplan</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4252-floorplan.jpg" class="chipimg">

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4252-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-06-R4252-chip.jpg" class="chipimg">

### III.4) TEEHW 64-bit Dual-core Rocket-chip with Crypto-cores and TRNG

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Feb. 2021</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV64GC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>2)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, Ed25519, and TRNG</td>
  </tr>
  <tr>
    <td><b>Secure Boot</b></td>
    <td>MCU as sub-system with IBex core (RV32IMC)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Floorplan</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-02-floorplan.jpg" class="chipimg">

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-02-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-21-02-chip.jpg" class="chipimg">

### III.3) TEEHW 64-bit Single-core Boom with Crypto-cores

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jun. 2020</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV64GC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Boom (<span>&#215;</span>1)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, and Ed25519</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-06-R4254-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-06-R4254-chip.jpg" class="chipimg">

### III.2) TEEHW 32-bit Dual-core Rocket-Boom with Crypto-cores

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jun. 2020</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV32IMAC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>1) + Boom (<span>&#215;</span>1)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, and Ed25519</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-06-R4252-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-06-R4252-chip.jpg" class="chipimg">

### III.1) TEEHW 64-bit Dual-core Rocket-chip with Crypto-cores

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jan. 2020</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV64GC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>2)</td>
  </tr>
  <tr>
    <td><b>Cryptography Accelerator</b></td>
    <td>AES, SHA3-512, and Ed25519</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-01-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/TEEHW-20-01-chip.jpg" class="chipimg">

## II. VexRiscv Chips

### II.2) VexRiscv ROHM Chip

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>2.5<span>&#215;</span>2.5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Jan. 2020</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV32IM</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>VexRiscv (<span>&#215;</span>1)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/VexRiscv-20-01-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/VexRiscv-20-01-chip.jpg" class="chipimg">

### II.1) VexRiscv SOTB Chip

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>SOTB-65nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>2<span>&#215;</span>1.5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Aug. 2019</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV32IM</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>VexRiscv (<span>&#215;</span>1)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/VexRiscv-19-08-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/VexRiscv-19-08-chip.jpg" class="chipimg">

## I. Freedom Chips

### I.1) Freedom Quad-core Rocket-chip

<p align="center"><b><font size=5>Summary</font></b></p>

<table>
  <tr>
    <td><b>Process</b></td>
    <td>ROHM-180nm</td>
  </tr>
  <tr>
    <td><b>Die</b></td>
    <td>5<span>&#215;</span>7.5-mm<sup>2</sup></td>
  </tr>
  <tr>
    <td><b>Fab. Date</b></td>
    <td>Oct. 2019</td>
  </tr>
  <tr>
    <td><b>ISA</b></td>
    <td>RV64GC</td>
  </tr>
  <tr>
    <td><b>Core</b></td>
    <td>Rocket (<span>&#215;</span>4)</td>
  </tr>
</table>

<p align="center"><b><font size=5>Layout</font></b></p>

<img src="/assets/sources/ChipCollection/Freedom-19-10-layout.jpg" class="chipimg">

<p align="center"><b><font size=5>Barechip</font></b></p>

<img src="/assets/sources/ChipCollection/Freedom-19-10-chip.jpg" class="chipimg">
