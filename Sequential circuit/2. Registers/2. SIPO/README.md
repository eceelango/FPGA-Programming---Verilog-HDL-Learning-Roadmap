##4-Bit SIPO Shift Register Using Verilog HDL

##📌 Overview

This project demonstrates the implementation of a 4-Bit SIPO (Serial-In Parallel-Out) Shift Register using Verilog HDL.

A SIPO shift register is a sequential digital circuit that accepts data one bit at a time through a serial input and provides the stored data simultaneously through multiple parallel outputs.

The register shifts the incoming serial data on every positive edge of the clock and includes a reset functionality.
---
##🎯 Aim

To design and simulate a 4-bit SIPO Shift Register using Verilog HDL.
---
##📖 Theory

SIPO stands for Serial-In Parallel-Out.

A SIPO shift register receives serial data through a single input and converts it into parallel data available at multiple outputs.

For a 4-bit SIPO register:

Serial Input = serial_in
Parallel Output = q[3:0]

The serial data is shifted into the register one bit at a time on every positive edge of the clock.

After four clock cycles, the complete 4-bit data becomes available at the parallel output.

Serial Input

The incoming data enters the shift register through the serial input:

serial_in → Q[3] → Q[2] → Q[1] → Q[0]

The stored data can be accessed simultaneously through:

Q[3:0]
---
##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/2.%20SIPO/Image/Block%20diagram%20%26%20Flow%20chart_SIPO.jpeg" width="80%">
</p>

---
##⚙️ Features

- 4-bit SIPO shift register
- Serial data input
- 4-bit parallel output
- Positive edge-triggered clock
- Reset functionality
- Sequential circuit implementation
- Behavioral modeling using Verilog HDL
- Testbench-based verification
- Simulation waveform analysis
---
##🛠️ Algorithm

1. Declare the clock, reset, serial input, and 4-bit parallel output.
2. Initialize the shift register to "0000" when reset is active.
3. On every positive edge of the clock, shift the existing data.
4. Insert the serial input into the appropriate end of the register.
5. Continue shifting the incoming serial data for every clock cycle.
6. Observe the 4-bit parallel output.
7. Verify the output after four clock cycles.
---
##📥 Inputs

Signal| Description
"clk"| Clock input
"reset"| Reset signal
"serial_in"| Serial data input
---
##📤 Output

Signal| Description
"parallel_out[3:0]"| 4-bit parallel data output
---
##💻 Code
```
`timescale 1ns / 1ps

module register(dout,din,clk);
output dout;
input din,clk;
reg q3,q2,q1,q0;
always@(posedge clk)
begin
q3<=din;
q2<=q3;
q1<=q2;
q0<=q1;
end
assign dout=q0;
endmodule
```
##🧪 Test Bench
```
`timescale 1ns / 1ps

module sipo_tb(
input clk,
input reset,
input sin,
output reg [3:0] q);
always @(posedge clk or posedge reset)
begin
if (reset)
q<= 4'b0000;
else
begin
q[3] <= q[2];
q[2] <= q[1];
q[1] <= q[0];
q[0] <= sin;
end
end
endmodule

```
---
##🌊 Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/2.%20SIPO/Image/stimulation_SIPO.jpeg" width="80%">
</p>

---
##🔄 Shift Operation

At every positive edge of the clock:

parallel_out <= {parallel_out[2:0], serial_in};

The data shifts toward the MSB while the new serial bit enters at the LSB.

For example:

Initial     = 0000

Serial = 1  → 0001
Serial = 0  → 0010
Serial = 1  → 0101
Serial = 1  → 1011

Thus:

Serial Input:    1 → 0 → 1 → 1

Parallel Output: 1011
---
##🏗️ Implemented Design

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/2.%20SIPO/Image/implemented_desgin_SIPO.jpeg" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/2.%20SIPO/Image/project_summary_SIPO.jpeg" width="80%">
</p>

---
##📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground
---
##✅ Result

The 4-Bit SIPO Shift Register was successfully designed and simulated using Verilog HDL.

The circuit correctly accepts serial data one bit at a time and produces the corresponding 4-bit parallel output after four clock cycles.

The simulation verifies the serial-to-parallel data conversion and correct shifting operation.
---
##🚀 Applications

SIPO shift registers are commonly used in:

- Serial-to-parallel data conversion
- Data communication systems
- Microprocessors
- Microcontrollers
- FPGA-based systems
- Digital communication
- Data storage
- GPIO expansion
- LED control
- Digital signal processing
---

##📜 License

This project is intended for educational and learning purposes.
