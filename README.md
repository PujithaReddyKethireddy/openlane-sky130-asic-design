# openlane-sky130-asic-design
End-to-end ASIC design flow using OpenLANE &amp; Sky130 (RTL to GDSII) with RISC-V (picorv32)
# 🚀 OpenLANE Sky130 ASIC Design Flow (RTL → GDSII)

## 📌 Overview

This repository documents my journey in learning and implementing the **complete ASIC design flow** using:

* 🧠 RISC-V ISA
* ⚙️ RTL Design (Verilog – picorv32)
* 🏗️ OpenLANE Flow
* 🧬 Sky130 PDK

---

## 🧠 Design Flow (Big Picture)

```text
C Program
   ↓
Compiler
   ↓
RISC-V ISA (Assembly)
   ↓
RTL (Verilog – picorv32)
   ↓
Synthesis (Netlist)
   ↓
Floorplan → Placement → CTS → Routing
   ↓
GDSII (Final Chip Layout)
```

---

## 🎯 Objective

* Understand how software translates into hardware
* Learn RTL to GDSII flow
* Gain hands-on experience with OpenLANE
* Build industry-relevant ASIC design knowledge

---

## 📂 Repository Structure

```text
docs/          → Concept explanations (theory + examples)
notes/         → Important points & interview questions
designs/       → OpenLANE runs and configs
screenshots/   → Layouts, floorplans, outputs
reports/       → Timing, area, power reports
```

---

## 📅 Progress Tracker

* [x] Day 1 – RISC-V Basics & Flow Understanding
* [ ] Day 2 – Floorplanning
* [ ] Day 3 – CMOS Design & Layout
* [ ] Day 4 – Timing Analysis & CTS
* [ ] Day 5 – Routing & Final GDS

---

## 🧠 Key Learnings

* RISC-V ISA and instruction flow
* Difference between ISA, RTL, and Layout
* RTL to Gate-level synthesis
* Physical design stages in ASIC flow

---

## 🔍 Example (From Day 1)

### RISC-V Instruction:

```c
add x5, x1, x2
```

### Meaning:

* Adds values from registers x1 and x2
* Stores result in x5

👉 This instruction is later implemented in hardware using RTL.

---

## 📸 Outputs

*(Will be updated as I progress through the course)*

---

## 💡 Notes

* This repository focuses on **understanding + implementation**
* All explanations are written in my own words
* Includes both theory and practical insights

---

## 🎯 Goal

To build a strong foundation in **ASIC design** and prepare for roles in:

* VLSI Design
* Physical Design
* Hardware Engineering

---
