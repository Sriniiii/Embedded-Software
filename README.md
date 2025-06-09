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

