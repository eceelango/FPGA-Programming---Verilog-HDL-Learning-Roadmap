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

## 💻 Verilog HDL Implementation

### `sr_flipflop.v`

```verilog
`timescale 1ns / 1ps

module sr_flipflop(
    input clk,
    input S,
    input R,
    output reg Q,
    output Q_bar
);

always @(posedge clk)
begin
    case ({S, R})

        2'b00: Q <= Q;
        2'b01: Q <= 1'b0;
        2'b10: Q <= 1'b1;
        2'b11: Q <= 1'bx;

    endcase
end

assign Q_bar = ~Q;

endmodule
```

---

## 🧪 Testbench

### `tb_sr_flipflop.v`

```verilog
`timescale 1ns / 1ps

module tb_sr_flipflop;

reg clk;
reg S;
reg R;

wire Q;
wire Q_bar;

sr_flipflop uut(
    .clk(clk),
    .S(S),
    .R(R),
    .Q(Q),
    .Q_bar(Q_bar)
);

initial
begin
    clk = 0;
    forever #10 clk = ~clk;
end

initial
begin

    // Hold
    S = 0;
    R = 0;
    #20;

    // Set
    S = 1;
    R = 0;
    #20;

    // Hold
    S = 0;
    R = 0;
    #20;

    // Reset
    S = 0;
    R = 1;
    #20;

    // Hold
    S = 0;
    R = 0;
    #20;

    // Invalid condition
    S = 1;
    R = 1;
    #20;

    $finish;

end

always @(posedge clk)
begin
    #1;

    $display(
        "clk=%b S=%b R=%b | Q=%b Q_bar=%b",
        clk, S, R, Q, Q_bar
    );
end

endmodule
```

---

## 🌊 Expected Waveform

The simulation waveform verifies the following operations:

```text
S  R  | Q(next) | Operation
----------------------------
0  0  | Q       | Hold
0  1  | 0       | Reset
1  0  | 1       | Set
1  1  | X       | Invalid
```

The output changes only at the **positive edge of the clock**.

---

## 🔧 Working Principle

The SR Flip-Flop responds to the inputs only at the positive edge of the clock.

### 1. Hold Condition

When:

```text
S = 0
R = 0
```

The flip-flop retains its previous state.

```text
Q(next) = Q
```

---

### 2. Reset Condition

When:

```text
S = 0
R = 1
```

The output is reset:

```text
Q = 0
Q_bar = 1
```

---

### 3. Set Condition

When:

```text
S = 1
R = 0
```

The output is set:

```text
Q = 1
Q_bar = 0
```

---

### 4. Invalid Condition

When:

```text
S = 1
R = 1
```

Both Set and Reset are requested simultaneously.

This is considered an **invalid condition** for a conventional SR Flip-Flop.

In this Verilog implementation:

```verilog
Q <= 1'bx;
```

is used to represent the invalid/unknown state.

Therefore:

```text
Q = X
Q_bar = X
```

---

## 🏗️ Block Diagram

```text
                 ┌──────────────┐
        S ──────►│              │
                 │              │
        R ──────►│ SR Flip-Flop │──────► Q
                 │              │
      CLK ──────►│              │──────► Q̅
                 └──────────────┘
```

### Internal Operation

```text
                    ┌─────────┐
S ─────────────────►│         │
                    │   SR    │──────► Q
R ─────────────────►│   FF    │
                    │         │──────► Q̅
CLK ───────────────►│         │
                    └─────────┘
```

The state changes only when a **positive edge of the clock** occurs.

---

## 🔄 State Transition Summary

```text
             S=1,R=0
          ┌─────────────┐
          │             ▼
      ┌───────┐       ┌───────┐
      │ Q = 0 │       │ Q = 1 │
      └───────┘       └───────┘
          ▲             │
          │             │
          └─────────────┘
             S=0,R=1

        S=0,R=0 → Hold

        S=1,R=1 → Invalid
```

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