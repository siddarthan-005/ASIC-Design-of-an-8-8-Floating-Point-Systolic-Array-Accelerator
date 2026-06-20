# ASIC Design of an 8×8 Floating-Point Systolic Array Accelerator

## Overview

This project implements an **8×8 Floating-Point Systolic Array Accelerator** for matrix multiplication and demonstrates a complete **RTL-to-GDSII ASIC design flow** using open-source EDA tools.

The accelerator consists of **64 Processing Elements (PEs)** arranged in an 8×8 grid. Each PE performs floating-point Multiply-Accumulate (MAC) operations, enabling highly parallel computation suitable for AI, Machine Learning, DSP, and scientific computing applications.

The design was implemented in **Verilog HDL**, verified through simulation, synthesized using **Yosys**, and physically realized using the **OpenROAD/OpenLane flow** targeting the **Sky130 technology node**.

---

## Features

- 8×8 Systolic Array Architecture
- IEEE-754 Floating Point Arithmetic
- Parallel Matrix Multiplication Engine
- 64 Processing Elements (PEs)
- RTL Design using Verilog HDL
- Functional Verification using Icarus Verilog & GTKWave
- Complete ASIC Backend Flow
  - Synthesis
  - Floorplanning
  - Placement
  - Clock Tree Synthesis (CTS)
  - Routing
  - Static Timing Analysis (STA)
  - DRC/LVS Verification
- Final GDSII Layout Generation

---

## Architecture

### Processing Element Operation

Each PE performs:

```text
C = C + (A × B)
```

where:

- A = Input from left
- B = Input from top
- C = Partial Sum

The systolic array streams matrix data across a 2D grid of processing elements, allowing matrix multiplication to be performed efficiently with high throughput and data reuse.

---

## Design Specifications

| Parameter | Value |
|------------|--------|
| Architecture | 8×8 Systolic Array |
| Processing Elements | 64 |
| Arithmetic | IEEE-754 Floating Point |
| Technology Node | Sky130 |
| Supply Voltage | 1.8 V |
| Clock Frequency | 10 MHz |
| ASIC Flow | OpenROAD / OpenLane |

---

## Repository Structure

```text
.
├── rtl/
│   ├── fp_adder.v
│   ├── fp_multiplier.v
│   ├── pe.v
│   ├── systolic_array.v
│   └── top.v
│
├── tb/
│   └── tb_MatMul8x8.v
│
├── synthesis/
│
├── floorplan/
│
├── placement/
│
├── routing/
│
├── reports/
│
└── README.md
```

---

## OpenROAD Output Files

### 1. Floorplanning Files

#### `1_floorplan.def`

Generated after floorplanning.

Contains:

- Die dimensions
- Core dimensions
- IO placement
- Macro placement
- Initial power planning

---

### 2. Placement Files

#### `placement_legalized.def`

Legalized placement output where all standard cells are positioned without overlap.

#### `placement_9ns_slack.def`

Timing-optimized placement output generated after placement optimization.

#### `placement_9ns_slack.db`

Timing database used for optimization and slack analysis.

---

### 3. Routing Files

#### `final_routed.def`

Final routed DEF containing all signal and power routes.

#### `final_routed.odb`

OpenDB database of the final routed design.

Can be loaded directly into OpenROAD GUI for inspection.

---

### 4. Simulation Files

#### `gls_output`

Gate-Level Simulation output.

#### `gls_sim`

Compiled simulation executable.

#### `gls_sim.vvp`

Icarus Verilog simulation binary.

Run using:

```bash
vvp gls_sim.vvp
```

---

### 5. Technology Libraries

#### `sky130_fd_sc_hd.v`

Sky130 standard-cell Verilog models used for simulation.

#### `sky130_fd_sc_hd_tt_025C_1v80.lib`

Sky130 timing library used for:

- Timing analysis
- Power analysis
- Cell characterization

---

### 6. Synthesized Netlist

#### `synth_sky130_netlist.v`

Technology-mapped gate-level netlist generated after synthesis.

Contains:

- Standard-cell instances
- Optimized logic
- Timing-aware implementation

---

## Functional Verification

### Compile RTL

```bash
iverilog -o sim.out tb_MatMul8x8.v systolic_array.v
```

### Run Simulation

```bash
vvp sim.out
```

### Open Waveforms

```bash
gtkwave waves.vcd
```

---

## ASIC Flow

### Synthesis

```bash
yosys synthesis.tcl
```

### OpenLane Flow

```bash
flow.tcl -design MatMul8x8
```

### OpenROAD GUI

```bash
openroad -gui
```

Load final design:

```tcl
read_db final_routed.odb
```

---

## Design Flow

```text
RTL Design
    ↓
Functional Verification
    ↓
Logic Synthesis
    ↓
Floorplanning
    ↓
Power Distribution Network
    ↓
Placement
    ↓
Clock Tree Synthesis
    ↓
Routing
    ↓
Static Timing Analysis
    ↓
DRC / LVS Verification
    ↓
GDSII Generation
```

---

## Results

### Area

| Metric | Value |
|----------|----------|
| Total Cell Area | 1,835,394 µm² |
| Core Area | 6,250,000 µm² |
| Utilization | 30% |

### Timing

| Metric | Value |
|----------|----------|
| Clock Period | 30 ns |
| Worst Negative Slack (WNS) | 2.70 ns |
| Total Negative Slack (TNS) | 0.0 ns |

### Power

| Metric | Value |
|----------|----------|
| Total Power | 127 mW |
| Dynamic Power | 127 mW |
| Leakage Power | 617 nW |

### Verification Status

- RTL Simulation Passed
- Gate-Level Simulation Passed
- Static Timing Analysis Completed
- DRC Clean
- LVS Passed
- GDSII Generated Successfully

---

## Applications

- AI Accelerators
- Machine Learning Hardware
- Neural Network Inference
- Matrix Multiplication Engines
- Digital Signal Processing
- Scientific Computing
- Edge AI Systems

---

## Future Work

- Support for FP16/BF16 arithmetic
- Larger systolic arrays (16×16, 32×32)
- SRAM integration
- FPGA prototyping
- RISC-V accelerator integration
- Migration to advanced technology nodes

---

## Authors

**Siddarthan (231EC258)**  
Department of Electronics and Communication Engineering  
National Institute of Technology Karnataka (NITK)

**G Vedanth (231EC216)**  
Department of Electronics and Communication Engineering  
National Institute of Technology Karnataka (NITK)

---

## Acknowledgements

- OpenROAD Project
- OpenLane
- SkyWater SKY130 PDK
- Yosys Open Synthesis Suite
- NITK Department of Electronics and Communication Engineering
