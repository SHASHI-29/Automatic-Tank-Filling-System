# ⚙️ Procedure – Automatic Tank Filling System (LabVIEW)

This document explains the **step-by-step procedure** to create and test the **Automatic Tank Filling Simulation** in **NI LabVIEW**.

---

## 🖥️ 1. Front Panel Design
1. **Open a New VI** → Switch to the *Front Panel*.
2. **Add Tank Indicators**
   - Controls → Modern → Numeric → **Tank** → place two tanks.
   - Label them as **Tank** and **Tank 2**.
   - Set range (0–10 units).
3. **Add Sliders & Controls**
   - **Flow Rate Slider** → to control water inflow.
   - **Threshold Slider** → to set the level at which the valve opens.
4. **Add Indicators**
   - **Valve (ON/OFF LED)** → Boolean indicator.
   - **Tank Full LED** → Boolean indicator for Tank 2 full condition.
   - **Emergency Stop** → Stop button for halting the simulation.
5. **Organize & Label**
   - Arrange controls neatly.
   - Optionally add decorations (pipes, text) for better visuals.

---

## 🔗 2. Block Diagram Logic
1. **Add While Loop**
   - Place a While Loop around all logic (Functions → Structures → While Loop).
   - Add **Shift Registers** for Tank1 and Tank2 levels (initialize to 0).
2. **Set Time Base**
   - Insert **Wait (ms)** = 100 → defines simulation step time (dt = 0.1s).
3. **Inflow Calculation**
   - `inflow_delta = FlowRate × dt`.
   - Add this to Tank1 each loop.
4. **Valve Condition**
   - If `Tank1 ≥ Threshold` → Valve = ON.
   - Wire result to **Valve LED**.
5. **Transfer Flow**
   - When valve is ON → `transfer_delta = FlowRate × dt` (or fixed constant).
   - Subtract from Tank1, add to Tank2.
6. **Clamp Levels**
   - Keep Tank values within [0, 10] using **In Range and Coerce**.
7. **Tank Full Logic**
   - If `Tank2 ≥ 10` → Turn ON **Tank Full LED** and stop further inflow.
8. **Emergency Stop**
   - Wire Stop button to While Loop conditional terminal → stops the simulation.

---

## ▶️ 3. Running the VI
1. Set **Flow Rate** and **Threshold** sliders.
2. Click **Run**.
3. Observe:
   - Tank1 fills with water.
   - When it reaches threshold → Valve opens → Tank2 fills.
   - When Tank2 reaches full → Tank Full LED lights up.
   - Press **Stop** at any time to end the program.

