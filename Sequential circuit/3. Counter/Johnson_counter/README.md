## 4-Bit Johnson Counter Using Verilog HDL

---

## 📌 Overview

This project demonstrates the implementation of a 4-Bit Johnson Counter using Verilog HDL.

A Johnson Counter, also known as a Twisted Ring Counter, is a sequential digital circuit formed by connecting the complemented output of the last flip-flop back to the input of the first flip-flop.

For a 4-bit Johnson Counter, the circuit produces 8 unique states before repeating. The counter shifts its contents on every positive edge of the clock signal.

---

## 🎯 Aim

To design and simulate a 4-bit Johnson Counter using Verilog HDL.

---

## 📖 Theory

A Johnson Counter is a modified ring counter in which the complement of the last flip-flop output is fed back to the first flip-flop input.

For an n-bit Johnson Counter, the number of unique states is:

Number of states = 2n

Therefore, a 4-bit Johnson Counter has:

2 × 4 = 8 unique states

The counting sequence is:

0000
1000
1100
1110
1111
0111
0011
0001
0000

The counter shifts its data by one position at every clock edge while the inverted output of the last flip-flop is fed back to the first flip-flop.

---

## Block Diagram
<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/3.%20Counter/Johnson_counter/Image/Block%20diagram%20%26%20Flow%20chart.jpeg" width="80%">
</p>

---

## ⚙️ Features

- 4-bit Johnson Counter
- Twisted Ring Counter implementation
- 8 unique counting states
- Positive edge-triggered clock
- Synchronous sequential operation
- Reset functionality
- Behavioral modeling using Verilog HDL
- Automatically repeats the sequence after 8 states
  
---

## 🛠️ Algorithm

1. Declare the clock, reset, and 4-bit counter output.
2. Initialize the counter to "0000" when reset is active.
3. On every positive edge of the clock:
   - Shift the current counter value by one position.
   - Feed the complement of the last bit back into the first bit.
4. Continue the shifting operation for every clock cycle.
5. Observe the 8-state Johnson Counter sequence using simulation waveforms.
6. After reaching "0001", the counter returns to "0000" and repeats the sequence.
   
---

## 📥 Inputs

Signal| Description
"clk"| Clock input
"reset"| Reset signal

---

## 📤 Output

Signal| Description
"count[3:0]"| 4-bit Johnson Counter output

---

## 💻 Code

`timescale 1ns / 1ps

module johnson_counter(
    output reg [3:0] count,
    input clk,
    input reset
);

always @(posedge clk)
begin
    if (reset)
        count <= 4'b0000;
    else
        count <= {count[2:0], ~count[3]};
end

endmodule

---

## 🧪 Test Bench

`timescale 1ns / 1ps

module tb_johnson_counter;

reg clk;
reg reset;
wire [3:0] count;

johnson_counter uut(
    .count(count),
    .clk(clk),
    .reset(reset)
);

initial
begin
    clk = 0;
    forever #10 clk = ~clk;
end

initial
begin
    reset = 1;
    #20;

    reset = 0;
    #180;

    $finish;
end

always @(posedge clk)
begin
    #1;
    $display("clk=%b reset=%b count=%b", clk, reset, count);
end

endmodule

---

## 🌊 Waveform
<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/3.%20Counter/Johnson_counter/Image/stimulation_johnson_counter.jpeg" width="80%">
</p>


## 🔄 Counting Sequence

Clock Cycle| Decimal| Binary
0| 0| "0000"
1| 8| "1000"
2| 12| "1100"
3| 14| "1110"
4| 15| "1111"
5| 7| "0111"
6| 3| "0011"
7| 1| "0001"
8| 0| "0000"

State Sequence

0000
  ↓
1000
  ↓
1100
  ↓
1110
  ↓
1111
  ↓
0111
  ↓
0011
  ↓
0001
  ↓
0000

The sequence repeats continuously.

---

## 🔧 Working Principle

The Johnson Counter works by shifting the bits of the counter on every positive clock edge.

The important operation is:

count <= {count[2:0], ~count[3]};

Here:

- "count[2:0]" shifts the existing bits.
- "~count[3]" generates the complement of the most significant bit.
- The complemented bit is inserted into the least significant position.

For example:

Initial:       0000

~count[3] = 1

Next state:    1000

Then:

1000 → 1100
1100 → 1110
1110 → 1111
1111 → 0111
0111 → 0011
0011 → 0001
0001 → 0000

---

## 🏗️ Implemented Design
<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/3.%20Counter/Johnson_counter/Image/implemented_design_johnson.jpeg" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/3.%20Counter/Johnson_counter/Image/project_summary_johnson.jpeg" width="80%">
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

The 4-Bit Johnson Counter was successfully designed and simulated using Verilog HDL.

The counter produces 8 unique states and continuously follows the Johnson Counter sequence:

0000 → 1000 → 1100 → 1110 → 1111 → 0111 → 0011 → 0001 → 0000

The design demonstrates the operation of a Twisted Ring Counter using behavioral modeling in Verilog HDL.

---

## 🚀 Applications

Johnson Counters are commonly used in:

- Sequence generators
- Timing circuits
- Frequency division
- Digital control systems
- Counter circuits
- LED chaser circuits
- Clock generation and sequencing
- State-machine applications
- Digital communication systems
  
---

## 📚 Concepts Covered

- Sequential circuits
- Flip-flops
- Shift registers
- Johnson Counter
- Ring Counter
- Behavioral modeling
- Clocked "always" blocks
- Reset operation
- Bit concatenation
- Non-blocking assignments
- Digital simulation
  
---

##📜 License

This project is intended for educational and learning purposes.
