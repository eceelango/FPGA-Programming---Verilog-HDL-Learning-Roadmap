# SR Flip-Flop Using Verilog HDL

## 📌 Overview

This project demonstrates the implementation and simulation of an **SR (Set-Reset) Flip-Flop** using Verilog HDL.

An SR Flip-Flop is a sequential digital circuit capable of storing **one bit of information**. It has two control inputs:

- `S` → Set
- `R` → Reset

The output changes according to the values of `S` and `R` at the **positive edge of the clock**.

The SR Flip-Flop is implemented using **Behavioral Modeling** in Verilog HDL.

---

## 🎯 Aim

To design and simulate an **SR Flip-Flop** using Behavioral Modeling in Verilog HDL.

---

## 🧠 Theory

An SR Flip-Flop is a basic memory element capable of storing a single binary bit.

It has the following signals:

| Signal | Description |
|--------|-------------|
| `S` | Set input |
| `R` | Reset input |
| `clk` | Clock input |
| `Q` | Main output |
| `Q_bar` | Complementary output |

The operation of the SR Flip-Flop is controlled by the clock signal.

The state changes only at the **positive edge (`posedge`)** of the clock.

---

## 🔄 Operation

| S | R | Q(next) | Q_bar(next) | Operation |
|---|---|---------|-------------|-----------|
| 0 | 0 | Q | Q̅ | Hold |
| 0 | 1 | 0 | 1 | Reset |
| 1 | 0 | 1 | 0 | Set |
| 1 | 1 | X | X | Invalid |

Where:

- `Q` represents the previous state.
- `X` represents an unknown/invalid state.

---

## ⚙️ Features

- SR Flip-Flop implementation
- Behavioral modeling using Verilog HDL
- Positive-edge-triggered clock
- Set and Reset functionality
- Stores one bit of data
- Complementary output
- Testbench-based verification
- Simulation waveform analysis

---

## 🛠️ Algorithm

1. Declare the inputs `S`, `R`, and `clk`.
2. Declare the outputs `Q` and `Q_bar`.
3. Trigger the sequential block on the positive edge of the clock.
4. Check the values of `S` and `R`.
5. If `S = 0` and `R = 0`, retain the previous state.
6. If `S = 1` and `R = 0`, set `Q` to `1`.
7. If `S = 0` and `R = 1`, reset `Q` to `0`.
8. If `S = 1` and `R = 1`, assign an invalid/unknown state.
9. Generate the complementary output using `Q_bar = ~Q`.
10. Verify the operation using the testbench and simulation waveform.

---

## 📥 Inputs

| Signal | Description |
|--------|-------------|
| `clk` | Clock input |
| `S` | Set input |
| `R` | Reset input |

---

## 📤 Outputs

| Signal | Description |
|--------|-------------|
| `Q` | Main output |
| `Q_bar` | Complementary output |

---

## Schematic

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/1.%20SR/Image/Schematic.jpeg" width="80%">
</p>

## 💻 Verilog HDL Implementation

### `sr_flipflop.v`

```verilog
module srflipflop(q,qbar,s,r,clk,rst);
output reg q,qbar;
input s,r,clk,rst;
always @(posedge clk or negedge rst)
begin
    if(!rst)begin
        q<=0;
        qbar<=1;
    end 
    else
    begin
        case ({s,r})
            2'b00: begin
                q<=q;
                qbar<=qbar;
            end
            2'b01: begin
                q<=0;
                qbar<=1;
            end
          2'b10: begin
                q<= 1;
                qbar<=0;
         end
        2'b11: begin
            q<= 1'bx;
            qbar<= 1'bx;
        end 
    endcase
end 
end
endmodule
```

---

## 🧪 Testbench

### `tb_sr_flipflop.v`

