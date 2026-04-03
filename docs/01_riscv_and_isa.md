# 🚀 OpenLANE + Sky130 ASIC Design Flow — Day 1 (Detailed + Logical Flow Documentation)

---

# 📌 1. Overview

This document provides a **complete and logically structured understanding of Day 1**, covering:

* Fundamentals of chip design
* Software-to-hardware abstraction
* Complete RTL-to-GDSII ASIC flow
* Tools used at each stage
* OpenLANE framework
* Directory structure
* Design preparation step
* Real-world applications
* Additional deep concepts for strong understanding

---

# 🌍 2. Real-World Context (WHY THIS MATTERS)

ASIC design is used in:

* AI accelerators (NVIDIA GPUs)
* CPUs and processors
* Mobile SoCs
* IoT devices
* Automotive electronics

### 🔥 IMPORTANT

* ASICs provide **high performance + low power**
* Used in **real silicon fabrication**
* Critical for modern computing systems
* Enables optimized hardware for specific applications

---

# 🧠 3. Fundamentals of Chip Design

## 📦 Chip Hierarchy

* **Package (QFN-48)** → Connects chip to PCB
* **Die** → Silicon substrate
* **Core** → Logic area
* **Pads** → External interface
* **IP Blocks** → Reusable modules

### 🔥 IMPORTANT

* Core is inside the die
* Pads connect to outside world
* IP reuse reduces design time
* Hierarchical design improves scalability

---

## 📦 QFN-48 Package

* No external pins → pads underneath
* Compact + better signal integrity
* Reduces parasitic inductance and resistance

---

# 💻 4. How Hardware Communicates with Software

## Levels of Abstraction

1. High-Level Language (C)
2. Assembly Language
3. Machine Code
4. RTL (Verilog)
5. Logic Gates
6. Transistors

### 🔥 IMPORTANT

* Each layer abstracts complexity
* Hardware executes **binary instructions**
* RTL bridges software and hardware
* Abstraction enables portability and scalability

---

# ⚙️ 5. RISC-V Architecture

* Open-source ISA
* Used in **picorv32a (OpenLANE design)**

### 🔥 IMPORTANT

* ISA = WHAT operations
* RTL = HOW operations are implemented
* Enables customization of processors

---

# 🔄 6. Software → Hardware Mapping

```text
C → Assembly → Machine Code → RTL → Gates → Layout
```

### 🔥 IMPORTANT

* Compiler + assembler convert software
* Hardware executes via datapath + control
* Control unit manages instruction execution
* Datapath performs arithmetic and logic operations

---

# 🏗️ 7. Components of ASIC Design

| Component      | Description  |
| -------------- | ------------ |
| RTL            | Behavior     |
| Standard Cells | Logic blocks |
| PDK            | Technology   |
| EDA Tools      | Automation   |

---

## 📌 Standard Cell Library

Contains:

* Gates, flip-flops, buffers

Includes:

* `.lib` → Timing
* `.lef` → Physical

---

### 🔥 IMPORTANT

> ASIC design is **library-based**, not transistor-level
> Standard cells are pre-characterized for timing and power

---

# 🧪 8. SKY130 PDK (Technology Backbone)

* 130nm open-source PDK
* By Google + SkyWater

Contains:

* Design rules
* Device models
* Standard cell libraries

### 🔥 IMPORTANT

* Defines manufacturing constraints
* Ensures DRC/LVS correctness
* Connects design → fabrication
* Includes SPICE models for simulation

---

# 🔁 9. Complete RTL-to-GDSII Flow (WITH TOOLS)

## ASIC Flow with Tools

1. **RTL Design**

   * Written in Verilog
   * Describes functionality

2. **Synthesis**

   * Tool: **Yosys**
   * Converts RTL → Gate-level netlist
   * Performs logic optimization

3. **Floorplanning**

   * Tool: **OpenROAD**
   * Defines chip area, IO placement
   * Sets core utilization and aspect ratio

4. **Placement**

   * Tool: **OpenROAD**
   * Places standard cells
   * Minimizes wirelength

5. **Clock Tree Synthesis (CTS)**

   * Tool: **OpenROAD**
   * Builds clock distribution network
   * Reduces clock skew

6. **Routing**

   * Tool: **OpenROAD**
   * Connects all components
   * Handles global and detailed routing

7. **Signoff**

   * DRC → **Magic**
   * LVS → **Netgen**
   * Parasitics → **SPEF Extractor**
   * Ensures design correctness

8. **Visualization**

   * Tool: **KLayout**

9. **GDSII Generation**

   * Final layout output

---

## ⚖️ Design vs Physical Implementation

* Design → RTL
* Implementation → Layout

### 🔥 IMPORTANT

* Same RTL → different layouts possible
* Physical design affects PPA (Power, Performance, Area)
* Trade-offs are required between speed, area, and power

