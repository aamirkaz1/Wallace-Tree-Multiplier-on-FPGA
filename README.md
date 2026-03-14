# Wallace-Tree-Multiplier-on-FPGA

## Objective
The goal of this project was to design and implement a high-speed 4×4 unsigned binary multiplier in Verilog using the Carry Save Adder (CSA) technique and Wallace Tree architecture. Specifically, the design focuses on reducing the number of generated partial products and minimizing half adder usage to lower circuit complexity and power consumption. The multiplier was synthesized and deployed on a Xilinx Spartan-6 FPGA, with performance evaluated across key metrics including speed, power efficiency, and hardware resource utilization.

## Architectural Block Diagram
The multiplier is organized into pipeline stages to optimize speed and resource usage:

<image>

Inputs: Two 4-bit unsigned numbers (Multiplier A and Multiplicand B).
Partial Product Generator: Generates 16 partial products using AND gates.
Wallace Tree Reduction: Uses half adders (HAs) and full adders (FAs) to reduce partial
products. Implemented using Carry Save Adders (CSA) for efficient addition.
Final Carry Propagate Adder (CPA): Computes the final sum to generate the 8-bit product.
Output: An 8-bit product representing the multiplication result. 

## Theory

A Wallace tree is a very useful hardware function that is used in digital circuits for multiplies
two integers. In Wallace method the multiplication of two numbers is done by reducing the
partial product matrix into a two-row matrix by a half adder, full adder, carry-save adder & these
two rows are added utilizing a fast carry propagate adder to produce the output product. In this
Wallace tree method, we used half adder for summation of 2 bit and full adder for summation of
3 bit. For multiplicands of higher than 8-bits this advantage is more beneficial, because the
addition of partial products is low in Wallace tree and hence increases speed. Here each bit of
each partial product in every column is added together by a set of counters used in parallel so
that no curry is propagated further. Then this matrix is reduced by another set of counters until a
two-row matrix generates.
In the Wallace tree approach, multiplication is achieved by reducing the partial product matrix
Department Of Electronics and Telecommunication Engineering 4
into a two-row matrix. This is done using a hierarchical structure that employs half adders, full
adders, and carry-save adders. Initially, the partial products generated from the multiplication of
bits are organized into a matrix form. Each column of this matrix contains bits that represent
partial products of the input operands. To reduce the matrix, the Wallace tree uses adders in
stages. A half adder is used when there are only two bits to be added in a column, and a full
adder is used when there are three bits. The output from these adders includes a sum and a carry,
where the sum remains in the same column, and the carry is moved to the next higher column.
These stages are repeated iteratively until the partial product matrix is reduced to only two rows.
These final two rows are then added using a fast carry propagate adder to produce the final
product. 
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

## Calculations 

The Wallace Tree Multiplier is designed to minimize the overall delay by reducing the number
of sequential addition steps. After the partial products are generated, they are passed on to the
reduction stage, where they are efficiently summed using a structure of carry-save adders
arranged in a tree-like format. This reduces the number of partial product rows layer by layer
until only two rows remain, which are then added using a conventional fast adder to produce the
final multiplication result. 

The partial products along each diagonal line are aligned according to their binary weight, which
directly affects how they are summed in the next reduction stages. This representation clearly
illustrates how multiple rows of partial products are formed during binary multiplication. The
goal of the Wallace Tree method is to reduce these multiple rows into just two rows as
efficiently as possible using carry-save adders arranged in a tree-like structure. By reducing the
height of the partial product tree at each stage, the Wallace Tree approach ensures faster
computation compared to conventional add-and-shift methods.

<image of Multiplication of 4-bit Wallace tree >
<image of Representation of Half adder & Full adder>


##  References
G. Challa Ram et al., Design of Delay Efficient Modified 16-bit Wallace Multiplier, IEEE RTEICT 2016

Sujan Sarkar, Jishan Mehedi, Design of Hybrid (CSACSkA) Adder for Improvement of Propagation Delay, ICRCICN 2017

Shahzad Asif and Yinan Kong, Low-Area Wallace Multiplier, Hindawi VLSI Design, 2014

C. S. Wallace, A Suggestion for Fast Multipliers, IEEE Trans. Electronics Computer, Vol. EC-13, Feb 1964

Kai Hwang, Computer Arithmetic: Principles, Architecture, and Design, John Wiley & Sons, 1979

Weste, Eshraghian & Kamran, CMOS VLSI Design, 3rd Edition, Pearson Education, 2005
