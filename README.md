# 🚀 RTL to GDSII using OpenLANE & Sky130

### Complete ASIC Design Flow | VSD SoC Design & Planning Workshop

---

## 🌟 Overview

This repository documents my complete hands-on journey through the **RTL-to-GDSII ASIC design flow** using **OpenLANE** and the **Sky130 PDK**.

Unlike just theoretical learning, this project walks through the **actual physical implementation of a digital design**, starting from RTL and ending at a manufacturable **GDSII layout**.

Throughout this workshop, I didn’t just run tools — I understood:

* how a chip is physically built
* how timing, power, and area interact
* and how every stage affects the final silicon

This README is written in a **detailed, structured, and explanation-driven format** so that:

* I can revise everything later
* I can explain confidently in interviews
* It reflects real understanding, not copied notes

---

# 📅 Day 1 — Foundations of ASIC Design & OpenLANE

## 🧠 Understanding What a Chip Really Is

When we look at a PCB and identify a “chip”, what we are actually seeing is the **package**, not the real silicon.

The actual working component is the **die**, which is enclosed inside this package. The die is where all computation happens.

The connection between the die and the external world is established using **wire bonding**, where extremely thin wires connect:

* **Pads on the die**
* **Pins on the package**

This simple realization changes how we understand hardware — the visible part is just protection and connectivity, while the intelligence lies inside.

---

## 🔍 Internal Structure of a Chip

Inside the die, the structure is divided into:

### Core

The core is the region where all digital logic exists. It contains:

* standard cells
* combinational logic
* sequential elements

This is where actual computation takes place.

---

### Pads

Pads are placed around the boundary and act as the interface between internal logic and the external environment.

Every signal entering or leaving the chip must go through pads.

---

### Die

The combination of core and pads forms the die — the actual fabricated silicon.

---

## 🏭 Industry Concepts

Understanding terminology is critical:

* **Foundry** → where chips are manufactured
* **Foundry IPs** → complex blocks like SRAM, PLL
* **Macros** → reusable digital modules

These concepts reflect how real industry designs are built using reuse and abstraction.

---

## 🔗 Software to Hardware Transformation

One of the most important learnings is how software becomes hardware.

A simple C program goes through multiple transformations:

```text
C → Assembly → Machine Code → RTL → Gates → Layout → GDSII
```

Each layer abstracts complexity:

* Software defines behavior
* RTL defines structure
* Physical design defines geometry

The final output is not code — it is **physical shapes on silicon**.

---

## 🌍 Importance of Open-Source EDA

ASIC design requires:

* RTL
* EDA tools
* PDK

Earlier, PDKs were restricted and available only under NDA.

The release of **Sky130 PDK (2020)** changed everything by making chip design accessible to students and researchers.

---

## ⚙️ OpenLANE Flow

OpenLANE integrates multiple tools into a single automated flow:

| Stage         | Purpose                 |
| ------------- | ----------------------- |
| Synthesis     | RTL → gates             |
| Floorplanning | Define layout structure |
| Placement     | Arrange cells           |
| CTS           | Build clock network     |
| Routing       | Connect wires           |
| STA           | Timing verification     |
| DRC/LVS       | Physical verification   |
| GDSII         | Final output            |

---

## 🧪 Hands-on Experience

I ran OpenLANE in interactive mode:

```bash
cd OpenLane
make mount
./flow.tcl -interactive
prep -design picorv32a
run_synthesis
```

This helped me understand how each stage works individually instead of treating it as a black box.

---

## 📊 Key Insight

Flop Ratio:

```text
1613 / 15762 ≈ 10.23%
```

This gives an idea of how much of the design is sequential logic.

---

# 📅 Day 2 — Floorplanning, Placement & Cell Design

Day 2 is where the entire learning shifted from theory to something much more tangible.

Until Day 1, the flow felt abstract — we knew the steps, but we didn’t really feel how a chip is physically built.
On Day 2, that changed. I started understanding how decisions made at this stage directly impact the final chip in terms of **area, performance, and routability**.

---

## 🧱 Floorplanning — The Foundation of Physical Design

Floorplanning is the stage where we define the **structure of the chip before placing any cells**.

At this point, we are not dealing with individual gates yet — instead, we are deciding:

* how much area the chip should occupy
* where major blocks will be placed
* how power and signals will flow

A bad floorplan can create problems that **cannot be fixed later**, no matter how good placement or routing is.

---

## 📍 Core vs Die — A Crucial Distinction

One of the most important clarifications at this stage is the difference between **core** and **die**.

The **die** represents the entire chip area, including pads and boundary regions.
The **core**, on the other hand, is the region where all standard cells and logic are placed.

This distinction matters because:

* all optimization happens inside the core
* routing congestion is evaluated in the core
* timing paths are mostly within the core

---

## 📊 Utilization — Balancing Area and Routability

Utilization defines how much of the core is occupied by standard cells.

```text
Utilization = Standard Cell Area / Core Area
```

If utilization is too low, we waste silicon area, which increases cost.
If utilization is too high, there is no space left for routing, which leads to congestion and timing failures.

Through this, I understood that ASIC design is always about **trade-offs**, not extremes.

The practical sweet spot lies around **50% to 70%**, where we balance area efficiency and routability.

---

## 📐 Aspect Ratio — More Than Just Geometry

Aspect ratio (height/width) may seem like a simple parameter, but it has deep implications.

A poorly chosen aspect ratio can:

* increase wirelength
* introduce routing congestion
* degrade timing

This showed me that even geometric decisions affect electrical performance.

---

## 🔌 Pin Placement — Connecting the Outside World

Pin placement is not arbitrary. It is carefully decided based on signal flow.

