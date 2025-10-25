# Building a Compact D Latch with Transmission Gate

## Overview
This tutorial will guide you through building the simple D latch from Figure 3.12(a) using discrete MOSFETs and push buttons. You'll experience the two major limitations: **floating output nodes** and **lack of buffers**.

---

## What You'll Need

### Components
- **2× N-channel MOSFETs** (2N7000 or BS170)
- **2× P-channel MOSFETs** (BS250 or similar)
- **2× Push buttons** (momentary, normally open)
- **2× Pull-down resistors** (10kΩ)
- **1× Pull-up resistor** (10kΩ, optional for output observation)
- **1× LED** (any color)
- **1× Current limiting resistor** (220Ω - 1kΩ)
- **Power supply** (5V or use USB power/batteries)
- **Breadboard and jumper wires**

### Optional but Recommended
- Multimeter or logic probe
- Oscilloscope (to see charge leakage over time)

---

## Circuit Description

The transmission gate acts as a **pass gate**:
- When **CLK = 1** and **CLK̄ = 0**: Gate is ON → D flows to Q (transparent)
- When **CLK = 0** and **CLK̄ = 1**: Gate is OFF → Q is isolated (opaque/hold)

### The Transmission Gate
A transmission gate uses both NMOS and PMOS in parallel:
- **NMOS**: Good at passing 0s (low voltages)
- **PMOS**: Good at passing 1s (high voltages)
- **Together**: Can pass both logic levels effectively

---

## Complete Breadboard Circuit

See the detailed SVG circuit diagram below showing all connections with proper MOSFET pinouts:

