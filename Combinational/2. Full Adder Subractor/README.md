# 4-Bit Adder/Subtractor Using Verilog HDL

## 📌 Overview

This project implements a **4-bit Adder/Subtractor** using Verilog HDL.

The circuit can perform both addition and subtraction of two 4-bit binary numbers. The operation is selected using the `Cin` control input.

- `Cin = 0` → Addition
- `Cin = 1` → Subtraction

The circuit is implemented using **four 1-bit Full Adders** connected in a ripple-carry configuration. Subtraction is performed using the **2's complement method**.

---

## 🎯 Aim

To design and simulate a **4-bit Adder/Subtractor combinational circuit** using Verilog HDL and verify its operation for both addition and subtraction.

---

## 🧠 Theory

A 4-bit Adder/Subtractor is a combinational circuit that performs arithmetic operations on two 4-bit binary inputs.

### Inputs

| Signal | Description |
|--------|-------------|
| `A[3:0]` | First 4-bit operand |
| `B[3:0]` | Second 4-bit operand |
| `Cin` | Operation control / initial carry input |

### Outputs

| Signal | Description |
|--------|-------------|
| `S[3:0]` | 4-bit sum or difference |
| `Cout` | Final carry output |

---

## 🔄 Operation

| `Cin` | Operation | Function |
|------|-----------|----------|
| `0` | Addition | `A + B` |
| `1` | Subtraction | `A - B` |


## 🏗️ Block Diagram
<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/2.%20Full%20Adder%20Subractor/Image/4%20Bit%20Adder%20Subractor%20Block%20Diagram.png" width="80%">
</p>

---

## 💻 Verilog HDL Code

### `adder_subractor.v`

```verilog
`timescale 1ns / 1ps

module adder_subractor(S,Cout,A,B,Cin);

input [3:0] A,B;
input Cin;

output [3:0] S;
output Cout;

wire c1,c2,c3;

fa FA0(S[0],c1,A[0],(Cin ^ B[0]),Cin);
fa FA1(S[1],c2,A[1],(Cin ^ B[1]),c1);
fa FA2(S[2],c3,A[2],(Cin ^ B[2]),c2);
fa FA3(S[3],Cout,A[3],(Cin ^ B[3]),c3);

endmodule
```

### Full Adder

```verilog
module fa(S,Cout,A,B,Cin);

output S,Cout;
input A,B,Cin;

assign S = A^B^Cin;

assign Cout = (A&B)|(A^B)&Cin;

endmodule
```

---

## 🧪 Testbench

### `tb_adder_subractor.v`

```verilog
`timescale 1ns / 1ps

module tb_adder_subractor;

reg [3:0] A,B;
reg Cin;

wire [3:0] S;
wire Cout;

adder_subractor uut(
    .S(S),
    .Cout(Cout),
    .A(A),
    .B(B),
    .Cin(Cin)
);

initial begin

    $monitor(
        "Time=%0t | A=%d B=%d Cin=%b | S=%d Cout=%b",
        $time, A, B, Cin, S, Cout
    );

    A=4'd0;
    B=4'd1;
    Cin=1'b0;
    #10;

    A=4'd5;
    B=4'd9;
    Cin=1'b0;
    #10;

    A=4'd3;
    B=4'd7;
    Cin=1'b0;
    #10;

    A=4'd2;
    B=4'd9;
    Cin=1'b0;
    #10;

    A=4'd10;
    B=4'd4;
    Cin=1'b0;
    #10;

    A=4'd12;
    B=4'd8;
    Cin=1'b1;
    #10;

    A=4'd5;
    B=4'd3;
    Cin=1'b1;
    #10;

    A=4'd7;
    B=4'd2;
    Cin=1'b1;
    #10;

    A=4'd9;
    B=4'd2;
    Cin=1'b1;
    #10;

    A=4'd15;
    B=4'd0;
    Cin=1'b1;
    #10;

    $finish;

end

endmodule
```

---

## 📊 Test Cases

### Addition

| A | B | Cin | Operation | Result | Cout |
|---|---|---|---|---|---|
| `0000` | `0001` | 0 | 0 + 1 | `0001` | 0 |
| `0101` | `1001` | 0 | 5 + 9 | `1110` | 0 |
| `0011` | `0111` | 0 | 3 + 7 | `1010` | 0 |
| `0010` | `1001` | 0 | 2 + 9 | `1011` | 0 |
| `1010` | `0100` | 0 | 10 + 4 | `1110` | 0 |

### Subtraction

| A | B | Cin | Operation | Result | Cout |
|---|---|---|---|---|---|
| `1100` | `1000` | 1 | 12 - 8 | `0100` | 1 |
| `0101` | `0011` | 1 | 5 - 3 | `0010` | 1 |
| `0111` | `0010` | 1 | 7 - 2 | `0101` | 1 |
| `1001` | `0010` | 1 | 9 - 2 | `0111` | 1 |
| `1111` | `0000` | 1 | 15 - 0 | `1111` | 1 |

---

## 🌊 Expected Simulation Output

The testbench uses `$monitor` to display the input and output values during simulation.

```text
Time=0  | A= 0| B= 1 Cin=0 | S= 1 Cout=0
Time=10 | A= 5 B= 9 Cin=0 | S=14 Cout=0
Time=20 | A= 3 B= 7 Cin=0 | S=10 Cout=0
Time=30 | A= 2 B= 9 Cin=0 | S=11 Cout=0
Time=40 | A=10 B= 4 Cin=0 | S=14 Cout=0
Time=50 | A=12 B= 8 Cin=1 | S= 4 Cout=1
Time=60 | A= 5 B= 3 Cin=1 | S= 2 Cout=1
Time=70 | A= 7 B= 2 Cin=1 | S= 5 Cout=1
Time=80 | A= 9 B= 2 Cin=1 | S= 7 Cout=1
Time=90 | A=15 B= 0 Cin=1 | S=15 Cout=1
```

---

## 🛠️ Tools

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

---

## 📂 Project Structure

```text
4-Bit-Adder-Subractor/
│
├── adder_subractor.v
├── tb_adder_subractor.v
└── README.md
```

---

## 📚 Concepts Covered

- Combinational Logic
- Binary Addition
- Binary Subtraction
- Full Adder
- Ripple Carry Adder
- XOR Gates
- 2's Complement
- Carry Generation
- Borrow Detection
- Verilog HDL
- Module Instantiation
- Continuous Assignment
- Hierarchical Design
- Testbench Development
- `$monitor`
- Simulation
- Waveform Verification

---

## 🚀 Applications

Adder/Subtractor circuits are commonly used in:

- Arithmetic Logic Units (ALUs)
- CPUs
- Microprocessors
- Microcontrollers
- Digital Calculators
- FPGA-based Systems
- Embedded Systems
- Digital Signal Processing
- Computer Arithmetic Units
- Processor Datapaths
- Control Systems

---

## ✅ Result

The **4-bit Adder/Subtractor** was successfully designed and simulated using Verilog HDL.

The circuit performs:

```text
Cin = 0 → A + B
Cin = 1 → A - B
```

Subtraction is implemented using the **2's complement method** by XORing each bit of `B` with `Cin` and using `Cin` as the initial carry input.

The simulation results verify the correct operation of the circuit for both addition and subtraction.

---

## 📜 License

This project is intended for educational and learning purposes.
