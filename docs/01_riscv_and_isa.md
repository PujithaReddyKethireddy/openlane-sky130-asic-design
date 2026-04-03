# 🧠 RISC-V and Instruction Set Architecture (ISA)

---

## 📌 What is ISA?

Instruction Set Architecture (ISA) is the interface between:

* Software (programs written in C/C++)
* Hardware (CPU implementation)

👉 It defines:

* Instructions
* Registers
* Data types
* Memory access methods

---

## 💡 Simple Understanding

ISA is like a **language**:

* Software writes instructions
* Hardware executes them

---

## 📌 What is RISC-V?

RISC-V is an **open-source ISA** based on RISC principles.

---

## 🔥 Why RISC-V is Important

* Open-source (no licensing cost)
* Modular (can add extensions)
* Simple and efficient
* Widely used in academia & industry

---

## ⚙️ RISC vs CISC

| Feature      | RISC   | CISC    |
| ------------ | ------ | ------- |
| Instructions | Simple | Complex |
| Execution    | Faster | Slower  |
| Example      | RISC-V | x86     |

---

## 🧠 RISC-V Architecture Basics

---

## 🔧 Registers

* 32 general-purpose registers
* Named: x0 → x31

### ⚠️ Special:

* x0 = always 0

---

## 🔧 Instruction Types

### 1️⃣ R-Type (Register)

```c id="r1"
add x5, x1, x2
```

👉 x5 = x1 + x2

---

### 2️⃣ I-Type (Immediate)

```c id="r2"
addi x5, x1, 10
```

---

### 3️⃣ Load/Store

```c id="r3"
lw x1, 0(x2)
sw x1, 0(x2)
```

---

### 4️⃣ Branch

```c id="r4"
beq x1, x2, label
```

---

### 5️⃣ Jump

```c id="r5"
jal x1, label
```

---

## 🔄 Program Execution Flow

```text id="flow_riscv"
C Program
 ↓
Compiler
 ↓
RISC-V Assembly
 ↓
Assembler
 ↓
Binary (Machine Code)
 ↓
CPU executes
```

---

## 🧠 What Happens Inside CPU?

* Instruction Fetch
* Decode
* Execute
* Memory Access
* Write Back

---

## 💡 Example Flow

C Code:

```c id="r6"
a = b + c;
```

Assembly:

```c id="r7"
add x5, x1, x2
```

Binary:

```
0100000...
```

---

## 🔗 Connection to ASIC Design

* RISC-V defines instructions
* RTL implements these instructions
* ASIC flow converts RTL → chip

---

## ⚠️ Important Concepts

* Load-store architecture
* Fixed instruction length
* Register-based operations

---

## 🎯 Interview Questions

### Q1: What is ISA?

👉 Interface between software and hardware

---

### Q2: Why RISC-V?

👉 Open-source, modular, simple

---

### Q3: What is x0 register?

👉 Always zero

---

### Q4: Difference between add and addi?

👉 add = register
👉 addi = immediate value

---

## 🚀 Summary

RISC-V is an open ISA that defines:

* How instructions are written
* How CPU executes them

👉 It is the foundation of hardware design

---