<svg viewBox="0 0 800 600" xmlns="http://www.w3.org/2000/svg">
  <!-- Title -->
  <text x="400" y="30" text-anchor="middle" font-size="20" font-weight="bold" fill="#333">
    Compact D Latch with Transmission Gate
  </text>
  
  <!-- Power Rail -->
  <line x1="100" y1="60" x2="700" y2="60" stroke="#c00" stroke-width="3"/>
  <text x="50" y="65" font-size="16" font-weight="bold" fill="#c00">+5V</text>
  
  <!-- Ground Rail -->
  <line x1="100" y1="550" x2="700" y2="550" stroke="#333" stroke-width="3"/>
  <text x="50" y="555" font-size="16" font-weight="bold" fill="#333">GND</text>
  
  <!-- D Input Section -->
  <g id="d-input">
    <!-- Button D -->
    <rect x="140" y="60" width="40" height="60" fill="none" stroke="#333" stroke-width="2" rx="5"/>
    <text x="160" y="95" text-anchor="middle" font-size="12" fill="#333">BTN</text>
    <text x="160" y="108" text-anchor="middle" font-size="12" fill="#333">D</text>
    <line x1="160" y1="120" x2="160" y2="160" stroke="#333" stroke-width="2"/>
    
    <!-- Node D -->
    <circle cx="160" cy="160" r="4" fill="#333"/>
    <text x="160" y="145" text-anchor="middle" font-size="16" font-weight="bold" fill="#00c">D</text>
    
    <!-- Pull-down resistor -->
    <line x1="160" y1="160" x2="160" y2="200" stroke="#333" stroke-width="2"/>
    <rect x="150" y="200" width="20" height="60" fill="none" stroke="#333" stroke-width="2"/>
    <text x="160" y="235" text-anchor="middle" font-size="10" fill="#333">10k</text>
    <line x1="160" y1="260" x2="160" y2="280" stroke="#333" stroke-width="2"/>
    <line x1="160" y1="280" x2="160" y2="550" stroke="#333" stroke-width="1" stroke-dasharray="3,3"/>
  </g>
  
  <!-- CLK Input Section -->
  <g id="clk-input">
    <!-- Button CLK -->
    <rect x="340" y="60" width="40" height="60" fill="none" stroke="#333" stroke-width="2" rx="5"/>
    <text x="360" y="95" text-anchor="middle" font-size="12" fill="#333">BTN</text>
    <text x="360" y="108" text-anchor="middle" font-size="12" fill="#333">CLK</text>
    <line x1="360" y1="120" x2="360" y2="160" stroke="#333" stroke-width="2"/>
    
    <!-- Node CLK -->
    <circle cx="360" cy="160" r="4" fill="#333"/>
    <text x="360" y="145" text-anchor="middle" font-size="16" font-weight="bold" fill="#0a0">CLK</text>
    
    <!-- Pull-down resistor -->
    <line x1="360" y1="160" x2="360" y2="200" stroke="#333" stroke-width="2"/>
    <rect x="350" y="200" width="20" height="60" fill="none" stroke="#333" stroke-width="2"/>
    <text x="360" y="235" text-anchor="middle" font-size="10" fill="#333">10k</text>
    <line x1="360" y1="260" x2="360" y2="280" stroke="#333" stroke-width="2"/>
    <line x1="360" y1="280" x2="360" y2="550" stroke="#333" stroke-width="1" stroke-dasharray="3,3"/>
  </g>
  
  <!-- CLK̄ Input Section -->
  <g id="clkbar-input">
    <!-- Button CLK̄ -->
    <rect x="540" y="60" width="40" height="60" fill="none" stroke="#333" stroke-width="2" rx="5"/>
    <text x="560" y="95" text-anchor="middle" font-size="12" fill="#333">BTN</text>
    <text x="560" y="108" text-anchor="middle" font-size="11" fill="#333">CLK̄</text>
    <line x1="560" y1="120" x2="560" y2="160" stroke="#333" stroke-width="2"/>
    
    <!-- Node CLK̄ -->
    <circle cx="560" cy="160" r="4" fill="#333"/>
    <text x="560" y="145" text-anchor="middle" font-size="16" font-weight="bold" fill="#0a0">CLK̄</text>
    
    <!-- Pull-down resistor -->
    <line x1="560" y1="160" x2="560" y2="200" stroke="#333" stroke-width="2"/>
    <rect x="550" y="200" width="20" height="60" fill="none" stroke="#333" stroke-width="2"/>
    <text x="560" y="235" text-anchor="middle" font-size="10" fill="#333">10k</text>
    <line x1="560" y1="260" x2="560" y2="280" stroke="#333" stroke-width="2"/>
    <line x1="560" y1="280" x2="560" y2="550" stroke="#333" stroke-width="1" stroke-dasharray="3,3"/>
  </g>
  
  <!-- Connection from D to transmission gate -->
  <line x1="160" y1="160" x2="260" y2="160" stroke="#00c" stroke-width="2"/>
  <line x1="260" y1="160" x2="260" y2="280" stroke="#00c" stroke-width="2"/>
  
  <!-- Transmission Gate -->
  <g id="transmission-gate">
    <!-- NMOS (2N7000) -->
    <g id="nmos">
      <!-- Drain (top) -->
      <line x1="260" y1="280" x2="290" y2="280" stroke="#00c" stroke-width="2"/>
      <circle cx="260" cy="280" r="3" fill="#00c"/>
      <text x="240" y="285" text-anchor="end" font-size="10" fill="#666">D</text>
      
      <!-- Body/Channel -->
      <line x1="290" y1="270" x2="290" y2="310" stroke="#333" stroke-width="3"/>
      
      <!-- Source (bottom) -->
      <line x1="290" y1="310" x2="320" y2="310" stroke="#c00" stroke-width="2"/>
      <circle cx="320" cy="310" r="3" fill="#c00"/>
      <text x="340" y="315" text-anchor="start" font-size="10" fill="#666">S</text>
      
      <!-- Gate (left side) -->
      <line x1="280" y1="270" x2="280" y2="310" stroke="#333" stroke-width="2"/>
      <line x1="280" y1="290" x2="360" y2="290" stroke="#0a0" stroke-width="2"/>
      <circle cx="280" cy="290" r="3" fill="#0a0"/>
      <text x="270" y="295" text-anchor="end" font-size="10" fill="#666">G</text>
      
      <!-- Label -->
      <text x="290" y="335" text-anchor="middle" font-size="12" fill="#333">NMOS</text>
      <text x="290" y="348" text-anchor="middle" font-size="10" fill="#666">2N7000</text>
    </g>
    
    <!-- PMOS (BS250) -->
    <g id="pmos">
      <!-- Drain (top) -->
      <line x1="420" y1="280" x2="450" y2="280" stroke="#00c" stroke-width="2"/>
      <circle cx="450" cy="280" r="3" fill="#00c"/>
      <text x="470" y="285" text-anchor="start" font-size="10" fill="#666">D</text>
      
      <!-- Body/Channel -->
      <line x1="450" y1="270" x2="450" y2="310" stroke="#333" stroke-width="3"/>
      
      <!-- Source (bottom) -->
      <line x1="420" y1="310" x2="450" y2="310" stroke="#c00" stroke-width="2"/>
      <circle cx="420" cy="310" r="3" fill="#c00"/>
      <text x="400" y="315" text-anchor="end" font-size="10" fill="#666">S</text>
      
      <!-- Gate (right side with bubble for P-channel) -->
      <line x1="460" y1="270" x2="460" y2="310" stroke="#333" stroke-width="2"/>
      <circle cx="465" cy="290" r="5" fill="none" stroke="#333" stroke-width="2"/>
      <line x1="470" y1="290" x2="560" y2="290" stroke="#0a0" stroke-width="2"/>
      <circle cx="470" cy="290" r="3" fill="#0a0"/>
      <text x="480" y="295" text-anchor="start" font-size="10" fill="#666">G</text>
      
      <!-- Label -->
      <text x="450" y="335" text-anchor="middle" font-size="12" fill="#333">PMOS</text>
      <text x="450" y="348" text-anchor="middle" font-size="10" fill="#666">BS250</text>
    </g>
    
    <!-- Connect Sources and Drains together -->
    <line x1="320" y1="310" x2="420" y2="310" stroke="#c00" stroke-width="2"/>
    <line x1="260" y1="280" x2="420" y2="280" stroke="#00c" stroke-width="2"/>
  </g>
  
  <!-- Connection to Q -->
  <line x1="420" y1="310" x2="550" y2="310" stroke="#c00" stroke-width="2"/>
  <circle cx="550" cy="310" r="4" fill="#c00"/>
  <text x="550" y="295" text-anchor="middle" font-size="16" font-weight="bold" fill="#c00">Q</text>
  
  <!-- Optional pull-down on Q -->
  <line x1="550" y1="310" x2="550" y2="350" stroke="#333" stroke-width="2"/>
  <rect x="540" y="350" width="20" height="60" fill="none" stroke="#333" stroke-width="2"/>
  <text x="550" y="385" text-anchor="middle" font-size="10" fill="#333">10k</text>
  <text x="595" y="385" text-anchor="start" font-size="10" fill="#666">(optional)</text>
  <line x1="550" y1="410" x2="550" y2="430" stroke="#333" stroke-width="2"/>
  <line x1="550" y1="430" x2="550" y2="550" stroke="#333" stroke-width="1" stroke-dasharray="3,3"/>
  
  <!-- LED Circuit -->
  <g id="led-circuit">
    <line x1="550" y1="310" x2="650" y2="310" stroke="#c00" stroke-width="2"/>
    
    <!-- LED -->
    <g transform="translate(650, 310)">
      <path d="M 0,-15 L 15,0 L 0,15 Z" fill="none" stroke="#f00" stroke-width="2"/>
      <line x1="-15" y1="-15" x2="-15" y2="15" stroke="#f00" stroke-width="2"/>
      <line x1="-15" y1="0" x2="0" y2="0" stroke="#f00" stroke-width="2"/>
      <line x1="15" y1="0" x2="30" y2="0" stroke="#f00" stroke-width="2"/>
      <text x="0" y="35" text-anchor="middle" font-size="12" fill="#f00">LED</text>
    </g>
    
    <!-- Current limiting resistor -->
    <line x1="680" y1="310" x2="680" y2="350" stroke="#333" stroke-width="2"/>
    <rect x="670" y="350" width="20" height="60" fill="none" stroke="#333" stroke-width="2"/>
    <text x="680" y="385" text-anchor="middle" font-size="10" fill="#333">220Ω</text>
    <line x1="680" y1="410" x2="680" y2="430" stroke="#333" stroke-width="2"/>
    <line x1="680" y1="430" x2="680" y2="550" stroke="#333" stroke-width="1" stroke-dasharray="3,3"/>
  </g>
  
  <!-- Labels and annotations -->
  <text x="400" y="580" text-anchor="middle" font-size="14" fill="#666" font-style="italic">
    Press CLK and CLK̄ alternately (one high, one low)
  </text>
  
  <!-- Legend -->
  <g id="legend" transform="translate(20, 420)">
    <text x="0" y="0" font-size="14" font-weight="bold" fill="#333">Operation:</text>
    <text x="0" y="20" font-size="12" fill="#333">CLK=1, CLK̄=0 → Transparent (D flows to Q)</text>
    <text x="0" y="40" font-size="12" fill="#333">CLK=0, CLK̄=1 → Opaque (Q holds value)</text>
    <text x="0" y="65" font-size="11" font-weight="bold" fill="#666">Pin Labels: G=Gate, D=Drain, S=Source</text>
  </g>
