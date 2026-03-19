# Wallace-Tree-Multiplier-on-FPGA

## Objective
The goal of this project was to design and implement a high-speed 4×4 unsigned binary multiplier in Verilog using the Carry Save Adder (CSA) technique and Wallace Tree architecture. Specifically, the design focuses on reducing the number of generated partial products and minimizing half adder usage to lower circuit complexity and power consumption. The multiplier was synthesized and deployed on a Xilinx Spartan-6 FPGA, with performance evaluated across key metrics including speed, power efficiency, and hardware resource utilization.

## Architectural Block Diagram
The multiplier is organized into pipeline stages to optimize speed and resource usage:

<img width="727" height="397" alt="image" src="https://github.com/user-attachments/assets/562780db-c5f1-4aaa-8c19-14ddf5a670a4" />



* Inputs: Two 4-bit unsigned numbers (Multiplier A and Multiplicand B)

* Partial Product Generator: Generates 16 partial products using AND gates.

* Wallace Tree Reduction: Uses half adders (HAs) and full adders (FAs) to reduce partial products. Implemented using Carry Save Adders (CSA) for efficient addition.

* Final Carry Propagate Adder (CPA): Computes the final sum to generate the 8-bit product.

* Output: An 8-bit product representing the multiplication result. 

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
                         
    Multiplication of 4-bit Wallace tree
     
<img width="584" height="383" alt="image" src="https://github.com/user-attachments/assets/2d556ccb-acb9-4bea-9942-b0db9011f3f1" />

    Representation of Half adder & Full adder>
<img width="332" height="357" alt="image" src="https://github.com/user-attachments/assets/6917992e-98c4-4f2f-8daf-9aaa4a171f45" />

## Partial Product Generation in Wallace Tree Multiplier

The partial products along each diagonal line are aligned according to their binary weight, which
directly affects how they are summed in the next reduction stages. This representation clearly
illustrates how multiple rows of partial products are formed during binary multiplication. The
goal of the Wallace Tree method is to reduce these multiple rows into just two rows as
efficiently as possible using carry-save adders arranged in a tree-like structure. By reducing the
height of the partial product tree at each stage, the Wallace Tree approach ensures faster
computation compared to conventional add-and-shift methods.

    Partial Product Generation>

<img width="495" height="460" alt="image" src="https://github.com/user-attachments/assets/bfd4c664-12ea-4344-abcb-84cb92d89509" />


## Carry Save Adder

In our project, we are designing a 4×4-bit multiplier using the Carry Save Adder (CSA)
technique to efficiently perform partial product addition. Before diving into the design, it’s
important to understand how a CSA works and why it is beneficial for multiplication.
A Carry Save Adder is used when we need to add three or more binary numbers simultaneously.
Instead of immediately propagating the carry like in ripple or carry-lookahead adders, CSA
delays the carry propagation until the final addition step. 

This makes the addition process significantly faster, especially in applications like multipliers,
where multiple partial products are generated. In 4×4 multiplication, we generate 4 partial
product rows (since the multiplier is 4 bits wide). These partial products must be added together
to get the final 8-bit result. Traditional adders would perform this addition sequentially, with
each step waiting for the carry to propagate — which increases the delay. 

    Carry Save Adder (CSA) block
<img width="596" height="318" alt="image" src="https://github.com/user-attachments/assets/e4b63584-bbed-4f71-b01b-82957b2333e7" />


## Wallace Tree Implementation

Conventional multiplication follows the standard algorithm like manual multiplication. For
binary numbers, each bit of the multiplier is multiplied with the entire multiplicand to generate
partial products, which are then sequentially added using ripple carry adders or similar methods.
Wallace Tree multiplication is an optimized method for multiplying binary numbers. It reduces
the number of sequential addition steps by using a tree-like structure of Carry Save Adders
(CSAs) to add multiple partial products in parallel. The process continues until only two rows of
bits remain, which are then added using a carry propagate adder (like a ripple carry or carry
lookahead adder). 

    Wallace tree implementation>
