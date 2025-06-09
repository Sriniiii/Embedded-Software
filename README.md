# Embedded-Software
SDRAM Interface Controller
# 💾 SDRAM Interface Controller

> **Project Duration:** Jan 2024 – May 2024  
> **Role:** Hardware Designer (RTL, Simulation, FPGA Integration)  
> **Goal:** Design a custom SDRAM controller to enable a microprocessor—lacking native synchronous memory support—to communicate with SDRAM reliably and efficiently.

---

##  Overview

This project implements a fully functional **SDRAM controller in Verilog**, capable of translating asynchronous memory access requests from a microprocessor into correctly timed SDRAM command sequences.

Features:
- Command FSM: `ACTIVATE`, `READ`, `WRITE`, `PRECHARGE`, `REFRESH`
- Auto-refresh management (configurable interval)
- Burst read/write support
- Reduced memory access latency by 30%
- Verified on simulation and FPGA hardware

---

## Background

Most modern SDRAM chips (e.g., MT48LC16M16) require:
- Strict timing control (tRCD, tRP, tRAS, CAS latency)
- Multiplexed row/column address setup
- Periodic refresh cycles

This controller bridges those requirements to work with simpler CPUs or MCUs that only support asynchronous SRAM-like memory.

---

##  Architecture
+--------------------------+
| Microprocessor |
| (asynchronous access) |
+------------+-------------+
|
v
+------------+-------------+
| SDRAM Interface Logic |
| - Asynch to Synch Bridge |
| - Command Scheduler FSM |
| - Row/Col Address Logic |
+------------+-------------+
|
v
+--------------------------+
| SDRAM |
+--------------------------+
├── rtl/ # Synthesizable Verilog modules
│ ├── sdram_controller.v
│ └── fsm.v
├── tb/ # Testbenches
│ └── tb_sdram.v
├── sim/ # Simulation scripts & waveforms
├── docs/ # Block diagrams, timing charts
├── fpga/ # Vivado project files
└── README.md


---

##  Verification

-  **Testbenches** simulate key timing scenarios (ACT → READ → PRE → REF)
-  **Simulation Logs** capture command FSM transitions and bus activity
-  **Waveform Dumps** verify SDRAM timing parameters met
-  **FPGA Validation** using LEDs + UART debug output

---

##  Results

| Metric                     | Result                     |
|----------------------------|----------------------------|
| Compatible MCUs            | Any async-only memory bus  |
| Latency Improvement        | ~30% faster than prior setup |
| Clock Frequency (tested)   | 50 MHz SDRAM clock         |
| SDRAM Chip Used            | MT48LC16M16 (16MB, 16-bit) |

---

## How to Use

### Simulate in ModelSim

```bash
cd sim/
vsim -do run_tb_sdram.do



