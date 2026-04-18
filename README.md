# 🚀 RTL to GDSII using OpenLANE & Sky130

### VSD SoC Design & Planning Workshop (Complete Detailed Notes)

This repository documents my complete journey through the **RTL-to-GDSII ASIC design flow** using **OpenLANE** and the **Sky130 PDK**.

This README is intentionally written in a **very detailed and step-by-step manner**, so that:

* I can revise everything without watching lectures again
* I can clearly explain each concept in interviews
* I don’t miss even small but important details

---

# 📅 Day 1 — Inception of Open-Source EDA, OpenLANE & Sky130 PDK

## 🧠 Understanding What We Actually See as a “Chip”

When we look at a PCB and point at a “chip”, what we are actually seeing is **NOT the real chip**.

What we see is called the **package**.

### 📦 Package

* Outer protective structure
* Protects internal silicon from damage
* Helps in heat dissipation
* Provides pins for external connection

---

## 🔬 Inside the Package — The Real Chip

Inside the package, there is a **small silicon block called the DIE**.

This die contains the actual circuit.

### 🔗 Wire Bonding

* Thin metal wires connect:

  * Die pads → Package pins
* These wires are extremely small but critical
* They allow communication between internal logic and outside world

---

## 🔍 Inside the Die

### 🟦 Core

* This is the most important region
* Contains:

  * logic gates
  * flip-flops
  * combinational circuits
* All computations happen here

---

### 🟨 Pads

* Located around the boundary
* Act as entry/exit points
* Every signal must pass through pads

---

### 🧱 Die = Core + Pads

👉 So overall structure is:

```text
Package → Die → (Core + Pads)
```

---

## 🏭 Important Industry Terms

### Foundry

* Place where chips are physically manufactured
* Example: SkyWater, TSMC

---

### Foundry IPs

* Complex blocks that depend on manufacturing process
* Examples:

  * SRAM
  * PLL
* Cannot be easily redesigned from scratch

---

### Macros

* Pre-designed reusable blocks
* Purely digital
* Example:

  * ALU
  * memory blocks

---

## 🔗 From Software to Hardware (VERY IMPORTANT)

A program written in C does not directly run on hardware.

It goes through multiple transformations:

```text
C Program
↓
Assembly (RISC-V ISA)
↓
Machine Code (0s and 1s)
↓
RTL (Hardware Description)
↓
Gate-Level Netlist
↓
Physical Layout
↓
GDSII (Final Chip)
```

---

### 🧠 Key Understanding

* Software defines behavior
* RTL defines hardware structure
* Physical design converts it into geometry

👉 Final output is literally **patterns on silicon**

---

## 🌍 Why Open-Source EDA Matters

To design a chip, we need:

1. RTL design
2. EDA tools
3. PDK

---

### 🚫 Before 2020

* PDKs were closed source
* Only big companies had access
* Students could not do full chip design

---

### 🚀 After Sky130

* Open-source PDK released
* Anyone can design chips
* Full RTL → GDSII flow became accessible

---

## ⚙️ OpenLANE Flow (Detailed Understanding)

OpenLANE is not a single tool — it is a **flow that combines multiple tools**.

### Flow Breakdown:

1. **Synthesis**

   * Converts RTL → gates
   * Tool: Yosys

2. **Floorplanning**

   * Defines chip area
   * Places macros
   * Plans power

3. **Placement**

   * Places standard cells

4. **Clock Tree Synthesis**

   * Distributes clock signal

5. **Routing**

   * Connects all wires

6. **Extraction**

   * Extracts parasitic R and C

7. **STA**

   * Checks timing

8. **DRC/LVS**

   * Ensures correctness

9. **GDSII**

   * Final chip file

---

## 🧪 Lab — Running OpenLANE

### Step 1 — Start OpenLANE

```bash
cd OpenLane
make mount
./flow.tcl -interactive
package require openlane 1.0.2
```

👉 Interactive mode helps run flow step-by-step

---

### Step 2 — Prepare Design

```tcl
prep -design picorv32a
```

What happens:

* Loads design files
* Merges LEF files
* Creates run directory

---

### Step 3 — Run Synthesis

