# 2-Bit Comparator Using Verilog HDL

## 📌 Overview

This project demonstrates the design and simulation of a **2-Bit Magnitude Comparator using Verilog HDL**.

A magnitude comparator is a **combinational digital circuit** used to compare two binary numbers and determine their relative magnitudes.

In this project, two 2-bit binary numbers, `A` and `B`, are compared.

The circuit produces three outputs:

* **A_greater_B** → A is greater than B
* **A_equal_B** → A is equal to B
* **A_less_B** → A is less than B

Since the comparator is a **combinational circuit**, its outputs depend only on the present input values and do not require a clock signal.

---

## 🎯 Aim

To design and simulate a **2-bit magnitude comparator using Verilog HDL** and verify its operation using a testbench and simulation waveform.

---

## 📖 Theory

A magnitude comparator compares two binary numbers and determines whether one number is:

* Greater than the other
* Equal to the other
* Less than the other

For a 2-bit comparator:

```text
A = A1 A0
B = B1 B0
```

The **Most Significant Bits (MSBs)** are compared first.

The comparison follows three possible conditions:

```text
A > B
A = B
A < B
```

For every valid combination of inputs, **only one of the three outputs is HIGH**.

### Comparison Conditions

#### A > B

`A` is greater than `B` when:

```text
A1 > B1
```

or, when the MSBs are equal:

```text
A1 = B1 AND A0 > B0
```

#### A < B

`A` is less than `B` when:

```text
A1 < B1
```

or, when the MSBs are equal:

```text
A1 = B1 AND A0 < B0
```

#### A = B

`A` is equal to `B` when:

```text
A1 = B1 AND A0 = B0
```

---

## ⚙️ Features

* 2-bit magnitude comparison
* Combinational circuit
* No clock required
* Three comparison outputs
* Greater-than detection
* Equal-to detection
* Less-than detection
* Verilog HDL implementation
* Complete truth table
* Testbench-based verification
* Simulation waveform analysis

---

## 🛠️ Algorithm

1. Declare two 2-bit inputs `A` and `B`.
2. Declare three outputs for greater-than, equal-to, and less-than conditions.
3. Compare the two binary numbers.
4. Generate `A_greater_B` when `A > B`.
5. Generate `A_equal_B` when `A = B`.
6. Generate `A_less_B` when `A < B`.
7. Apply different combinations of the inputs.
8. Observe the outputs using simulation waveforms.
9. Verify the results against the expected truth table.

---

## 📥 Inputs

| Signal   | Description                |
| -------- | -------------------------- |
| `A[1:0]` | First 2-bit binary number  |
| `B[1:0]` | Second 2-bit binary number |

---

## 📤 Outputs

| Signal        | Description     |
| ------------- | --------------- |
| `A_greater_B` | HIGH when A > B |
| `A_equal_B`   | HIGH when A = B |
| `A_less_B`    | HIGH when A < B |

---

# 💻 Verilog HDL Code

```verilog
`timescale 1ns / 1ps
module comparator(
input wire[1:0]A,
input wire[1:0]B,
output reg A_greater,
output reg A_eq_B,
output reg A_less
);
always @ (*) begin
if(A>B) begin
A_greater = 1'b1;
A_eq_B =1'b0;
A_less =1'b0;
end
else if (A==B) begin
A_eq_B =1'b1;
A_greater =1'b0;
A_less =1'b0;
end
else begin 
A_less=1'b1;
A_greater =1'b0;
A_eq_B =1'b0;
end
end
endmodule
```

---

# 🧪 Testbench

The following testbench verifies different combinations of the two 2-bit inputs.

```verilog
`timescale 1ns / 1ps
module comparator_tb;
reg[1:0]A;
reg[1:0]B;
wire A_greater;
wire A_eq_B;
wire A_less;
comparator DUT(
.A(A),
.B(B),
.A_greater(A_greater),
.A_eq_B(A_eq_B),
.A_less(A_less)
);
initial begin
$monitor($time, "A[1]=%b,A[0]=%b,B[1]=%b,B[0]=%b,A>B=%b,A=B=%b,A<B=%b",A[1],A[0],B[1],B[0],A_greater,A_eq_B,A_less
);
      #0 A=2'b00; B=2'b00;
      #10 A=2'b00; B=2'b01;
      #20 A=2'b00; B=2'b10;
      #30 A=2'b00; B=2'b11;
      #40 A=2'b01; B=2'b00;
      #50 A=2'b01; B=2'b01;
      #60 A=2'b01; B=2'b10;
      #70 A=2'b01; B=2'b11;
      #80 A=2'b10; B=2'b00;
      #90 A=2'b10; B=2'b01;
      #100 A=2'b10; B=2'b10;
      #110 A=2'b10; B=2'b11;
      #120 A=2'b11; B=2'b00;
      #130 A=2'b11; B=2'b01;
      #140 A=2'b11; B=2'b10;
      #150 A=2'b11; B=2'b11;
$finish;
end 
endmodule

```