</svg>

**Pin Connections Summary:**
- **D Input**: Button to +5V, 10kΩ pull-down to GND
- **CLK Input**: Button to +5V, 10kΩ pull-down to GND  
- **CLK̄ Input**: Button to +5V, 10kΩ pull-down to GND (press when CLK is released)
- **NMOS (2N7000)**: Gate→CLK, Drain→D, Source→Q
- **PMOS (BS250)**: Gate→CLK̄, Drain→D, Source→Q
- **Q Output**: Optional 10kΩ pull-down, LED through 220Ω to GND

The diagram shows all three pins (G, D, S) for each MOSFET clearly labeled.

---

## Step-by-Step Build

### Step 1: Set Up Power Rails
1. Connect +5V and GND rails on your breadboard
2. Double-check polarity with a multimeter

### Step 2: Build the D Input (Data Button)
1. Connect one side of Button D to +5V
2. Connect the other side to a node we'll call "D"
3. Add a 10kΩ pull-down resistor from D to GND
4. **Result**: Pressing button → D = 1, releasing → D = 0

### Step 3: Build the CLK Input (Clock Button)
1. Connect one side of Button CLK to +5V
2. Connect the other side to a node we'll call "CLK"
3. Add a 10kΩ pull-down resistor from CLK to GND
4. **Result**: Pressing button → CLK = 1, releasing → CLK = 0