---

# 📦 10. GDSII (Final Output)

* Final layout file
* Sent for fabrication

### 🔥 IMPORTANT

* Final deliverable
* Contains complete chip geometry
* Used directly by fabrication facilities

---

# 🧰 11. OpenLANE Framework

## 📌 Definition

OpenLANE is an **automated RTL-to-GDSII flow** integrating multiple open-source tools.

---

## 🔧 Tools Used in OpenLANE

| Tool           | Function                           |
| -------------- | ---------------------------------- |
| Yosys          | RTL Synthesis                      |
| OpenROAD       | Floorplan, Placement, CTS, Routing |
| Magic          | Layout + DRC                       |
| Netgen         | LVS                                |
| KLayout        | Layout Visualization               |
| SPEF Extractor | Parasitic Extraction               |

---

### 🔥 IMPORTANT

* OpenLANE = Automation layer
* Uses TCL + Python
* Tapeout proven
* Enables reproducible ASIC design flow

---

# 🧩 12. Strive Chipsets (Reference Designs)

* Open-source SoC designs used in OpenLANE

Examples:

* Strive 1
* Strive 2
* Strive SoC

### 🔥 IMPORTANT

* Used in real silicon tapeouts
* Demonstrates complete ASIC flow
* Includes CPU + peripherals
* Helps beginners understand full-chip integration

---

# 📁 13. OpenLANE Directory Structure

```text
OpenLANE/
├── designs/
├── runs/
├── scripts/
├── pdks/
├── configuration/
```

---

## 📂 designs/

```text
designs/<design_name>/
├── src/
├── config.tcl
```

### 🔥 IMPORTANT

* config.tcl controls full flow
* Defines clock period, constraints, and design parameters

---

## 📂 runs/

```text
runs/<run_name>/
├── logs/
├── reports/
├── results/
├── tmp/
```

---

## 📂 Folder Roles

| Folder  | Purpose       |
| ------- | ------------- |
| logs    | Debug         |
| reports | Analysis      |
| results | Output        |
| tmp     | Working files |

---

## 📂 tmp/

* merged.lef
* trimmed.lib

### 🔥 IMPORTANT

> tmp = working memory
> Stores intermediate files used during flow execution

---

# ⚙️ 14. OpenLANE Execution Modes

## 1. Interactive Mode

* Step-by-step execution
* Used for debugging
* Allows manual control of each stage

## 2. Non-Interactive Mode

* Fully automated flow
* Used for production runs
* Executes entire flow in one command

---

# ⚙️ 15. Design Preparation Step

## Command

```bash
prep -design <design_name>
```

---

## Internal Steps

1. Load config
2. Load PDK
3. Extract libraries
4. Merge LEF
5. Prepare timing libraries
6. Create run directory

---

## Outputs

* merged.lef
* trimmed.lib

---

### 🔥 IMPORTANT

* LEF → Physical
* LIB → Timing
* Preparation ensures environment is ready for synthesis

---

# 🔍 16. Review After Prep

## Checks

* LEF merged successfully
* Libraries loaded
* No errors

---

### 🔥 DEBUG RULE

> Always check logs/
> Logs provide detailed error and warning information

---

# ⚙️ 17. OpenLANE Execution Flow

```bash
./flow.tcl -interactive
prep -design <design>
run_synthesis
```

---

# 📊 18. Synthesis (Intro)

## Output

* Gate-level netlist
* Timing report
* Area report

---

### 🔥 IMPORTANT

* RTL → standard cells
* Uses timing libraries
* Optimization balances area and performance

---

# 🧠 19. Key Concepts Summary

* OpenLANE = automated ASIC flow
* PDK = technology backbone
* RTL = hardware description
* LEF = physical data
* LIB = timing data
* GDSII = final fabrication file

---

# 🎯 20. Interview Highlights

### What is OpenLANE?

Automated RTL-to-GDSII open-source flow integrating multiple EDA tools.

---

### What happens in design prep?

Loads config, prepares libraries, merges LEF, and creates run environment.

---

### LEF vs LIB?

* LEF → Physical
* LIB → Timing

---

### Why PDK important?

Defines fabrication rules and ensures manufacturability.

---

### What is GDSII?

Final layout file sent for chip fabrication.

---

# 🚀 21. Key Learnings

* Complete ASIC design flow understanding
* Tools used in RTL-to-GDSII
* OpenLANE workflow
* Directory structure
* Design preparation
* Debugging approach
* Real-world chip relevance
* Understanding of abstraction layers and hardware mapping

---

# 🏁 22. Conclusion

Day 1 builds a strong foundation for:

* ASIC design flow
* OpenLANE usage
* Transition to physical design (Day 2)
* Understanding real chip design workflow

---

# 📎 Author

**Pujitha Reddy**
Future ASIC / VLSI Engineer 🚀