---

## 🌊 Expected Simulation Behavior

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/6.%20Comparator/Image/Simulation.jpeg" width="80%">
</p>

---

## Schematic

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/6.%20Comparator/Image/Schematic.jpeg" width="80%">
</p>

---

# 🔄 Truth Table

| A  | B  | A > B | A = B | A < B |
| -- | -- | :---: | :---: | :---: |
| 00 | 00 |   0   |   1   |   0   |
| 00 | 01 |   0   |   0   |   1   |
| 00 | 10 |   0   |   0   |   1   |
| 00 | 11 |   0   |   0   |   1   |
| 01 | 00 |   1   |   0   |   0   |
| 01 | 01 |   0   |   1   |   0   |
| 01 | 10 |   0   |   0   |   1   |
| 01 | 11 |   0   |   0   |   1   |
| 10 | 00 |   1   |   0   |   0   |
| 10 | 01 |   1   |   0   |   0   |
| 10 | 10 |   0   |   1   |   0   |
| 10 | 11 |   0   |   0   |   1   |
| 11 | 00 |   1   |   0   |   0   |
| 11 | 01 |   1   |   0   |   0   |
| 11 | 10 |   1   |   0   |   0   |
| 11 | 11 |   0   |   1   |   0   |

---

# 🏗️ Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/6.%20Comparator/Image/Block%20Diagram.jpeg" width="80%">
</p>


The comparator accepts two 2-bit binary numbers and generates three **mutually exclusive outputs**.

---

## 🔍 Working Principle

The comparator determines the relationship between `A` and `B` using their binary values.

For example:

```text
A = 11
B = 01
```

The decimal values are:

```text
A = 3
B = 1
```

Therefore:

```text
A > B
```

and the output becomes:

```text
A_greater_B = 1
A_equal_B   = 0
A_less_B    = 0
```

The Verilog relational operators perform these comparisons directly:

```verilog
A > B
A == B
A < B
```

Because the circuit is combinational, the outputs update whenever the inputs change.

---

## 🧩 Why No Clock Is Required

A magnitude comparator is a **combinational circuit**.

Unlike sequential circuits such as flip-flops and counters, it does not store previous input values.

Therefore:

```text
Current Inputs → Combinational Logic → Current Outputs
```

There is no requirement for:

* Clock
* Reset
* Memory
* Previous state

---

## 📊 Simulation

The design can be simulated using:

* **Xilinx Vivado**
* **ModelSim**
* **Icarus Verilog**
* **EDA Playground**

The testbench applies different combinations of `A` and `B` and verifies the three comparison outputs.

---

## ✅ Result

The **2-Bit Magnitude Comparator was successfully designed and simulated using Verilog HDL**.

The circuit correctly compares two 2-bit binary numbers and generates the appropriate output for:

```text
A > B
A = B
A < B
```

The simulation results match the expected truth table for all possible input combinations.

---

## 🚀 Applications

Magnitude comparators are commonly used in:

* Arithmetic Logic Units (ALUs)
* Digital processors
* Microprocessors
* Microcontrollers
* Control systems
* Address comparison
* Digital sorting circuits
* Data processing systems
* FPGA-based digital systems
* Decision-making circuits

---

## 📚 Concepts Covered

This project covers:

* Combinational circuits
* Binary comparison
* Magnitude comparator
* Greater-than comparison
* Equal-to comparison
* Less-than comparison
* Relational operators
* Continuous assignment
* Verilog HDL
* Testbench creation
* Truth table verification
* Simulation
* Waveform analysis
* FPGA implementation

---

## 📁 Project Structure

A recommended project structure is:

```text
2-Bit-Comparator-Verilog/
│
├── comparator_2bit.v
├── tb_comparator_2bit.v
└── README.md
```


## 📜 License

This project is intended for **educational and learning purposes**.

Feel free to use, modify, and improve the project for academic and personal learning.