### Step 4: Create CLK̄ (Inverted Clock)
For this simple demo, **manually control CLK̄**:
- When CLK button is pressed: Connect CLK̄ to GND (0)
- When CLK button is released: Connect CLK̄ to +5V (1)

*Alternative: Use a NOT gate (like 74HC04) or a simple NMOS inverter*

### Step 5: Build the Transmission Gate
1. Place NMOS (T1) and PMOS (T2) side by side
2. Connect the **Sources/Drains**:
   - Connect D input to one end of both transistors (in parallel)
   - Connect Q output node to the other end of both transistors
3. Connect the **Gates**:
   - NMOS gate to CLK
   - PMOS gate to CLK̄

### Step 6: Add Output Indicator
1. Connect LED cathode (short leg) to Q node
2. Connect LED anode (long leg) through 220Ω resistor to +5V
3. *Note: LED will light when Q is LOW (sinking current)*

Alternatively, for active-high indication:
- Connect LED anode to Q
- Connect LED cathode through resistor to GND

### Step 7: Optional Pull-down on Q
Add a 10kΩ resistor from Q to GND to help observe floating behavior

---

## Testing & Experiencing the Limitations

### Basic Operation Test
1. **Set D = 0** (button released)
2. **Press CLK** (CLK = 1, CLK̄ = 0) → Transparent mode
3. **Observe Q = 0** (LED state)
4. **Release CLK** (CLK = 0, CLK̄ = 1) → Opaque mode
5. **Press D button** (D = 1)
6. **Q should remain at 0** (latched)
7. **Press CLK again** → Q should now follow D and become 1
8. **Release CLK** → Q should stay at 1

