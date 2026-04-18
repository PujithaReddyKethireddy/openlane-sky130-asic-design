🚀 Day 2 – Floorplanning, Placement & Cell Design (OpenLANE - Sky130)

This day was honestly where things started to feel real.
Till Day 1, everything was more about flow and concepts — but Day 2 is where we actually understand how a chip is physically built and optimized.

🧠 What I Learned Today

Day 2 mainly revolves around three big things:

Floorplanning
Placement (and optimization)
Standard Cell Design & Characterization

And the most important realization:

Everything in ASIC design ultimately depends on standard cells and their characterization (.lib).

🧱 Floorplanning
📍 Core vs Die

At first, I was confused — but this is simple:

Die → entire chip area
Core → where actual logic (standard cells) is placed

All the action happens inside the core.

📊 Utilization

This is one of the most important parameters:

Utilization = Standard Cell Area / Core Area
If too low → wasted silicon
If too high → routing becomes impossible

👉 Sweet spot: ~50–70%

📐 Aspect Ratio

This is just:

Height / Width of the core

But it has a big impact on routing.
A bad ratio can create congestion and longer wires.

🔌 Pin Placement

This part was very interesting.

Inputs should be close to where they are used
Outputs should be near exit
Clock pins → placed very carefully

The clock path should have minimum resistance and delay

⚡ Power Planning

We create a VDD and VSS grid across the chip.

Goal:

Avoid IR drop
Ensure stable power delivery
❌ Good vs Bad Floorplan

A bad floorplan leads to:

Congestion
Long wires
Timing issues

A good one:

Balanced
Clean
Easier to route
📍 Placement

This is where the actual standard cells get placed inside the core.

🧩 Types of Placement
1. Global Placement
Rough placement
Focus on minimizing wirelength
Overlaps allowed
2. Detailed Placement (Legalization)
Remove overlaps
Align cells in rows
Follow design rules
3. Placement Optimization

This is where things get interesting.

⚡ What happens during optimization?
🔹 Buffer Insertion

Long wires = high delay

So we break them using buffers.

🔹 Cell Movement

Cells are moved closer to reduce wirelength.

🔹 Cell Resizing

Increase drive strength when needed.

🚧 Congestion-Aware Placement (RePlAce)

This was a key concept.

Problem:

Too many cells in one area → routing fails

Solution:

Spread cells evenly

Tool used:

RePlAce

It helps in:

Density balancing
Reducing congestion
Improving routability
🔋 Decap Cells

These are used to:

Stabilize power supply
Reduce voltage fluctuations

I didn’t realize earlier how important power stability is — this made it clear.

🔬 Standard Cells

These are the building blocks of everything.

Examples:

Inverter
Buffer
NAND / NOR
Flip-flops
⚙️ Variations in Cells
Size Variants
Bigger → faster
Smaller → less power
Vt Variants
Type	Speed	Leakage
LVT	Fast	High
HVT	Slow	Low

This is a classic tradeoff between speed and power.

🔬 Cell Design Flow

This part connects everything.

📥 Inputs
PDK
DRC rules
LVS rules
SPICE models
⚙️ Steps
Circuit design (transistor level)
Layout design
DRC & LVS checks
Parasitic extraction
Characterization
📤 Outputs
.lib → timing + power
.lef → abstract layout
.gds → final layout
⏱️ Characterization (Most Important Part)

This is where we generate actual data used in the entire flow.

🧪 What we do?
Build a testbench
Apply input signal
Run SPICE simulation
Observe output
📏 Timing Definitions

This part is very important:

20% → 80% → Slew (transition time)
50% → 50% → Propagation delay
⏱️ Propagation Delay
tpd = time(output @ 50%) - time(input @ 50%)

This tells how fast a signal propagates.

⚡ Transition Time (Slew)
Slew = time(80%) - time(20%)

This affects:

Delay
Power
Signal integrity
🔋 Power

Two types:

Dynamic power → switching
Leakage power → static
🔊 Noise

Includes:

Crosstalk
Signal degradation
📦 Final Output → .lib File

This is the most important file.

It contains:

Delay values
Slew values
Power data

And it is used in:

Synthesis
Placement
STA
🔗 Final Understanding

This is what finally clicked for me:

Standard Cell → Characterization → .lib
         ↓
Used everywhere in ASIC flow
🎯 My Key Takeaways
Floorplanning quality directly affects everything later
Placement is not just “placing cells” — it’s optimization
Congestion is a real problem and must be handled early
Characterization is the backbone of timing analysis
.lib file is the most critical output
🚀 What’s Next

Next, I’ll go deeper into:

Timing analysis (setup/hold)
Clock Tree Synthesis (CTS)
Routing