```verilog
module srflipflop_tb;
reg s,r,clk,rst;
wire q,qbar;
srflipflop uut (.q(q),.qbar(qbar),.s(s),.r(r),.clk(clk),.rst(rst));
always #5 clk = ~clk;
initial begin
    clk=0;
    rst=0;
    s=0;r=0;
    #10;
    rst=1;
    #10;
    s=0;r=0;
    #10;
    s=1;r=0;
    #10;
    s=0;r=0;
    #10;
    s=0;r=1;
    #10;
    s=0;r=0;
    #10;
    s=1;r=1;
    #10;
    rst=0;
    #10;
    $finish;
end
initial begin
$monitor("Time=%0t|rst=%b|clk=%b|s=%b|r=%b|q=%b|qbar=%b",$time,rst,clk,s,r,q,qbar);
end
endmodule
```

---

## Waveform

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/1.%20SR/Image/Simulation.jpeg" width="80%">
</p>

---

## 🏗️ Block Diagram

<p align="center">
<img src="https://github.com/eceelango/FPGA-Programming---Verilog-HDL-Learning-Roadmap/blob/main/Sequential%20circuit/1.%20Flip%20Flop/1.%20SR/Image/Block%20Diagram.jpeg" width="80%">
</p>

The state changes only when a **positive edge of the clock** occurs.

---



## 📊 Truth Table

| S | R | Q(next) | Q_bar(next) | Operation |
|---|---|---------|-------------|-----------|
| 0 | 0 | Q | Q̅ | Hold |
| 0 | 1 | 0 | 1 | Reset |
| 1 | 0 | 1 | 0 | Set |
| 1 | 1 | X | X | Invalid |

---

## 🧪 Simulation Verification

The testbench verifies all four possible combinations of the `S` and `R` inputs.

### Hold

```text
S = 0
R = 0
```

The previous state is retained.

### Set

```text
S = 1
R = 0
```

The output becomes:

```text
Q = 1
Q_bar = 0
```

### Reset

```text
S = 0
R = 1
```

The output becomes:

```text
Q = 0
Q_bar = 1
```

### Invalid

```text
S = 1
R = 1
```

The output becomes:

```text
Q = X
Q_bar = X
```

---

## 📊 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

The simulation waveform should verify that the output changes according to the SR Flip-Flop truth table at every positive edge of the clock.

---

## 📂 Project Structure

```text
SR-Flip-Flop/
│
├── sr_flipflop.v
├── tb_sr_flipflop.v
└── README.md
```

---

## 🔬 Verification Procedure

1. Create the SR Flip-Flop module.
2. Declare `S`, `R`, and `clk` as inputs.
3. Declare `Q` and `Q_bar` as outputs.
4. Use an `always @(posedge clk)` block.
5. Apply the four possible combinations of `S` and `R`.
6. Verify the Hold condition.
7. Verify the Set condition.
8. Verify the Reset condition.
9. Verify the Invalid condition.
10. Observe the output using the simulation waveform.

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
- SR Flip-Flop
- Set and Reset Operations
- Clocked Circuits
- Behavioral Modeling
- `always` Block
- Positive-Edge Triggering
- Non-Blocking Assignments
- Truth Tables
- Invalid States
- Testbench Creation
- Simulation
- Waveform Analysis
- Verilog HDL

---

## 🚀 Applications

SR Flip-Flops are commonly used in:

- Memory Elements
- Sequential Circuits
- Control Circuits
- Switch Debouncing
- Registers
- Counters
- State Machines
- Digital Control Systems
- Data Storage Circuits

---

## ✅ Result

The **SR Flip-Flop** was successfully designed and simulated using **Behavioral Modeling in Verilog HDL**.

The flip-flop correctly performs the following operations at the positive edge of the clock:

```text
S = 0, R = 0 → Hold
S = 0, R = 1 → Reset
S = 1, R = 0 → Set
S = 1, R = 1 → Invalid
```

The simulation verifies the correct Set, Reset, Hold, and Invalid operations of the SR Flip-Flop.

---

## 📜 License

This project is intended for **educational and learning purposes**.
