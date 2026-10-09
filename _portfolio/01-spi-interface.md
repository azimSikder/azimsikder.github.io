---
title: "Adaptive SPI Communication Interface: RTL to GDS"
excerpt: "SPI master/slave controller with a 256 × 32 memory, verified to 100% functional coverage and implemented from RTL to GDS at 100 MHz.<br/><img src='/images/spi-layout-gpdk045.jpg' width='300'>"
collection: portfolio
---

**Course:** EEE 468 VLSI Circuit Design Laboratory, BUET (team project)  
**Tools:** SystemVerilog, Cadence Xcelium, Genus, Innovus (GPDK045); Yosys, OpenROAD, OpenSTA, KLayout (IHP SG13G2 130 nm)

## Overview

A complete SPI communication interface designed and taken through the full VLSI flow: RTL design, functional verification, synthesis, and physical layout. The system supports write and read operations using a 64-bit frame with an 8-bit command, a 24-bit address, and a 32-bit data field.

## Architecture

![Top-level architecture](/images/spi-architecture.jpg)

- **SPI master:** initiates each transaction, drives chip select and the serial clock, and shifts the 64-bit frame out over MOSI while capturing read data from MISO. Controlled by an FSM with IDLE, ENABLE, and DATA states.
- **SPI slave:** reconstructs the frame through MSB-first serial-to-parallel shifting, decodes the command, and either writes to memory or returns the addressed word over MISO. Controlled by an FSM with IDLE, DATA, and DISABLE states.
- **256 × 32 memory:** synchronous write, asynchronous read, interfaced directly with the slave.

## Outputs

### Verification

A layered constrained-random SystemVerilog testbench (generator, driver, monitor, scoreboard, coverage) generated random write-read pairs and checked every read. Functional coverage across 65 bins reached **100%** after about 500 transactions, with zero mismatches.

| Write-read pairs | Functional coverage |
|---|---|
| 10 | 27.69% |
| 100 | 83.08% |
| 256 | 96.92% |
| ~500 | **100%** |

![Simulation waveform: write and read cycles](/images/spi-layered-tb-waveform.jpg)

![Functional coverage report](/images/spi-coverage-report.jpg)

### Physical Implementation

- **Cadence flow (GPDK045):** met **100 MHz** with positive setup and hold slack, in about **3,100 µm²** (1,297 gate equivalents).
- **Open-source flow (IHP SG13G2, 130 nm):** full I/O pad ring on a 2.5 mm × 2.5 mm die, **23.8 mW** at 100 MHz.

![Routed layout in Cadence Innovus (GPDK045)](/images/spi-layout-gpdk045.jpg)

![Layout with I/O pad ring (IHP SG13G2, OpenROAD)](/images/spi-layout-ihp-sg13g2.jpg)
