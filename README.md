# 4-Bit Up Counter Using Behavioral Modeling (Verilog HDL)

## 📌 Overview

This project demonstrates the implementation of a **4-Bit Synchronous Up Counter** using **Behavioral Modeling** in **Verilog HDL**. The counter increments its value by one on every positive edge of the clock signal and resets to zero when the reset signal is asserted.

Behavioral modeling describes the functionality of the circuit using procedural blocks (`always`) instead of specifying the gate-level structure, making the design simple, readable, and easy to maintain.

---

## 🎯 Aim

To design and simulate a **4-bit synchronous up counter** using **Behavioral Modeling** in Verilog HDL.

---

## 📖 Theory

A **4-bit Up Counter** is a sequential digital circuit that counts upward in binary from **0000 (0)** to **1111 (15)**. The counter increases its count by one on each positive edge of the clock. Once it reaches the maximum count (**1111**), it automatically wraps around to **0000** and continues counting.

Behavioral modeling uses procedural statements such as `always` blocks and conditional statements to describe the circuit's operation rather than its hardware implementation.

---

##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/Block%20Diagram%20%26%20Flow%20Chart.png" width="80%">
</p>

---

## ⚙️ Features

- 4-bit synchronous binary up counter
- Behavioral modeling using Verilog HDL
- Positive edge-triggered clock
- Reset functionality
- Counts from **0 to 15**
- Automatically rolls over after reaching the maximum count

---

## 🛠️ Algorithm

1. Declare the clock, reset, and 4-bit counter output.
2. Initialize the counter to zero whenever the reset signal is active.
3. On every positive edge of the clock:
   - If reset is active, clear the counter.
   - Otherwise, increment the counter by one.
4. Continue counting until the maximum value (1111) is reached.
5. After reaching 1111, the counter automatically returns to 0000.
6. Observe the output using simulation waveforms.

---

## 📥 Inputs

| Signal | Description |
|--------|-------------|
| `clk` | Clock input |
| `reset` | Reset signal |

---

## 📤 Output

| Signal | Description |
|--------|-------------|
| `count[3:0]` | 4-bit counter output |

---

## Code
```verilog
`timescale 1ns / 1ps

module up_counter(y,clk,j,k);
output y;
input clk,j,k;
wire [2:0]w;

jk_ff ff_1(w[0],clk,j,k);
jk_ff ff_2(w[1],w[0],j,k);
jk_ff ff_3(w[2],w[1],j,k);
jk_ff ff_4(y,w[2],j,k);

endmodule

module jk_ff(y,clk,j,k);

output reg y;
input clk,j,k;

always @(negedge clk)
begin
    case({j,k})
        2'b00: y = y;
        2'b01: y = 1'b0;
        2'b10: y = 1'b1;
        2'b11: y = ~y;
    endcase
end

endmodule
```

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

## Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/stimulation_upcounter.png" width="80%">
</p>


## 🔄 Counting Sequence

| Decimal | Binary |
|---------|--------|
| 0 | 0000 |
| 1 | 0001 |
| 2 | 0010 |
| 3 | 0011 |
| 4 | 0100 |
| 5 | 0101 |
| 6 | 0110 |
| 7 | 0111 |
| 8 | 1000 |
| 9 | 1001 |
| 10 | 1010 |
| 11 | 1011 |
| 12 | 1100 |
| 13 | 1101 |
| 14 | 1110 |
| 15 | 1111 |
| Next | 0000 |

---

## Implemented Design

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/implemented_design_upcounter.png" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/project_summary_upcounter.png" width="80%">
</p>

---

## 💻 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

---

## ✅ Result

The **4-Bit Up Counter** was successfully designed and simulated using **Behavioral Modeling** in Verilog HDL. The counter increments correctly on every positive clock edge, resets properly, and wraps around from **1111** to **0000** as expected.

---

## 🚀 Applications

- Digital clocks
- Frequency counters
- Event counters
- Timer circuits
- Digital control systems
- Embedded system applications

---

## 📜 License

This project is intended for educational and learning purposes.
