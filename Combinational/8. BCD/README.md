# 4-Bit BCD Adder Using Verilog HDL

## 📌 Overview

This project demonstrates the implementation and simulation of a **4-Bit BCD Adder** using Verilog HDL.

A **BCD (Binary Coded Decimal) Adder** is a combinational digital circuit used to add two 4-bit BCD digits.

In BCD representation, each decimal digit is represented using four binary bits. Only the combinations from `0000` to `1001` are valid BCD codes, representing decimal digits `0` to `9`.

When the binary addition produces a result greater than `9`, the result is not a valid BCD digit. In this case, `0110` (decimal 6) is added to correct the result.

---

## 🎯 Aim

To design and simulate a **4-bit BCD Adder** using Verilog HDL.

---

## 🧠 Theory

BCD stands for **Binary Coded Decimal**.

Each decimal digit is represented separately using four binary bits.

### BCD Representation

| Decimal | BCD |
|---------|-----|
| 0 | `0000` |
| 1 | `0001` |
| 2 | `0010` |
| 3 | `0011` |
| 4 | `0100` |
| 5 | `0101` |
| 6 | `0110` |
| 7 | `0111` |
| 8 | `1000` |
| 9 | `1001` |

The BCD codes from:

```text
1010 to 1111
```

are invalid because a single BCD digit can represent only decimal values from `0` to `9`.

---

## ➕ BCD Addition

BCD addition is performed in two main stages:

1. Add the two 4-bit BCD numbers as ordinary binary numbers.
2. Check whether the intermediate result requires BCD correction.
3. If correction is required, add `0110`.
4. The lower four bits become the valid BCD result.
5. The correction carry becomes the decimal carry output.

### Correction Condition

BCD correction is required when:

```text
Binary Sum > 1001
```

or when the binary addition generates a carry.

The correction condition is:

```text
Correction = Carry | (S3 & S2) | (S3 & S1)
```

where:

- `S3` = Most significant bit of the intermediate sum
- `S2` = Second most significant bit
- `S1` = Second least significant bit

When correction is required:

```text
Corrected Sum = Intermediate Sum + 0110
```
## Schematic

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/8.%20BCD/Image/Schematic.jpeg" width="80%">
</p>

---

## ⚙️ Features

- 4-bit BCD addition
- Combinational circuit
- No clock required
- Detects invalid BCD results
- Automatic BCD correction
- Adds `0110` when correction is required
- Generates decimal carry
- Verilog HDL implementation
- Testbench-based verification
- Simulation waveform analysis

---

## 🛠️ Algorithm

1. Declare two 4-bit BCD inputs `A` and `B`.
2. Add `A` and `B` using binary addition.
3. Store the intermediate sum and carry.
4. Check whether the intermediate result is greater than `9` or a carry is generated.
5. If correction is required, add `0110`.
6. Generate the corrected BCD output.
7. Generate the decimal carry output.
8. Apply different valid BCD input combinations.
9. Observe the output using simulation waveforms.
10. Verify the results with the expected BCD addition.

---

## 📥 Inputs

| Signal | Description |
|--------|-------------|
| `A[3:0]` | First 4-bit BCD digit |
| `B[3:0]` | Second 4-bit BCD digit |

---

## 📤 Outputs

| Signal | Description |
|--------|-------------|
| `sum[3:0]` | Corrected 4-bit BCD result |
| `carry` | Decimal carry output |

---

## Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/8.%20BCD/Image/Stimulation.jpeg" width="80%">
</p>

## 💻 Verilog HDL Implementation

### `bcd_adder.v`

```verilog
`timescale 1ns / 1ps
module bcd_adder(S,Cout,A,B,Cin);
input [3:0]A,B;
input Cin;
output [3:0]S;
output Cout;
wire c0,c1,c2,c3,c4,c5,c6,s0,s1,s2,s3,b;
fa fa0(s0,c0,A[0],B[0],Cin);
fa fa1(s1,c1,A[1],B[1],c0);
fa fa2(s2,c2,A[2],B[2],c1);
fa fa3(s3,c3,A[3],B[3],c2);
assign b = s3 & (s2|s1) | c3;
fa fa4(S[0],c4,s0,0,0);
fa fa5(S[1],c5,s1,b,c4);
fa fa6(S[2],c6,s2,b,c5);
fa fa7(S[3],Cout,s3,0,c6);
endmodule
module fa(S,Cout,A,B,Cin);
input A,B,Cin;
output S,Cout;
xor(S,A,B,Cin);
or(Cout,A&B,Cin&(A^B));
endmodule
```

---

## 🧪 Testbench

### `tb_bcd_adder.v`

```verilog
`timescale 1ns / 1ps
    module tb_bcd_adder;
    reg [3:0] A,B;
    reg Cin;
    wire [3:0]S;
    wire Cout;
    bcd_adder uut(
    .S(S),
    .Cout(Cout),
    .A(A),
    .B(B),
    .Cin(Cin)
    );
    initial
    begin
    $monitor("Time = %0t | A=%d B=%d Cin = %b | S = %b Cout = %b",
    $time, A,B,Cin,S,Cout);
    A=4'd0 ; B=4'd9; Cin =0;
    #10;
    A=4'd5 ; B=4'd3; Cin =0;
    #10;
    A=4'd9 ; B=4'd10; Cin =0;
    #10;
    A=4'd5 ; B=4'd5; Cin =0;
    #10;
    A=4'd9 ; B=4'd5; Cin =0;
    #10;
    A=4'd15 ; B=4'd3; Cin =0;
    #10;
    A=4'd8 ; B=4'd9; Cin =0;
    #10;
    A=4'd5 ; B=4'd5; Cin =1;
    #10;
    A=4'd10 ; B=4'd8; Cin =1;
    #10;
    $finish;
    end
    endmodule
```

