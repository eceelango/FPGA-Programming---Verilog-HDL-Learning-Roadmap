# Verilog Core Labs — Boolean Board Edition

This repository is a shared academic collection of Verilog designs developed and verified on the **RealDigital Boolean Board**. It's organized into three core digital design domains — **Combinational Logic**, **Sequential Logic**, and **Finite State Machines (FSM)** — covering the standard progression from basic gate-level design through clocked and multi-state hardware.

---

## 🔧 Boolean Board — Hardware Specification

| Component                       | Detail                                                                                                        |
|:---------------------------------|:---------------------------------------------------------------------------------------------------------------|
| **FPGA**                        | Xilinx (AMD) Spartan-7 XC7S50-CSGA324                                                                        |
| **Logic Capacity**              | ~52K logic cells (8,000+ slices, each with four 6-input LUTs + 8 flip-flops)                                 |
| **DSP Blocks**                  | 120 (dual 24-bit adders, 2's complement multiplier, 48-bit accumulator)                                      |
| **Clocking**                    | 5 Clock Management Tiles (CMTs)                                                                              |
| **Programming**                 | Single USB port — power, UART/COM, and FPGA programming (JTAG or PROM via jumper J13)                        |
| **Display**                     | 8-digit seven-segment display                                                                                |
| **Switches**                    | 16 slide switches                                                                                            |
| **Buttons**                     | 4 pushbuttons                                                                                                |
| **LEDs**                        | 16 discrete LEDs + 2 RGB LEDs                                                                                |
| **Audio**                       | PWM audio output                                                                                             |
| **Motors**                      | 4 servo motor headers                                                                                        |
| **Analog**                      | On-board ADC with thumbwheel potentiometer                                                                   |
| **Expansion**                   | 2 Pmod+ connectors (4 Pmods total)                                                                           |
| **Wireless (Upgrade version)**  | Bluetooth Low Energy (BLE) radio                                                                             |
| **Video (Upgrade version)**     | HDMI source, up to 1080p                                                                                     |
| **Storage**                     | 16MB QSPI Flash                                                                                              |
| **Toolchain**                   | AMD Vivado (free) — Verilog/VHDL entry, simulation, synthesis, implementation, and bitstream programming     |

**Programming flow:** Vivado synthesizes and implements the Verilog source into a `.bit` file, which is either sent directly to the FPGA over USB (JTAG mode) or programmed into the on-board QSPI Flash so the FPGA auto-configures on power-up/reset (PROM mode). Jumper **J13** selects between these two modes.

📄 Reference: [Boolean Board Reference Manual](https://www.realdigital.org/doc/02013cd17602c8af749f00561f88ae21) · [Schematic](https://www.realdigital.org/downloads/63f9a8205ebd9c2e8c2d265ad25097dc.pdf) · [Spartan-7 Datasheet](https://www.xilinx.com/products/silicon-devices/fpga/spartan-7.html#documentation)

---

## 📁 Repository Structure

```
├── combinational
├── sequential
├── fsm
└── README.md
```

Each folder contains standalone Verilog modules, their testbenches, and (where applicable) a Boolean Board constraints (`.xdc`) file mapping I/O to switches, LEDs, buttons, or the seven-segment display.

---

## 🔹 combinational

Combinational circuits — output depends only on current inputs, no memory/clock involved.

| File                      | Description                            |
|:---------------------------|:-----------------------------------------|
| `mux_2to1.v`               | 2-to-1 multiplexer                     |
| `full_adder.v`              | 1-bit full adder (gate-level)          |
| `priority_encoder.v`        | 4-to-2 priority encoder                |
| `seven_seg_decoder.v`       | BCD to seven-segment display decoder   |
                                        
---

## 🔹 sequential

Sequential circuits — output depends on current inputs **and** stored state, driven by a clock.

| File                      | Description                              |
|:---------------------------|:-------------------------------------------|
| `d_flip_flop.v`             | Basic D flip-flop                        |
| `shift_register.v`          | Serial-in/serial-out shift register      |
| `counter_up_down.v`         | Up/down binary counter                   |
| `synchronizer.v`            | Two-stage input synchronizer             |


---

## 🔹 fsm

Finite State Machines — Moore and Mealy style controllers and sequence detectors.

| File                            | Description                                              |
|:----------------------------------|:------------------------------------------------------------|
| `traffic_light_fsm.v`             | Moore machine, Gray-coded states, 3-block coding style   |
| `vending_machine_fsm.v`           | Moore vs. Mealy comparison                               |
| `sequence_detector_1011.v`        | Mealy overlapping sequence detector for pattern 1011     |
| `sequence_detector_1001.v`        | Mealy overlapping sequence detector for pattern 1001     |


---

## 🚀 Getting Started

1. Clone the repository.
2. Open Vivado and create a new project targeting **xc7s50csga324-1**.
3. Add the desired `.v` source file(s) and, if targeting hardware, the matching `.xdc` constraints file.
4. Simulate using the built-in Vivado simulator to verify functional correctness.
5. Synthesize and generate the bitstream.
6. Connect the Boolean board via USB, set jumper **J13** to JTAG, and program the FPGA directly — or set it to PROM to load onto QSPI Flash for auto-boot.

---