### Limitation 1: Floating Output Node

**Experiment A - Charge Leakage**
1. Set D = 1, press CLK to load a HIGH into Q
2. Release CLK (Q is now isolated)
3. **Remove the pull-down resistor** if present
4. **Wait and observe Q over time** (use multimeter)
   - Q voltage will gradually decay
   - Leakage currents discharge the floating node
   - LED may dim or change state unexpectedly

**Experiment B - Noise Sensitivity**
1. Load Q = 1, enter opaque mode (CLK = 0)
2. **Touch Q node with your finger** or bring your hand near
3. Body capacitance and EMI can change Q's state!
4. Try waving a phone or other electronic device near Q

### Limitation 2: No Buffers

**Experiment C - Backward Drive (nMOS path)**
1. Load Q = 1, enter opaque mode
2. **Touch D input node** or connect it briefly to GND
3. If there's enough coupling or you force D LOW:
   - Noise can conduct through the symmetric transmission gate
   - You might see Q get disturbed
4. **The transmission gate is bidirectional** - current can flow both ways

**Experiment D - Threshold Voltage Issues**
1. Load Q = 1 (press D, press CLK, release CLK)
2. Measure voltage at Q with multimeter
3. You may find Q is slightly below VDD (like 4.3V instead of 5V)
4. This is because NMOS can't pass a full HIGH (loses Vth)
5. PMOS helps but the gate isn't perfect

**Experiment E - External Load Effect**
1. Load Q = 1, enter opaque mode
2. Connect a 1kΩ resistor from Q to GND momentarily
3. The floating node Q will quickly discharge
4. Remove resistor - Q stays LOW even though you latched a HIGH
5. **A proper latch would drive Q strongly and resist this**

---

## What You've Learned

### Floating Nodes are Problematic
- Without active drive, Q loses its state to leakage
- Real circuits need the full latch with cross-coupled inverters

### Buffers are Essential
- Neither D nor Q should be exposed to the outside world
- Input buffers protect D from backward drive
- Output buffers actively drive Q and isolate the storage node

### Why Commercial ICs Don't Use This Design
This compact latch is **too fragile** for real use:
- Noise immunity is poor
- State retention is unreliable
- Cannot drive significant loads

The full D latch in Figure 3.12(b) adds:
- Input inverters to buffer D
- Cross-coupled inverters for stable state storage
- Output buffers for strong drive capability

---

## Next Steps

1. **Build the full latch** from Figure 3.12(b) and compare behavior
2. **Add a NOT gate** to properly generate CLK̄
3. **Build a D flip-flop** using two latches (master-slave configuration)
4. **Measure charge decay** with an oscilloscope over seconds/minutes

---

## Safety Notes
- MOSFET gates are ESD-sensitive - handle carefully
- Never exceed component voltage ratings
- Double-check power connections before applying power
- Use current limiting resistors with LEDs

---

**Happy experimenting! You're now experiencing firsthand why real digital circuits need proper buffering and why transmission gates alone aren't enough for reliable state storage.**