<img width="1024" height="541" alt="image" src="https://github.com/user-attachments/assets/38bcf11c-1031-4a22-80c6-5c40475f5e23" />

    Comparision of Different Multiplication techniques 
<img width="773" height="325" alt="image" src="https://github.com/user-attachments/assets/db5d8b14-4a74-4600-9a6d-5f1dd5f49ce7" />

## RTL Design

Troubleshooting an RTL (Register Transfer Level) design, such as the one shown in the 
image, involves systematically identifying and resolving issues that arise during simulation, 
synthesis, or hardware implementation. The first step in troubleshooting begins with 
functional simulation. If the output doesn't match the expected results, designers should 
check the testbench for completeness and correctness. Verify that the correct input stimulus 
is being applied and that the clock (XSI_Clk) and reset signals are properly initialized. Any 
misbehaviour in logic often originates from incorrect signal timing or improper data flow 
across flip-flops and logic gates.

During synthesis, tools may report warnings or errors such as unconnected inputs/outputs or 
timing violations. It’s critical to resolve these warnings, as they may affect the synthesized 
netlist. Perform static timing analysis (STA) to ensure that timing constraints are met, 
especially setup and hold times.

The image represents an RTL (Register Transfer Level) schematic diagram of a digital logic 
design, likely part of a sequential circuit or FSM (Finite State Machine). It features multiple 
AND, OR, and NOT logic gates (labeled as pw2) and flip-flops (labeled as f1, f2, etc.), 
interconnected by red signal lines. These elements collectively implement specific logic 
functions. The presence of multiple flip-flops suggests a pipeline or register-based 
architecture. The design is modular, with signals branching across various logic blocks. The 
lower-left input named "XSI_Clk" indicates a clock signal for synchronous operation, 
making this suitable for synthesis in ASIC or FPGA implementations.

    RTL Design
<img width="411" height="602" alt="RTL" src="https://github.com/user-attachments/assets/aca8a051-393a-4a92-80a6-081cd0c3b36f" />

## Scope And Application

The Wallace Tree Multiplier is a high-speed, hardware-efficient digital circuit used for 
performing fast binary multiplication, especially in processors and digital signal processing 
(DSP) systems. Its scope extends into a wide range of computational domains where speed and 
power efficiency are paramount. Unlike traditional multiplication techniques, the Wallace Tree 
architecture reduces the critical path delay by organizing the addition of partial products in a 
tree-like structure using carry-save adders. This significantly decreases the time complexity of 
multiplication operations, making it highly suitable for high-performance computing 
environments.  

The scope of the Wallace Tree Multiplier includes both academic and industrial domains. From 
a learning perspective, it offers deep insight into digital arithmetic, parallel computing, and VLSI 
design, making it an essential component in engineering education. In terms of research, it 
continues to inspire innovations in low-power and high-speed arithmetic units, particularly in the 
areas of approximate computing and custom processor design. The architecture is scalable and 
can be adapted for n-bit multipliers, providing designers with flexibility in terms of performance 
and area optimization. 

In practical applications, Wallace Tree Multipliers are extensively used in microprocessors and 
digital signal processors, where multiplication is a fundamental operation. They play a critical 
role in arithmetic logic units (ALUs) for performing mathematical operations in CPUs and 
embedded systems. Their high speed makes them ideal for real-time image and video 
processing, where large volumes of pixel data require fast computation. Similarly, in machine 
learning and artificial intelligence (AI) accelerators, Wallace Tree Multipliers are often 
employed in matrix multiplication cores, particularly in convolutional layers of neural networks, 
to enhance the performance of deep learning computations. 

Moreover, Wallace Tree Multipliers are integral to cryptographic hardware, where fast 
multiplication of large binary numbers is required, such as in RSA encryption or ECC-based 
security systems. In control systems and robotics, these multipliers support real-time decision
making by enabling fast arithmetic processing. In digital communication systems, they are used 
in modulation and demodulation circuits, error detection and correction modules, and digital 
filters.