---

## 🏗️ Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Combinational/8.%20BCD/Image/Block%20Diagram.jpeg" width="80%">
</p>

---

## 🧮 BCD Correction Logic

The correction signal is generated using:

```text
Correction = Carry | (S3 & S2) | (S3 & S1)
```

Correction occurs when:

- The first addition produces a carry, or
- The intermediate sum is greater than 9.

### If `Correction = 1`

```text
Corrected Sum = Intermediate Sum + 0110
```

### If `Correction = 0`

```text
Corrected Sum = Intermediate Sum
```

---

## 📊 BCD Addition Table

| A | B | Decimal Operation | Binary Sum | Correction | Carry | BCD Result |
|---|---|-------------------|------------|------------|-------|------------|
| `0000` | `0000` | 0 + 0 | `00000` | No | 0 | `0000` |
| `0010` | `0011` | 2 + 3 | `00101` | No | 0 | `0101` |
| `0100` | `0101` | 4 + 5 | `01001` | No | 0 | `1001` |
| `0101` | `0101` | 5 + 5 | `01010` | + `0110` | 1 | `0000` |
| `0111` | `1000` | 7 + 8 | `01111` | + `0110` | 1 | `0101` |
| `1001` | `1001` | 9 + 9 | `10010` | + `0110` | 1 | `1000` |

---

## 🌊 Expected Simulation Output

The simulation waveform verifies both normal BCD addition and BCD correction.

Expected output:

```text
A       B       Carry    Sum
--------------------------------
0010    0011      0      0101
0100    0101      0      1001
0101    0101      1      0000
0111    1000      1      0101
1001    1001      1      1000
```

---

## 📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

The waveform should verify that:

- Valid BCD sums from `0` to `9` require no correction.
- Results greater than `9` require the addition of `0110`.
- The `carry` output indicates the decimal carry.
- The final `sum[3:0]` remains a valid BCD digit.

---

## 📂 Project Structure

```text
4-Bit-BCD-Adder/
│
├── bcd_adder.v
├── tb_bcd_adder.v
└── README.md
```

---

## 🔬 Verification Procedure

1. Declare two 4-bit BCD inputs.
2. Perform binary addition of the two inputs.
3. Detect whether BCD correction is required.
4. Add `0110` when correction is required.
5. Generate the corrected BCD sum.
6. Generate the decimal carry.
7. Apply different valid BCD input combinations.
8. Observe the simulation output.
9. Compare the results with the expected decimal values.
10. Verify the simulation waveform.

---

## 🛠️ Tools Used

- **Verilog HDL**
- **Xilinx Vivado**
- **ModelSim**
- **Icarus Verilog**
- **EDA Playground**

---

## 📚 Concepts Covered

- BCD Representation
- BCD Addition
- Binary Addition
- BCD Correction
- Correction Value `0110`
- Combinational Circuits
- Carry Generation
- Boolean Logic
- Verilog HDL
- Continuous Assignment
- Testbench Creation
- Functional Verification
- Simulation
- Waveform Analysis
- FPGA Implementation

---

## 🚀 Applications

BCD Adders are commonly used in:

- Digital Clocks
- Digital Calculators
- Seven-Segment Display Systems
- Digital Meters
- Electronic Counters
- ALUs
- Financial and Commercial Systems
- Decimal Arithmetic Circuits
- Embedded Systems
- FPGA-Based Digital Systems

---

## ✅ Result

The **4-Bit BCD Adder** was successfully designed and simulated using Verilog HDL.

The circuit correctly adds two valid 4-bit BCD digits and automatically performs BCD correction whenever the binary result exceeds decimal `9`.

The correction value `0110` is added whenever required, producing a valid BCD result and decimal carry.

---

## 📜 License

This project is intended for **educational and learning purposes**.
