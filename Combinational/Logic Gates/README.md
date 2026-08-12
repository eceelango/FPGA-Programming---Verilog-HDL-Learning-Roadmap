# Basic Logic Gates Using Verilog HDL

A simple Verilog HDL project demonstrating the **design, simulation, and verification of fundamental digital logic gates** using Verilog gate-level primitives.

## 📌 Overview

This project implements and verifies the following seven logic gates:

* Buffer
* NOT (Inverter)
* AND
* OR
* NAND
* XOR
* XNOR

The design is written in **Verilog HDL** and verified using a **testbench** by applying all possible combinations of input signals.

## 🎯 Aim

To design and simulate the **Buffer, NOT, AND, OR, NAND, XOR, and XNOR gates** using Verilog HDL and verify their functionality using simulation waveforms.

## 🧠 Logic Gates

| Gate   | Boolean Expression | Function                       |
| ------ | ------------------ | ------------------------------ |
| Buffer | `Y = A`            | Output follows input           |
| NOT    | `Y = A'`           | Produces complement of input   |
| AND    | `Y = A · B`        | 1 when both inputs are 1       |
| OR     | `Y = A + B`        | 1 when at least one input is 1 |
| NAND   | `Y = (A · B)'`     | Complement of AND              |
| XOR    | `Y = A ⊕ B`        | 1 when inputs are different    |
| XNOR   | `Y = A ⊙ B`        | 1 when inputs are equal        |

## 📊 Truth Table

| A | B | Buffer | NOT | AND | OR | NAND | XOR | XNOR |
| - | - | ------ | --- | --- | -- | ---- | --- | ---- |
| 0 | 0 | 0      | 1   | 0   | 0  | 1    | 0   | 1    |
| 0 | 1 | 0      | 1   | 0   | 1  | 1    | 1   | 0    |
| 1 | 0 | 1      | 0   | 0   | 1  | 1    | 1   | 0    |
| 1 | 1 | 1      | 0   | 1   | 1  | 0    | 0   | 1    |

### Gate-Level Modeling

Each primitive directly represents a physical logic gate:

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/Logic%20Gates/Image/Gates.png" width="80%">
</p>

## 💻 Verilog Design

## AND

```verilog
`timescale 1ns / 1ps
module AND_Gate(y,a,b);
output y;
input a,b;
assign y = a & b;
endmodule
```
## OR

```verilog
`timescale 1ns / 1ps
module OR_Gate(y,a,b);
output y;
input a,b;
assign y = a | b;
endmodule
```
## NOT

```verilog
`timescale 1ns / 1ps
module NOT_Gate(y,a);
output y;
input a;
y = ~a;
endmodule
```
## BUFFER

```verilog
`timescale 1ns / 1ps
module BUFFER_Gate(y,a);
output y;
input a;
y = a;
endmodule
```

## NAND

```verilog
`timescale 1ns / 1ps
module NAND_Gate(y,a,b);
output y;
input a,b;
assign y = ~(a & b);
endmodule

```
## NOR

```verilog
`timescale 1ns / 1ps
module NOR_Gate(y,a,b);
output y;
input a,b;
assign y = ~(a | b);
endmodule
```
## XOR

```verilog
`timescale 1ns / 1ps
module XOR_Gate(y,a,b);
output y;
input a,b;
assign y = a ^ b;
endmodule
```
## XNOR

```verilog
`timescale 1ns / 1ps
module XNOR_Gate(y,a,b);
output y;
input a,b;
assign y = ~(a ^ b);
endmodule

```

## 🧪 Testbench

The testbench applies all four possible combinations of the two inputs:

```verilog
`timescale 1ns / 1ps
module tb_Gate;
reg a,b;
wire y;
Gatename_Gate uut ( y,a,b ); // Change Gatename 
initial begin
$monitor("Time=%0t | a=%b b=%b | y=%b", $time, a, b, y);
a = 0; b = 0;     #10;
a = 0; b = 1;     #10;
a = 1; b = 0;     #10;
a = 1; b = 1;     #10;
$finish;
end
endmodule

```

## 🔬 Simulation

The testbench verifies the following input combinations:

```text
A B | BUF NOT AND OR NAND XOR XNOR
-----------------------------------
0 0 |  0   1   0  0   1   0    1
0 1 |  0   1   0  1   1   1    0
1 0 |  1   0   0  1   1   1    0
1 1 |  1   0   1  1   0   0    1
```

The simulation waveform should match the expected truth table for all seven gates.

## 🛠️ Tools

This project can be simulated using:

* **Xilinx Vivado**
* **ModelSim**
* **Icarus Verilog**
* **EDA Playground**

## 📂 Project Structure

```text
Basic-Logic-Gates-Verilog/
│
├── logic_gates.v
├── tb_logic_gates.v
└── README.md
```

## 🔄 Verification Method

1. Declare the input and output signals.
2. Implement each gate using Verilog gate primitives.
3. Create a testbench.
4. Apply all possible input combinations.
5. Observe the generated outputs.
6. Compare the simulation results with the expected truth table.
7. Verify the corresponding waveform.

## 📚 Concepts Covered

* Digital Logic Gates
* Boolean Algebra
* Truth Tables
* Combinational Logic
* Verilog HDL
* Gate-Level Modeling
* Verilog Primitive Gates
* Testbench Development
* Simulation
* Waveform Analysis
* Functional Verification

## 🚀 Applications

Logic gates form the foundation of larger digital systems, including:

* Adders and subtractors
* Multiplexers and demultiplexers
* Encoders and decoders
* Comparators
* Flip-flops
* Registers
* Counters
* ALUs
* Control circuits
* Digital communication systems
* Processor architectures
* FPGA-based digital systems

## ✅ Result

The **Buffer, NOT, AND, OR, NAND, XOR, and XNOR gates** were successfully implemented using **Verilog HDL gate-level primitives**.

All possible input combinations were tested, and the simulation results matched the expected truth tables.

## 📜 License

This project is intended for **educational and learning purposes**.
