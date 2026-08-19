## 4-Bit Bidirectional Shift Register Using Verilog HDL

## 📌 Overview

This project demonstrates the implementation of a 4-Bit Bidirectional Shift Register using Verilog HDL.

A bidirectional shift register is a sequential digital circuit that can shift stored data in both left and right directions depending on the control signal.

In this design, a control input "dir" is used to select the direction of shifting:

- "dir = 0" → Shift Right
- "dir = 1" → Shift Left

The shift register operates on the positive edge of the clock and includes a reset functionality to clear all stored bits.

---

## 🎯 Aim

To design and simulate a 4-bit bidirectional shift register using Verilog HDL.

---

## 📖 Theory

A shift register is a sequential digital circuit used to store and shift binary data.

A 4-bit bidirectional shift register consists of four storage elements and can shift the stored data either toward the left or toward the right.

The direction of shifting is controlled using a direction input.

Shift Right

When:

dir = 0

the data shifts toward the right.

Q[3] → Q[2] → Q[1] → Q[0]

A serial input is introduced at "Q[3]".

Shift Left

When:

dir = 1

the data shifts toward the left.

Q[0] → Q[1] → Q[2] → Q[3]

A serial input is introduced at "Q[0]".

---

##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/Bidirectional_sreg/Image/Block%20diagram%20%26%20Flow%20chart_bidirectional_sreg.jpeg" width="80%">
</p>

---

## ⚙️ Features

- 4-bit bidirectional shift register
- Shift-left operation
- Shift-right operation
- Direction control input
- Serial input for both directions
- Positive edge-triggered clock
- Reset functionality
- Sequential circuit implementation
- Behavioral modeling using Verilog HDL
- Testbench-based verification
- Simulation waveform analysis

---

## 🛠️ Algorithm

1. Declare the clock, reset, direction control, serial input, and 4-bit output.
2. Initialize the shift register to "0000" when reset is active.
3. On every positive edge of the clock, check the direction control signal.
4. If "dir = 0", perform a right shift.
5. If "dir = 1", perform a left shift.
6. Insert the serial input into the appropriate end of the shift register.
7. Continue shifting according to the selected direction.
8. Observe the output using simulation waveforms.

---

## 📥 Inputs

|Signal| Description|
|------|------------|
|clk| Clock input|
|reset| Reset signal|
|dir| Direction control|
|serial_in| Serial data input|

---

## 📤 Output

|Signal| Description|
|------|-------------|
|q[3:0]| 4-bit shift register output|

---

## 💻 Code
```
`timescale 1ns / 1ps
module bidirectional_shift_register(
input clk,
input rst,
input dir,
input serial_in,
output reg[3:0]y
);
always @(negedge clk )begin 
if (rst) begin
y<=4'b0000;  //reset shift register
end
else if(dir) begin
y<={y[2:0],serial_in};//left shift
end
else begin
y<={serial_in,y[3:1]};//right shift
end
end
endmodule
```
## 🧪 Test Bench
```
`timescale 1ns / 1ps
module bidirectional_shift_register_tb;
reg clk;
reg rst;
reg dir;
reg serial_in;
wire[3:0]y;
bidirectional_shift_register DUT(
.clk(clk),
.rst(rst),
.dir(dir),
.serial_in(serial_in),
.y(y)
);
initial begin
clk=1'b0;
forever #5 clk=~clk;
end
initial begin
//initialize and reset
rst=1'b1;
dir=1'b0;
serial_in=1'b0;
#10;
rst=1'b0;
//shift right
dir=1'b0;
serial_in=1'b1;
#10;
//shift left
dir=1'b1;
serial_in=1'b0;
#10;
//apply reset again
rst=1'b1;
#10;
rst=1'b0;
//shift left
dir=1'b1;
serial_in=1'b0;
#10;
//shift right
dir=1'b0;
serial_in=1'b1;
#10;
$finish;
end
endmodule
```
--- 
🌊 Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/Bidirectional_sreg/Image/stimulation_bidirectional_sreg.jpeg" width="80%">
</p>

---
## EXPECTED OUTPUT
Shift Right

dir = 0

|serial_in  |  q|
|----------|------|
    |1   |    |1000|
   | 0  |     |0100|
    |1 |      |1010|
    |1|       |1101|

Shift Left

dir = 1

|serial_in |   q|
----------------
 |   0   |    1010|
  |  1  |     0101|
   | 0 |    1010|

---

##🔄 Shift Operation

|dir| Operation| Shift|
|----|---------|--------|
|0| Shift Right| {serial_in, q[3:1]}|
|1| Shift Left| {q[2:0], serial_in}|
---

## Reset Operation

|Reset| Operation|
|1| q = 0000|
|0| Normal shifting|
---

## 🏗️ Implemented Design

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/Bidirectional_sreg/Image/implemented_desgin_bidirectional_sreg.jpeg" width="80%">
</p>
---
## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/Bidirectional_sreg/Image/project_summary_bidirectional_sreg.jpeg" width="80%">
</p>

---

📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

✅ Result

The 4-Bit Bidirectional Shift Register was successfully designed and simulated using Verilog HDL.

The circuit correctly performs both left and right shifting operations according to the direction control signal.

The register also correctly resets its contents to "0000" when the reset signal is asserted.

🚀 Applications

Bidirectional shift registers are commonly used in:

- Data storage
- Serial-to-parallel conversion
- Parallel-to-serial conversion
- Data transfer
- Digital communication systems
- FPGA-based digital systems
- Microprocessors
- Microcontrollers
- Digital control systems
- Data manipulation circuits



This project is intended for educational and learning purposes.