## Summary & Output
    Generated Summary report from Xilinx Software
<img width="938" height="611" alt="1" src="https://github.com/user-attachments/assets/73e62f9a-b0ff-429c-996d-503359e5b1f5" />
<img width="929" height="473" alt="3" src="https://github.com/user-attachments/assets/b1dee16d-c407-4ce3-8d9b-84a470568262" />
<img width="935" height="554" alt="2" src="https://github.com/user-attachments/assets/db176bb0-f7d4-439d-bd4d-67f4bc9efaf7" />

    Output on FPGA Board

![output](https://github.com/user-attachments/assets/9a1bc02a-51e7-480e-bf4a-e4faa67d503d)

## Conclusion

The implementation of the Wallace Tree Multiplier successfully demonstrates a high-speed 
and efficient method of binary multiplication. The design was tested using simulation tools 
and verified through logical analysis, confirming the correct generation and reduction of 
partial products, followed by accurate computation of the final multiplication result. 
Compared to traditional array and sequential multipliers, the Wallace Tree architecture 
significantly reduces the overall delay by minimizing the number of sequential additions 
required. The parallelism introduced during the partial product reduction stage results in a 
shorter critical path, enhancing the overall computation speed. 
 
In conclusion, the Wallace Tree Multiplier achieves the primary objectives of speed and 
efficiency, making it an essential building block for high-performance digital systems. Its 
ability to perform multiplication faster than conventional methods makes it ideal for time
sensitive applications such as image processing, cryptography, machine learning, and real
time embedded systems. This project highlights the advantages of parallelism in digital 
design and provides a practical approach for implementing complex arithmetic operations in 
hardware. The study and successful implementation of the Wallace Tree Multiplier not only 
reinforce theoretical concepts but also contribute towards developing efficient digital 
systems for modern computing applications.

##  References

[1] https://ieeexplore.ieee.org/document/7746174  
[2] G.Challa Ram, D.Sudha Rani, R.Balasaikesava, K.Bala Sindhuri,’’ Design of Delay 
Efficient Modified 16 bit Wallace Multiplier’’, IEEE International Conference On Recent 
Trends In Electronics Information Communication Technology, May 20-21, 2016, India  
[3] Sujan Sarkar1, Jishan Mehedi2, “Design of Hybrid (CSACSkA) Adder for Improvement 
of Propagation Delay,” 2017 third international conference on research in computational 
intelligence and communication networks  
[4] ShahzadAsifandYinanKong,“Low-Area Wallace Multiplier,”Hindawi Publishing 
Corporation VLSI Design Volume 2014, Article ID 343960.  
[5] Meenali Janveja and Vandana Niranjan,”High performance Wallace tree multiplier using 
improved adder”, ICTACT JOURNAL ON MICR 
[6] Kai Hwang “Computer Arithmetic: Principles, Architecture, and Design” John Wiley & 
Sons 1979 
[7] S. D. Pezaris "A 40-ns 17-Bit by 17-Bit Array Multiplier", IEEE Trans. on Computers, 
pp. 442-447,.Apr. 197 
[8] C. Baugh y A. Wooley "A Two's Complement Parallel Array Multiplication Algorithm". 
IEEE Trans.on Computer, Vol.C-22, Nº12. Dec.1973.  
[9] Weste, Neil H.E. Eshraghian, and kamran,” CMOS VLSI Design: A Circuit and System 
Prespective”, 3rd Edition, Pearson Education, pp. 345-356, 2005.  
[10] Neeta Sharma, Ravi Sindal “Modified Booth Multiplier using Wallace Structure and 
Efficient Carry Select Adder”,International Journal of Computer Applications (0975 – 8887) 
Volume 68– No.13, pp 40- 42,April 2013. C.S.Wallace,” A Suggestion for fast multipliers”, 
IEEE Trans. Electronics Computer. Vol. EC-13, PP. 14-17, Feb 1964
