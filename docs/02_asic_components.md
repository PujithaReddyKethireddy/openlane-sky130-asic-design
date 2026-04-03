# 🧩 ASIC Design Components (Detailed)

---

## 📌 What is ASIC?

ASIC (Application-Specific Integrated Circuit) is a chip designed for a specific application.

---

## 💡 Example:

* CPU
* GPU
* AI accelerators

---

## 🧠 Key Components of ASIC Design

ASIC design requires 3 major components:

---

# 1️⃣ RTL (Register Transfer Level)

---

## 📌 What is RTL?

RTL describes:

* Data flow between registers
* Logic operations

---

## 🔧 Written in:

* Verilog
* VHDL

---

## 🎯 Example:

```verilog id="rtl1"
always @(posedge clk)
```

---

## 💡 Role:

* Defines hardware behavior
* Input to synthesis

---

---

# 2️⃣ EDA Tools

---

## 📌 What are EDA Tools?

Software tools used to design and verify chips.

---

## 🔧 Examples:

* OpenLANE
* OpenROAD
* Magic
* Netgen

---

## 🔧 Tasks performed:

| Task         | Tool Function         |
| ------------ | --------------------- |
| Synthesis    | Convert RTL → netlist |
| Placement    | Place cells           |
| Routing      | Connect wires         |
| Verification | Check correctness     |

---

## 💡 Key Idea:

EDA tools automate chip design

---

---

# 3️⃣ PDK (Process Design Kit)

---

## 📌 What is PDK?

PDK is a collection of files that model the fabrication process.

---

## 💡 Role:

Acts as interface between:

* Designers
* Fabrication (FAB)

---

## 🔧 Contains:

### ✔ Design Rules

* DRC (Design Rule Check)
* LVS (Layout vs Schematic)
* PEX (Parasitic Extraction)

---

### ✔ Device Models

* Transistor behavior

---

### ✔ Standard Cell Libraries

* AND, OR, DFF, etc.

---

### ✔ I/O Libraries

* Pads and interfaces

---

---

## 🔗 Relationship

```text id="rel1"
RTL + EDA Tools + PDK → ASIC
```

---

## 🧠 Open-Source ASIC Ecosystem

---

### 🔹 RTL Designs

* picorv32
* Open cores

---

### 🔹 EDA Tools

* OpenLANE
* OpenROAD

---

### 🔹 PDK

* Sky130 (Google + SkyWater)

---

## 📊 Technology Node (130nm)

---

## 📌 Is 130nm still used?

👉 YES ✅

Used in:

* IoT
* Analog circuits
* Research chips

---

## 📌 Why?

* Low cost
* Mature technology
* Open-source availability

---

---

## ⚡ Performance of 130nm

* Can reach hundreds of MHz
* Even GHz with pipelining

---

---

## 💡 Key Understanding

| Component | Role                |
| --------- | ------------------- |
| RTL       | Design logic        |
| EDA Tools | Implement design    |
| PDK       | Manufacturing rules |

---

---

## 🎯 Interview Questions

### Q1: What are ASIC components?

👉 RTL, EDA tools, PDK

---

### Q2: What is PDK?

👉 Collection of files defining fabrication process

---

### Q3: Why is Sky130 important?

👉 Open-source PDK for learning ASIC design

---

---

## 🚀 Summary

ASIC design is a combination of:

* Design (RTL)
* Tools (EDA)
* Technology (PDK)

👉 Together they create a physical chip

---
