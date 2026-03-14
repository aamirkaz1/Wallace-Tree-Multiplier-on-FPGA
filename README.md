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
  

