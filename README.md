# Wallace-Tree-Multiplier-on-FPGA

## Overview
Multiplication is one of the most fundamental operations in digital systems, widely used in Digital Signal Processing (DSP), cryptography, and embedded systems. Traditional multipliers often suffer from significant latency due to carry propagation. 

This project implements a **4×4 Wallace Tree Multiplier** using the Carry Save Adder (CSA) technique in Verilog HDL, targeting the **Xilinx Spartan-6 (XC6SLX9)** FPGA. The design achieves:
* **Reduced critical path delay** through parallel partial product reduction.
* **Lower power consumption** by minimizing the number of adder stages.
* **Efficient hardware utilization** using only 7 LUTs and 4 occupied slices on the FPGA.

## Architecture
The multiplier is organized into pipeline stages to optimize speed and resource usage:

```text
[Multiplier A] ──┐
                 ├──► [Partial Product Generator] ──► [Wallace Tree Reduction] ──► [Carry Propagate Adder] ──► [8-bit Product]
[Multiplicand B] ┘         (AND gates)                  (Half/Full Adders, CSA)          (RCA/CLA)

```
## Methodology 
* **Partial Product Generation**
  
Each bit of multiplicand A is ANDed with each bit of multiplier B using AND gates, producing 16 partial product bits (a 4×4 matrix). All partial products are generated in parallel.

* **Wallace Tree Reduction**

The partial product matrix is reduced layer by layer using:

   1) Half Adder (HA): For columns with 2 bits.

   2) Full Adder (FA): For columns with 3 bits.

   3) Carry Save Adder (CSA): Delays carry propagation for speed.
      Reduction continues until only two rows remain.

* **Final Addition**
The two remaining rows are summed using a Carry Propagate Adder (CPA) to produce the final 8-bit product.

## Comparison of Multiplication Techniques



## Hardware & Software Specifications

### 1) Hardware

* FPGA      :  AMD Xilinx Spartan-6 XC6SLX9 (CSG324 package)
* Memory  :    512 Mb LPDDR @ 166 MHz
* Flash  :    16 Mb SPI Flash (M25P16)
* I/O     :   8 LEDs, 6 push buttons, 8-way DIP switch
* Display  :  3-digit seven-segment display
* Programming : USB 2.0 (JTAG + USB)

### 2) Software

* Xilinx ISE : 14.7	Synthesis, Implementation, Bitstream Generation
* Verilog HDL	: Hardware Description Language
* ISim / ModelSim	: Functional & Timing Simulation


##  References
G. Challa Ram et al., Design of Delay Efficient Modified 16-bit Wallace Multiplier, IEEE RTEICT 2016

Sujan Sarkar, Jishan Mehedi, Design of Hybrid (CSACSkA) Adder for Improvement of Propagation Delay, ICRCICN 2017

Shahzad Asif and Yinan Kong, Low-Area Wallace Multiplier, Hindawi VLSI Design, 2014

C. S. Wallace, A Suggestion for Fast Multipliers, IEEE Trans. Electronics Computer, Vol. EC-13, Feb 1964

Kai Hwang, Computer Arithmetic: Principles, Architecture, and Design, John Wiley & Sons, 1979

Weste, Eshraghian & Kamran, CMOS VLSI Design, 3rd Edition, Pearson Education, 2005
