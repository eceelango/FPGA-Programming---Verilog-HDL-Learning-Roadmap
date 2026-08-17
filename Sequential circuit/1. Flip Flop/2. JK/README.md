# JK Flip-Flop Using Verilog HDL

## 📌 Overview

This project demonstrates the design and simulation of a **JK Flip-Flop using Verilog HDL**.

A JK Flip-Flop is a sequential digital circuit capable of storing **one bit of information**. It is an improved version of the SR Flip-Flop because it eliminates the invalid condition associated with the SR Flip-Flop.

The JK Flip-Flop has two control inputs:

* **J** → Set input
* **K** → Reset input

The output changes according to the values of `J` and `K` at the **active edge of the clock signal**.

This project implements a **positive-edge-triggered JK Flip-Flop using Behavioral Modeling in Verilog HDL**.

---

## 🎯 Aim

To design and simulate a **JK Flip-Flop using Behavioral Modeling in Verilog HDL** and verify its operation using a testbench and simulation waveform.

---

## 📖 Theory

A JK Flip-Flop is a clocked sequential circuit that stores a single bit of data.

### Inputs

* **J** → Set input
* **K** → Reset input
* **CLK** → Clock input

### Outputs

* **Q** → Main output
* **Q_bar** → Complementary output

The output changes only when the **positive edge of the clock** occurs.

### JK Flip-Flop Operations

| J | K | Q(next) | Operation |
| - | - | ------- | --------- |
| 0 | 0 | Q       | Hold      |
| 0 | 1 | 0       | Reset     |
| 1 | 0 | 1       | Set       |
| 1 | 1 | Q̅      | Toggle    |

Unlike the SR Flip-Flop, the condition **J = 1, K = 1** is valid and causes the output to toggle.

---

## ⚙️ Features

* JK Flip-Flop implementation
* Behavioral modeling using Verilog HDL
* Positive-edge-triggered operation
* Set and Reset functionality
* Toggle operation
* Hold operation
* Single-bit data storage
* Complementary output
* Testbench-based verification
* Simulation waveform analysis

---

## 🧠 JK Flip-Flop Characteristic Equation

The characteristic equation of a JK Flip-Flop is:

```text
Q(next) = JQ̅ + K̅Q
```

This equation represents all four operating conditions of the JK Flip-Flop.

---

## 🔄 Truth Table

| J | K | Q(next) | Q_bar(next) | Operation |
| - | - | ------- | ----------- | --------- |
| 0 | 0 | Q       | Q̅          | Hold      |
| 0 | 1 | 0       | 1           | Reset     |
| 1 | 0 | 1       | 0           | Set       |
| 1 | 1 | Q̅      | Q           | Toggle    |

---

## 🛠️ Algorithm

1. Declare the inputs `J`, `K`, and `clk`.
2. Declare the outputs `Q` and `Q_bar`.
3. Trigger the sequential block on the positive edge of `clk`.
4. Check the values of `J` and `K`.
5. If `J = 0` and `K = 0`, retain the previous state.
6. If `J = 0` and `K = 1`, reset `Q` to `0`.
7. If `J = 1` and `K = 0`, set `Q` to `1`.
8. If `J = 1` and `K = 1`, toggle the current state of `Q`.
9. Generate `Q_bar` as the complement of `Q`.
10. Verify the operation using simulation waveforms.

---

## 📥 Inputs

| Signal | Description                   |
| ------ | ----------------------------- |
| `clk`  | Positive-edge-triggered clock |
| `J`    | Set input                     |
| `K`    | Reset input                   |

---

## 📤 Outputs

| Signal  | Description          |
| ------- | -------------------- |
| `Q`     | Main output          |
| `Q_bar` | Complementary output |

---

# 💻 Verilog HDL Code

