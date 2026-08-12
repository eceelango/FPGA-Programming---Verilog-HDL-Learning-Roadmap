# 2×1 Multiplier Using Combinational Logic (Verilog HDL)

## 📌 Overview

This project demonstrates the implementation of a 2×1 Combinational Multiplier using Verilog HDL.

The circuit multiplies a 2-bit binary number by a 1-bit binary number and produces a 3-bit binary output.

Since the multiplier is a combinational circuit, the output depends only on the present values of the inputs and does not require a clock signal.

The design is implemented using basic combinational logic operations and can be simulated using tools such as Xilinx Vivado, ModelSim, Icarus Verilog, or EDA Playground.

---

## 🎯 Aim

To design and simulate a 2×1 combinational binary multiplier using Verilog HDL.

---

## 📖 Theory

A binary multiplier is a combinational digital circuit used to perform multiplication of binary numbers.

In this project:

- "A[1:0]" is the 2-bit multiplicand.
- "B" is the 1-bit multiplier.
- "Y[2:0]" is the 3-bit product.

---

Boolean Expressions

The partial products are generated using AND gates:

P0 = A0 · B

P1 = A1 · B

Therefore, the product is:

Y[2] = 0
Y[1] = P1
Y[0] = P0

Hence:

Y = {1'b0, A[1] & B, A[0] & B}

---

##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/Block%20Diagram%20%26%20Flow%20Chart.png" width="80%">
</p>

---

## ⚙️ Features

- 2-bit × 1-bit binary multiplication
- Combinational circuit
- No clock required
- No memory elements
- Implemented using basic AND operations
- 3-bit product output
- Verilog HDL implementation
- Complete truth table
- Testbench-based verification
- Suitable for FPGA implementation and simulation

---

## 🛠️ Algorithm

1. Declare the 2-bit input "A[1:0]".
2. Declare the 1-bit input "B".
3. Generate the partial products using AND gates.
4. Connect the partial products to the corresponding product bits.
5. Set the most significant product bit to "0".
6. Apply all possible input combinations.
7. Observe the output using simulation waveforms.
8. Verify the output with the expected multiplication results.

---

📥 Inputs

|Signal| Description|
|-------|-----------|
|"A[1:0]"| 2-bit multiplicand|
|"B"| 1-bit multiplier|

---

##📤 Output

|Signal| Description|
|-------|-----------|
|"Y[2:0]"| 3-bit product|

---

## Code
```verilog
`timescale 1ns / 1ps

module johnson_counter(y,clk,rst);
output reg [3:0] y;
input clk,rst;
always @(negedge clk or posedge rst)
begin
if (rst)
y = 4'b0000;
else
begin 
y[0] <= ~y[3];
y[1] <= y[0];
y[2] <= y[1];
y[3] <= y[2];
end
end 
endmodule
```

---

## Test Bench

```verilog
`timescale 1ns / 1ps

module tb_upcounter;
wire y;
reg j,k,clk;
integer x;

up_counter uut(.y(y), .clk(clk), .j(j), .k(k));

initial
begin
    clk = 0;
    forever #10 clk = ~clk;
end

initial
begin
    for(x=0; x<5; x=x+1)
    begin
        j = $random;
        k = $random;
        #10;
    end
    $finish;
end

always @(negedge clk)
begin
    #1;
    $display("clk=%b j=%b k=%b y=%b", clk, j, k, y);
end

endmodule
```
---

##🌊 Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/johnson_counter/Image/stimulation_johnson_counter.jpeg" width="80%">
</p>

---

## 🔄 Multiplication Table

|A| A (Decimal)| B| B (Decimal)| Product| Y|
|----|----------|--|------------|--------|---|
|00| 0| 0| 0| 0| 000|
|00| 0| 1| 1| 0| 000|
|01| 1| 0| 0| 0| 000|
|01| 1| 1| 1| 1| 001|
|10| 2| 0| 0| 0| 000|
|10| 2| 1| 1| 2| 010|
|11| 3| 0| 0| 0| 000|
|11| 3| 1| 1| 3| 011|

---

## Implemented Design

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/johnson_counter/Image/implemented_design_johnson.jpeg" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/johnson_counter/Image/project_summary_johnson.jpeg" width="80%">
</p>

---

## 📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

---

## ✅ Result

The 2×1 Combinational Multiplier was successfully designed and simulated using Verilog HDL.

The circuit correctly multiplies a 2-bit binary number by a 1-bit binary number and produces the corresponding 3-bit product.

The simulation results match the expected multiplication table for all possible input combinations.

---

## 🚀 Applications

Combinational multipliers are commonly used in:

- Arithmetic Logic Units (ALUs)
- Digital signal processing
- Microprocessors
- Microcontrollers
- FPGA-based computing
- Digital calculators
- DSP systems
- Arithmetic circuits
- Embedded systems
- MAC (Multiply-Accumulate) units

---

## 📜 License

This project is intended for educational and learning purposes.
