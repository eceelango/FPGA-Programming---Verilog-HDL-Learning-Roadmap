# D Flip-Flop Using Verilog HDL

## 📌 Overview

This project demonstrates the implementation and simulation of a **D (Data/Delay) Flip-Flop** using Verilog HDL.

A D Flip-Flop is a sequential digital circuit capable of storing **one bit of information**. It has a single data control input:

- `D` → Data

The output follows the value of `D` at the **positive edge of the clock**, eliminating the invalid state present in the SR Flip-Flop.

The D Flip-Flop is implemented using **Behavioral Modeling** in Verilog HDL.

---

## 🎯 Aim

To design and simulate a **D Flip-Flop** using Behavioral Modeling in Verilog HDL.

---

## 🧠 Theory

A D Flip-Flop is a basic memory element capable of storing a single binary bit.

It has the following signals:

| Signal | Description |
|--------|-------------|
| `D` | Data input |
| `clk` | Clock input |
| `rst` | Asynchronous reset input |
| `Q` | Main output |
| `Q_bar` | Complementary output |

The operation of the D Flip-Flop is controlled by the clock signal.

The state changes only at the **positive edge (`posedge`)** of the clock, at which point `Q` takes on the value of `D`.

---
##  Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/Block%20Diagram%20%26%20Flow%20Chart.png" width="80%">
</p>
---

## 🔄 Operation

| D | Q(next) | Q_bar(next) | Operation |
|---|---------|-------------|-----------|
| 0 | 0 | 1 | Reset (transfer 0) |
| 1 | 1 | 0 | Set (transfer 1) |

Where:

- The D Flip-Flop has **no invalid state**, unlike the SR Flip-Flop.
- `Q` simply follows `D` on every positive clock edge.

---

## ⚙️ Features

- D Flip-Flop implementation
- Behavioral modeling using Verilog HDL
- Positive-edge-triggered clock
- Asynchronous active-low reset
- No invalid/undefined state
- Stores one bit of data
- Complementary output
- Testbench-based verification
- Simulation waveform analysis

---

## 🛠️ Algorithm

1. Declare the inputs `D`, `clk`, and `rst`.
2. Declare the outputs `Q` and `Q_bar`.
3. Trigger the sequential block on the positive edge of the clock or negative edge of reset.
4. If `rst = 0`, asynchronously clear `Q` to `0` and `Q_bar` to `1`.
5. Otherwise, on `posedge clk`, assign `Q = D`.
6. Generate the complementary output using `Q_bar = ~D`.
7. Verify the operation using the testbench and simulation waveform.

---

## 📥 Inputs

| Signal | Description |
|--------|-------------|
| `clk` | Clock input |
| `D` | Data input |
| `rst` | Asynchronous reset input |

---

## 📤 Outputs

| Signal | Description |
|--------|-------------|
| `Q` | Main output |
| `Q_bar` | Complementary output |

---

## 💻 Verilog HDL Implementation

### `d_flipflop.v`

```verilog
module dflipflop(q,qbar,d,clk,rst);
output reg q,qbar;
input d,clk,rst;
always @(posedge clk or negedge rst)
begin
if(!rst)begin
q<=0;
qbar<=1;
end
else
begin
q<=d;
qbar<=~d;
end
end
endmodule
```

---

## 🧪 Testbench

### `tb_d_flipflop.v`

```verilog
module dflipflop_tb;
reg d,clk,rst;
wire q,qbar;
dflipflop uut(.q(q),.qbar(qbar),.d(d),.clk(clk),.rst(rst));
always #5 clk = ~clk;
initial begin
clk = 0;
rst = 0;
d = 0;
#10;
rst = 1;
#10;
d = 0;
#10;
d = 1;
#10;
d = 0;
#10;
d = 1;
#10;
d = 1;
#10;
rst = 0;
#10;
rst = 1;
#10;
$finish;
end
initial begin
$monitor("Time=%0t|rst=%b|clk=%b|d=%b|q=%b|qbar=%b",$time,rst,clk,d,q,qbar);
end
endmodule
```

---

## Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/2.D/Image/stimulation_dff.jpeg" width="80%">
</p>

---


## 📊 Truth Table

| D | Q(next) | Q_bar(next) | Operation |
|---|---------|-------------|-----------|
| 0 | 0 | 1 | Reset (transfer 0) |
| 1 | 1 | 0 | Set (transfer 1) |

---
## Implemented Design

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/2.D/Image/implemented_desgin_dff.jpeg" width="80%">
</p>

---

## Project Summary

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Image/project_summary_upcounter.png" width="80%">
</p>
---


## 📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

The simulation waveform should verify that `Q` follows `D` at every positive edge of the clock, with no undefined states.

---

## 🔬 Verification Procedure

1. Create the D Flip-Flop module.
2. Declare `D`, `clk`, and `rst` as inputs.
3. Declare `Q` and `Q_bar` as outputs.
4. Use an `always @(posedge clk or negedge rst)` block.
5. Apply both possible values of `D` (0 and 1).
6. Verify the Reset (transfer 0) condition.
7. Verify the Set (transfer 1) condition.
8. Confirm asynchronous reset behavior.
9. Observe the output using the simulation waveform.

---

## 🛠️ Tools Used

- **Verilog HDL**
- **Xilinx Vivado**
- **ModelSim**
- **Icarus Verilog**
- **EDA Playground**

---

## 📚 Concepts Covered

- Sequential Circuits
- D Flip-Flop
- Data Transfer Operations
- Clocked Circuits
- Behavioral Modeling
- `always` Block
- Positive-Edge Triggering
- Non-Blocking Assignments
- Truth Tables
- Asynchronous Reset
- Testbench Creation
- Simulation
- Waveform Analysis
- Verilog HDL

---

## 🚀 Applications

D Flip-Flops are commonly used in:

- Memory Elements
- Sequential Circuits
- Shift Registers
- Data Latches
- Registers
- Counters
- State Machines
- Digital Control Systems
- Pipeline Stages in Processors

---

## ✅ Result

The **D Flip-Flop** was successfully designed and simulated using **Behavioral Modeling in Verilog HDL**.

The flip-flop correctly performs the following operations at the positive edge of the clock:

```text
D = 0 → Q = 0 (Reset/transfer 0)
D = 1 → Q = 1 (Set/transfer 1)
```

The simulation verifies the correct data transfer operation of the D Flip-Flop, with no invalid states.

---

## 📜 License

This project is intended for **educational and learning purposes**.