```tcl
run_synthesis
```

What happens internally:

* RTL converted to gates
* Optimizations performed

---

## 📊 Important Metric — Flop Ratio

```text
Flop Ratio = Number of Flip-Flops / Total Cells
           = 1613 / 15762 ≈ 10.23%
```

👉 Helps understand design composition

---

# 📅 Day 2 — Floorplanning & Placement

## 🧠 Floorplanning Basics

Floorplanning is about **deciding where everything goes on the chip**.

---

### 📐 Utilization Factor

```text
Utilization = Area of Cells / Total Core Area
```

* Ideal: 50–60%
* Too high → congestion
* Too low → wasted area

---

### 📏 Aspect Ratio

```text
Aspect Ratio = Height / Width
```

* 1 → square
* ≠1 → rectangular

---

## ⚡ Key Concepts

### Pre-Placed Cells

* SRAM, macros
* Fixed before placement

---

### Decoupling Capacitors

* Provide local charge
* Reduce voltage drop

---

### Power Planning

* Uses:

  * Power rings
  * Power mesh
* Ensures stable power

---

### Pin Placement

* Based on connectivity
* Helps reduce routing complexity

---

## 🧪 Lab — Floorplanning

```tcl
run_floorplan
```

---

### View DEF File

```bash
cd results/floorplan
less picorv32a.def
```

---

### View Layout

```bash
magic -T sky130A.tech ...
```

---

## 🧪 Placement

```tcl
run_placement
```

---

### Result

* Cells placed legally
* No overlaps
* Ready for CTS

---

# 📅 Day 3 — Standard Cell Design & Characterization

## 🧠 CMOS Inverter

Basic building block of digital design.

---

### Key Parameters

* Rise Time (20% → 80%)
* Fall Time (80% → 20%)
* Propagation Delay (50% → 50%)

---

## 🧪 Lab — Design & Simulation

### Clone Repository

```bash
git clone https://github.com/nickson-jose/vsdstdcelldesign.git
```

---

### Open Layout

```bash
magic -T sky130A.tech sky130_inv.mag &
```

---

### Extract SPICE

```tcl
extract all
ext2spice
```

---

### Run Simulation

```bash
ngspice sky130_inv.spice
```

---

## 📊 Measurements

* Rise time
* Fall time
* Switching threshold

---

## ⚠️ Debug Learning

* Found issue in **poly.9 rule**
* Fixed DRC rule manually

👉 Important real-world skill

---

## 🏭 Fabrication Steps (High-Level)

* Substrate
* Wells
* Gate
* Source/Drain
* Metal layers

---

# 📅 Day 4 — Timing Analysis & CTS

## 🧠 STA Basics

```text
Slack = Required Time - Arrival Time
```

---

### Concepts

* OCV → variation
* Clock uncertainty → jitter
* CRPR → remove pessimism

---

## 🌲 Clock Tree Synthesis

* Distributes clock
* Reduces skew
* Impacts timing

---

## 🧪 Lab

### Add Custom Cell

* Generate LEF
* Add to OpenLANE

---

### Run STA

```bash
sta pre_sta.conf
```

---

### Run CTS

```tcl
run_cts
```

---

## 📊 Learning

* Timing changes after CTS
* Must recheck timing

---

# 📅 Day 5 — Routing & Final Flow

## 🧠 Routing

### Global Routing

* Rough path planning

### Detailed Routing

* Exact wires

---

## ⚡ Concepts

### SPEF

* Parasitic extraction

### Post-route STA

* Final timing check

---

## 🧪 Lab

```tcl
gen_pdn
run_routing
```

---

## ⚠️ Issues

* Spacing violations
* Antenna effects

---

# 🛠️ Tools Used

* OpenLANE
* Yosys
* OpenROAD
* Magic
* OpenSTA
* ngspice
* TritonRoute
* Netgen

---

# 🎯 Final Learnings

* Complete RTL → GDSII understanding
* Hands-on full flow
* Standard cell design
* Timing analysis
* Real debugging experience

---

# ✍️ Author

Kethireddy Pujitha Reddy 
ECE | VLSI Enthusiast

---
