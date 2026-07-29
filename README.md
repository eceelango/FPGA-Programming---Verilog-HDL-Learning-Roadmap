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

## 💻 Simulation

The design can be simulated using:

- Xilinx Vivado
- ModelSim
- Icarus Verilog
- EDA Playground

---

## 📂 Project Structure

```
4-bit-up-counter/
│── up_counter.v          # Verilog design
│── up_counter_tb.v       # Testbench
│── README.md             # Documentation
```

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

## 👨‍💻 Author

**Name:** *Your Name*  
**Course:** Digital System Design / Verilog HDL  
**Institution:** *Your College Name*

---

## 📜 License

This project is intended for educational and learning purposes.
