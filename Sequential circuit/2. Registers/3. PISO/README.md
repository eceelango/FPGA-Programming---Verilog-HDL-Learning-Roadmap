## 4-Bit PISO Shift Register Using Verilog HDL
---
##📌 Overview

This project demonstrates the implementation of a 4-Bit PISO (Parallel-In Serial-Out) Shift Register using Verilog HDL.

A PISO shift register is a sequential digital circuit that accepts multiple bits of data simultaneously through parallel inputs and then shifts the stored data out one bit at a time through a serial output.

The register uses a load control signal to select between parallel loading and serial shifting.

- "load = 1" → Parallel Load
- "load = 0" → Shift Operation

The shift register operates on the positive edge of the clock and includes a reset functionality.
---

##🎯 Aim

To design and simulate a 4-bit PISO Shift Register using Verilog HDL.

---

##📖 Theory

PISO stands for Parallel-In Serial-Out.

A PISO shift register allows 4 bits of parallel data to be loaded into the register simultaneously. Once the data is loaded, the bits are shifted out sequentially through a single serial output.

For a 4-bit PISO register:

Parallel Input = P[3:0]
Serial Output  = serial_out

The parallel data is loaded when "load = 1".

When "load = 0", the stored data is shifted toward the serial output on every positive edge of the clock.

Parallel Load

When:

load = 1

the register loads all four input bits simultaneously.

P[3:0] → Q[3:0]

Serial Shift

When:

load = 0

the stored data shifts one position on every positive clock edge.

For right shifting:

Q[3] → Q[2] → Q[1] → Q[0] → serial_out

---

##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/3.%20PISO/Image/Block%20diagram%20%26%20Flow%20chart_PISO.jpeg" width="80%">
</p>

---

⚙️ Features

- 4-bit PISO shift register
- Parallel data loading
- Serial data output
- Load control signal
- Positive edge-triggered clock
- Reset functionality
- Sequential circuit implementation
- Behavioral modeling using Verilog HDL
- Testbench-based verification
- Simulation waveform analysis

---

##🛠️ Algorithm

1. Declare the clock, reset, load control, parallel input, and serial output.
2. Initialize the shift register to "0000" when reset is active.
3. On every positive edge of the clock, check the "load" signal.
4. If "load = 1", load the 4-bit parallel input into the shift register.
5. If "load = 0", shift the stored data toward the serial output.
6. Continue shifting one bit at a time.
7. Observe the serial output using simulation waveforms.

---

##📥 Inputs

Signal| Description
"clk"| Clock input
"reset"| Reset signal
"load"| Parallel load control
"parallel_in[3:0]"| 4-bit parallel data input

---

##📤 Output

Signal| Description
"serial_out"| Serial data output

---

##💻 Code
```
module register(dout,din,clk,load);
input [3:0] din;
input clk,load;
output dout;
reg [3:0] q;
always@(posedge clk)
begin
if (load)
begin
q[0]<=din[0];
q[1]<=din[1];
q[2]<=din[2];
q[3]<=din[3];
end
else
begin
q[0]<=1'b0;
q[1]<=q[0];
q[2]<=q[1];
q[3]<=q[2];
end
end
assign dout=q[3];
endmodule
```
##🧪 Test Bench

```
module register_tb;
reg [3:0] din;
reg clk,load;
wire dout;
register uut(dout,din,clk,load);
always #5 clk=~clk;
initial
begin
$monitor("time=%0t clk=%b load=%b din=%b dout=%b",$time,clk,load,din,dout);
clk=0;
load=0;
din=4'b0000;
#10;
load=1;
din=4'b1011;
#10;
load=0;
#40;
$finish;
end
endmodule
```
---

##🌊 Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/3.%20PISO/Image/stimulation_PISO.jpeg" width="80%">
</p>
---

##🔄 Operation

"load"| Operation
"0"| Serial Shift
"1"| Parallel Load

Parallel Load

load = 1

The 4-bit input is loaded simultaneously:

parallel_in[3:0] → q[3:0]

Serial Shift

load = 0

The stored data shifts toward the serial output:

q[3] → q[2] → q[1] → q[0] → serial_out

---

##🏗️ Implemented Design


<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/3.%20PISO/Image/implemented_desgin_PISO.jpeg" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/2.%20Registers/3.%20PISO/Image/project_summary_PISO.jpeg" width="80%">
</p>

---

##📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

##✅ Result

The 4-Bit PISO Shift Register was successfully designed and simulated using Verilog HDL.

The circuit correctly loads 4-bit parallel data when the "load" signal is asserted and shifts the stored data serially when the "load" signal is deasserted.

The simulation verifies that the parallel input data is successfully converted into a serial data stream.

##🚀 Applications

PISO shift registers are commonly used in:

- Parallel-to-serial data conversion
- Serial communication
- Data transmission
- Microprocessors
- Microcontrollers
- FPGA-based systems
- Digital communication systems
- Data storage
- GPIO expansion
- Data transfer circuits
---

##📜 License

This project is intended for educational and learning purposes.