```verilog
module jkflipflop (q,qbar,j,k,clk,rst);
output reg q,qbar;
input j,k,clk,rst;
always @(posedge clk or negedge rst)
begin
if (!rst) begin
q<=0;
qbar<=1;
end
else
begin
case ({j,k})
2'b00 :begin
q<=q;
qbar<=qbar;
end 
2'b01:begin
q<=0;
qbar<=1;
end 
2'b10:begin
q<=1;
qbar<=0;
end 
2'b11:begin
q<=qbar;
qbar<=q;
end
endcase
end
end
endmodule
```

---

# 🧪 Testbench

The following testbench verifies all four operating conditions of the JK Flip-Flop:

* Set
* Hold
* Reset
* Toggle

```verilog
module jkflipflop_tb;
reg j,k,clk,rst;
wire q,qbar;
jkflipflop uut(.q(q),.qbar(qbar),.j(j),.k(k),.clk(clk),.rst(rst));
always #5 clk =~clk;
initial begin
clk=0;
rst=0;
j=0;
k=0;
#10;
rst=1;
#10;
j=0;
k=0;
#10;
j=0;
k=1;
#10;
j=1;
k=0;
#10;
j=1;
k=1;
#10;
j=1;
k=1;
#10;
rst=0;
#10;
rst=1;
#10;
$finish;
end
initial begin
$monitor("Time=%0t | rst=%b | clk=%b | j=%b | k=%b | q=%b | qbar=%b",$time,rst,clk,j,k,q,qbar);
end
endmodule
```

---

## 🌊 Expected Simulation Behavior

The simulation waveform should verify the following operations at every positive edge of the clock:

```text
J = 0, K = 0  →  HOLD
J = 0, K = 1  →  RESET
J = 1, K = 0  →  SET
J = 1, K = 1  →  TOGGLE
```

---

## 🏗️ Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/2.%20JK/Image/Block%20Diagram.jpeg" width="80%">
</p>

---

### Operations

```text
J = 0, K = 0  →  HOLD

J = 0, K = 1  →  RESET

J = 1, K = 0  →  SET

J = 1, K = 1  →  TOGGLE
```

---

## 📊 Simulation

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/2.%20JK/Image/Simulation.jpeg" width="80%">
</p>

---

## Schematic

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/2.%20JK/Image/Schematic.jpeg" width="80%">
</p>

---

## ✅ Result

The **JK Flip-Flop was successfully designed and simulated using Behavioral Modeling in Verilog HDL**.

The simulation verifies all four operating conditions:

| J | K | Result |
| - | - | ------ |
| 0 | 0 | Hold   |
| 0 | 1 | Reset  |
| 1 | 0 | Set    |
| 1 | 1 | Toggle |

The output changes according to the JK Flip-Flop truth table at every **positive edge of the clock**.

---

## 🚀 Applications

JK Flip-Flops are commonly used in:

* Digital counters
* Frequency dividers
* Registers
* Sequential circuits
* Finite State Machines (FSMs)
* Digital control systems
* Memory elements
* Timing circuits
* Digital clocks
* Computer architecture

---

## 📚 Concepts Covered

This project covers the following concepts:

* Sequential circuits
* JK Flip-Flop
* Set and Reset operations
* Toggle operation
* Hold operation
* Clocked circuits
* Behavioral modeling
* `always` block
* Positive-edge triggering
* Non-blocking assignments
* `case` statement
* Truth tables
* Characteristic equation
* Testbench creation
* Simulation
* Waveform analysis
* Verilog HDL

---

## 📁 Project Structure

A recommended project structure is:

```text
JK-Flip-Flop-Verilog/
│
├── jk_flipflop.v
├── tb_jk_flipflop.v
└── README.md
```

### File Description

| File               | Description                           |
| ------------------ | ------------------------------------- |
| `jk_flipflop.v`    | JK Flip-Flop design module            |
| `tb_jk_flipflop.v` | Testbench for functional verification |
| `README.md`        | Project documentation                 |

---



The design uses **behavioral modeling**, where the desired sequential behavior is described using an `always @(posedge clk)` block.

The `case` statement determines the next state based on the combined `{J, K}` input.

---

## 📜 License

This project is intended for **educational and learning purposes**.

Feel free to use, modify, and improve the project for academic and personal learning.