Inputs are placed close to where they are consumed.
Outputs are placed near exit points.
Clock pins are handled with extra care because the clock network spans the entire chip.

This made me realize that **physical proximity directly impacts delay**.

---

## ⚡ Power Planning — Ensuring Stability

Power planning involves building a **robust VDD and VSS network** across the chip.

The goal is to ensure:

* uniform voltage distribution
* minimal IR drop
* reliable operation under switching activity

Without proper power planning, even a logically correct design can fail physically.

---

## 📍 Placement — From Logic to Physical Reality

Placement is where the abstract netlist starts becoming a real physical design.

Instead of just connections, we now assign **exact locations to every standard cell**.

---

## 🔄 Placement Stages

### Global Placement

This is an initial rough arrangement where cells are placed to minimize wirelength, even if overlaps exist.

---

### Detailed Placement

Here, overlaps are removed and cells are aligned into legal rows, following design rules.

---

### Placement Optimization

This is where most of the intelligence of the tool is applied.

The tool continuously adjusts placement to improve timing, reduce congestion, and optimize area.

---

## ⚡ Optimization Techniques — Where Real Engineering Happens

Placement is not just positioning — it is continuous optimization.

### Buffer Insertion

Long wires introduce delay. Buffers are inserted to split long paths and improve signal propagation.

---

### Cell Movement

Cells are moved closer to reduce wirelength and improve timing paths.

---

### Cell Resizing

Cells are upsized to increase drive strength when needed.
However, this increases power — again showing the trade-off between performance and efficiency.

---

## 🚧 Congestion — A Real Physical Problem

One major issue I learned is **congestion**.

When too many cells are packed into one region:

* routing becomes difficult
* timing paths get worse
* design may fail

The tool **RePlAce** helps solve this by distributing cells evenly and balancing density across the chip.

---

## 🔋 Decap Cells — Hidden but Critical

Decoupling capacitors are inserted to stabilize power.

They act as local charge reservoirs and reduce voltage fluctuations during switching.

This was a key realization — power integrity is just as important as logic design.

---

## 🔬 Standard Cells & Characterization — The Backbone

Every stage of ASIC design depends on standard cells.

But more importantly, it depends on their **characterization**, which is captured in the `.lib` file.

This file defines:

* delay
* transition time
* power

And is used in:

* synthesis
* placement
* timing analysis

---

## ⏱️ Timing Understanding

Propagation delay measures how fast signals move through logic.
Slew measures how fast signals transition.

Both directly affect:

* timing
* power
* signal quality

---

## 📦 Final Realization of Day 2

At the end of Day 2, one thing became very clear:

```text
Standard Cell → Characterization → .lib → Used in entire flow
```

This is the backbone of ASIC design.

---

# 📅 Day 3 — Standard Cell Design & Characterization

Day 3 moved deeper into the **foundation of digital design — the standard cell itself**.

Instead of just using cells, I understood how they are designed and analyzed.

---

## 🔬 CMOS Inverter — The Simplest but Most Important Cell

The CMOS inverter is the basic building block of all digital circuits.

By studying it, I understood:

* switching behavior
* delay characteristics
* power consumption

---

## 🧪 From Layout to Simulation

I used Magic to view and edit layout, then extracted a SPICE netlist.

Using ngspice, I simulated the inverter to observe real waveform behavior.

This bridged the gap between:

* layout
* electrical behavior

---

## 📊 Measurements

From the waveform, I extracted:

* rise time
* fall time
* propagation delay

These values are essential for characterization.

---

## ⚠️ Real Debugging Experience

I encountered a **poly.9 DRC issue**, where rules were not correctly enforced.

Fixing this required:

* understanding design rules
* modifying tech files
* verifying correctness

This was my first real exposure to debugging in physical design.

---

# 📅 Day 4 — Timing Analysis & Clock Tree Synthesis

Day 4 focused on understanding **timing**, which is one of the most critical aspects of chip design.

---

## 🧠 Static Timing Analysis (STA)

STA checks whether signals arrive on time without needing simulation.

The key metric is:

```text
Slack = Required Time - Arrival Time
```

If slack is negative → timing violation
If positive → timing is safe

---

## 🔍 Real-World Effects

I learned that timing is affected by:

* process variations (OCV)
* clock uncertainty (jitter, skew)
* pessimism (CRPR)

This showed how real chips deal with uncertainty.

---

## 🌲 Clock Tree Synthesis (CTS)

Clock is the most critical signal in a synchronous design.

CTS builds a tree of buffers to distribute the clock evenly.

Goals:

* minimize skew
* balance delays

After CTS, timing must be re-evaluated because new delays are introduced.

---

# 📅 Day 5 — Routing & Final GDSII

Day 5 is the final stage where everything comes together.

---

## 🧠 Routing — Connecting Everything

Routing converts placed cells into a fully connected circuit.

### Global Routing

Plans approximate paths

### Detailed Routing

Creates exact wires following design rules

---

## ⚡ Parasitics — The Hidden Effects

Real wires introduce resistance and capacitance.

These are extracted into a **SPEF file**, which is used for final timing analysis.

---

## 📊 Post-Route STA

After routing, timing is checked again with real parasitic values.

This is the final verification before tapeout.

---

## ⚠️ Practical Issues

During routing, issues like:

* spacing violations
* antenna effects

must be fixed to ensure manufacturability.

---

## 🎯 Final Understanding

By the end of Day 5, I understood the complete journey:

```text
RTL → Synthesis → Floorplan → Placement → CTS → Routing → GDSII
```

---

## 🚀 Final Takeaway

This workshop gave me a **complete end-to-end understanding of ASIC design**, from abstract logic to real silicon implementation.

More importantly, I now understand:

* how each stage impacts the next
* how trade-offs are made
* and how real chip design works in practice

---
