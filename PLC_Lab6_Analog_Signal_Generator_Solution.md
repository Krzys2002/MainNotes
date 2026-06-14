# PLC Lab 6 — Analog Signal Generator: Complete Solution Guide

**Platform:** Siemens S7-1200 (CPU 1214C DC/DC/DC) with Signal Board SB 1232 AQ  
**Environment:** TIA Portal, Structured Text (SCL)  
**Lab source:** Poznań University of Technology — Digital Controllers and PLC

---

## Overview of the Three Tasks

| Task | Objective |
|------|-----------|
| 1. Configuration and Testing of the DAC Channel | Configure the SB 1232 AQ, verify range, resolution, and dynamics |
| 2. Sawtooth Wave Generator | Generate a rising sawtooth using a 20 ms cyclic interrupt |
| 3. Tunable Generator | Full generator with 4 waveform shapes, adjustable period/amplitude/offset |

---

## Key Technical Reference

Before writing any code, internalize these hardware facts — they drive every scaling decision.

| Parameter | Value |
|-----------|-------|
| DAC module | SB 1232 AQ 1×12 bit |
| DAC output address | **QW80** (AQ0) |
| DAC voltage range | **±10 V** |
| DAC data word range | **−27648 to +27648** (signed integer in a 16-bit word) |
| DAC resolution | 12 bits (voltage mode) |
| DAC settling time | ~300 µs (resistive load) |
| ADC input addresses | IW64 (AI0), IW66 (AI1) |
| ADC input range | 0–10 V → 0–27648 |
| ADC resolution | 10 bits |
| Internal signal range (this lab) | **−100.0 to +100.0** (Real) |
| Scaling factor | **276.48** (i.e. 27648 ÷ 100.0) |
| Voltage mapping | Internal 100.0 = 10 V physical |

---

## TASK 1 — Configuration and Testing of the DAC Channel

### Step 1.1 — Create the TIA Portal Project

1. Launch TIA Portal. Select **Create new project**, name it (e.g., `Lab6_Generator`).
2. Select **Add new device** → Controllers → SIMATIC S7-1200 → **CPU 1214C DC/DC/DC** (order number **6ES7 214-1AG31-0XB0**). Choose the firmware version matching your physical unit.
3. Click **OK** to enter the project view.

### Step 1.2 — Add the Signal Board SB 1232 AQ

1. Open **Device configuration** (double-click the CPU in the project tree).
2. In the Device View, locate the **Signal Board slot** — the small rectangular slot on top of the CPU graphic.
3. In the **Hardware Catalog** panel on the right, navigate to:  
   `Signal boards → AQ → SB 1232 → 6ES7 232-4HA30-0XB0`
4. Drag it into the Signal Board slot.
5. Double-click the newly added SB 1232 to open its **Properties**.
6. Under **Channel 0**, set:
   - Output type: **Voltage**
   - Output range: **±10 V**
7. **Compile** the hardware configuration (Ctrl+B) and **Download** it to the PLC.

### Step 1.3 — Wire the Grounds on the Workstation

On the physical educational workstation:

1. **Analog output ground:** Connect the **0M** terminal of the SB 1232 AQ module (the ground pin next to the AQ0 output) to the controller's common ground terminal (black "M" connector on the terminal board).
2. **Digital input ground:** Connect the **1M** terminal (digital input common) to the controller's **N potential** (the black ground rail). This is required for the digital inputs used in Tasks 2 and 3.

Without these connections, the analog output will float and the digital inputs will not register.

### Step 1.4 — Define the PLC Tag Table

Open **PLC tags → Default tag table** and create:

| Name | Data type | Address | Comment |
|------|-----------|---------|---------|
| `AnalogOutput` | Int | QW80 | DAC output – SB 1232 AQ channel 0 |

Using an `Int` tag at `QW80` lets you write signed values (−27648 to +27648) directly, without needing `INT_TO_WORD` conversion. The PLC handles the two's-complement encoding automatically.

### Step 1.5 — Write a Test Program in OB1 (Main)

Create a simple SCL program in OB1 that writes constant values to the analog output:

```pascal
// === OB1 [Main] — DAC Test Program ===
// Change the constant below, download, and measure with multimeter/oscilloscope.

"AnalogOutput" := 27648;    // Expected: +10.0 V
// "AnalogOutput" := 13824;  // Expected: +5.0 V
// "AnalogOutput" := 0;      // Expected:  0.0 V
// "AnalogOutput" := -13824; // Expected: -5.0 V
// "AnalogOutput" := -27648; // Expected: -10.0 V
// "AnalogOutput" := 1;      // Expected: +361.7 µV (tests resolution)
```

### Step 1.6 — Perform the Measurements

Download, go online, and run the program. For each test value:

**Range test:** Set the output to 27648, 0, and −27648 in turn. Measure with a **multimeter** on the AQ0 output terminal (green connector). Verify you get approximately +10 V, 0 V, and −10 V.

**Resolution test:** Set the output to 1. The multimeter should read roughly 362 µV (= 10 V ÷ 27648). This confirms single-LSB resolution. Try value 2, expect ~723 µV.

**Dynamic test:** Modify the program to alternate between 0 and 27648 on each scan cycle, and observe the step response on the **oscilloscope**. You should see the settling time of approximately 300 µs (per the SB 1232 datasheet). This establishes the maximum useful update rate for signal generation.

**Linearity spot-check:** Test a few midrange values (e.g., 13824 → 5.0 V, 20736 → 7.5 V) and confirm the output tracks linearly.

---

## TASK 2 — Sawtooth Wave Generator

### Step 2.1 — Understand the Architecture

The lab requires two separate cyclic interrupt OBs:

| OB | Cycle time | Purpose |
|----|-----------|---------|
| `OB_Generator` | **20 ms** | Signal computation and DAC output (time-critical) |
| `OB_InputHandler` | **250 ms** | Reading digital inputs and adjusting parameters (human-speed) |

This separation is important: signal generation needs a fixed, fast sample rate for waveform quality. Input handling is slow (button presses) and would waste resources at 20 ms.

### Step 2.2 — Create the Global Data Block

Add a new **Global Data Block** named `DB_GenParams`. Define these variables:

| Name | Data type | Initial value | Purpose |
|------|-----------|---------------|---------|
| `Period` | Real | 1.0 | Signal period in seconds (valid range: 0.1 to 10.0) |
| `Amplitude` | Real | 100.0 | Peak amplitude in internal units (0.0 to 100.0; 100.0 = 10 V) |
| `Phase` | Real | 0.0 | Phase accumulator, ranges from 0.0 to 1.0 |
| `SignalOut` | Real | 0.0 | Final signal value after scaling and clamping (−100.0 to +100.0) |

> **Why a Global DB and not OB-Static variables?**  
> The `Phase` variable **must persist** between 20 ms calls. While some TIA Portal versions support Static sections in OBs, using a Global DB is universally reliable and makes the data accessible from other blocks (useful for debugging via Watch Tables).

### Step 2.3 — Create the Cyclic Interrupt OB for Signal Generation

1. Go to **Program blocks → Add new block → Organization Block**.
2. Select type: **Cyclic interrupt**.
3. Name: `OB_Generator`.
4. Language: **SCL**.
5. In the OB properties, set the **Cycle time** to **20000 µs** (= 20 ms).

### Step 2.4 — The Phase Accumulator Algorithm (Core Concept)

The phase accumulator is the heart of this generator. It works as follows:

- Maintain a variable `Phase` that represents the current position within one cycle, normalized to the range [0.0, 1.0).
- Every 20 ms, increment it by: `PhaseIncrement = CycleTime / Period`
- When `Phase` reaches or exceeds 1.0, subtract 1.0 (do **not** reset to 0.0).

**Why subtract instead of reset?** Consider a period of 0.15 s. Each 20 ms step adds 0.02 / 0.15 = 0.1333... to the phase. After 7 steps the phase is 0.9333, and after step 8 it becomes 1.0666. If you reset to 0.0, you lose the 0.0666 fractional remainder, causing a systematic period error that accumulates over time. By subtracting 1.0, you carry the remainder forward (Phase becomes 0.0666), and the average period remains correct even when it's not a multiple of 20 ms.

**Why a simple `IF` suffices (no `WHILE` loop needed):** The maximum phase increment occurs at the minimum period: 0.02 / 0.1 = 0.2. Since this is always less than 1.0, the phase can never jump past 1.0 by more than one full cycle in a single step. A single `IF` check is therefore sufficient.

### Step 2.5 — Write the Sawtooth Generator Code

```pascal
// =====================================================
// OB_Generator [Cyclic Interrupt, 20 ms]
// Rising sawtooth signal generation
// =====================================================

// --- Constants ---
#CYCLE_TIME_S    := 0.02;       // 20 ms expressed in seconds
#DAC_SCALE       := 276.48;     // 27648 / 100.0 — maps internal ±100 to DAC ±27648

// --- Phase accumulation ---
#phaseIncrement := #CYCLE_TIME_S / "DB_GenParams".Period;
"DB_GenParams".Phase := "DB_GenParams".Phase + #phaseIncrement;

// Wrap phase — preserve fractional remainder for period accuracy
IF "DB_GenParams".Phase >= 1.0 THEN
    "DB_GenParams".Phase := "DB_GenParams".Phase - 1.0;
END_IF;

// --- Rising sawtooth waveform ---
// Phase 0.0 → −Amplitude (minimum)
// Phase ~1.0 → +Amplitude (maximum, then drops back)
"DB_GenParams".SignalOut :=
    (2.0 * "DB_GenParams".Phase - 1.0) * "DB_GenParams".Amplitude;

// --- Clamp to internal range ---
IF "DB_GenParams".SignalOut > 100.0 THEN
    "DB_GenParams".SignalOut := 100.0;
ELSIF "DB_GenParams".SignalOut < -100.0 THEN
    "DB_GenParams".SignalOut := -100.0;
END_IF;

// --- Scale to DAC and write to output ---
#dacValue := REAL_TO_INT("DB_GenParams".SignalOut * #DAC_SCALE);

// Safety clamp (should be redundant, but protects the hardware)
IF #dacValue > 27648 THEN
    #dacValue := 27648;
ELSIF #dacValue < -27648 THEN
    #dacValue := -27648;
END_IF;

"AnalogOutput" := #dacValue;
```

**Temporary variable declarations** (in the OB's Temp interface section):

| Name | Data type |
|------|-----------|
| `CYCLE_TIME_S` | Real |
| `DAC_SCALE` | Real |
| `phaseIncrement` | Real |
| `dacValue` | Int |

### Step 2.6 — Create the Input Handler OB

1. Add another **Cyclic Interrupt OB**, name it `OB_InputHandler`, cycle time **250000 µs** (250 ms), language SCL.
2. For Task 2, a minimal version handles period and amplitude adjustment only.

First, extend `DB_GenParams` with edge-detection memory variables:

| Name | Data type | Initial value |
|------|-----------|---------------|
| `prevPeriodUp` | Bool | FALSE |
| `prevPeriodDown` | Bool | FALSE |
| `prevAmpUp` | Bool | FALSE |
| `prevAmpDown` | Bool | FALSE |

Then define additional PLC tags for the digital inputs:

| Name | Data type | Address | Comment |
|------|-----------|---------|---------|
| `BtnPeriodUp` | Bool | I0.2 | Increase period (rising edge) |
| `BtnPeriodDown` | Bool | I0.3 | Decrease period (rising edge) |
| `BtnAmpUp` | Bool | I0.4 | Increase amplitude (rising edge) |
| `BtnAmpDown` | Bool | I0.5 | Decrease amplitude (rising edge) |

```pascal
// =====================================================
// OB_InputHandler [Cyclic Interrupt, 250 ms]
// Read digital inputs, adjust generator parameters
// =====================================================

#PERIOD_STEP := 0.1;       // seconds per button press
#AMPLITUDE_STEP := 10.0;   // internal units per press (= 1.0 V)

// --- Period adjustment (manual rising-edge detection) ---
IF "BtnPeriodUp" AND NOT "DB_GenParams".prevPeriodUp THEN
    "DB_GenParams".Period := "DB_GenParams".Period + #PERIOD_STEP;
END_IF;
IF "BtnPeriodDown" AND NOT "DB_GenParams".prevPeriodDown THEN
    "DB_GenParams".Period := "DB_GenParams".Period - #PERIOD_STEP;
END_IF;
// Store current state for next edge detection
"DB_GenParams".prevPeriodUp   := "BtnPeriodUp";
"DB_GenParams".prevPeriodDown := "BtnPeriodDown";

// Clamp period to valid range
IF "DB_GenParams".Period < 0.1 THEN
    "DB_GenParams".Period := 0.1;
ELSIF "DB_GenParams".Period > 10.0 THEN
    "DB_GenParams".Period := 10.0;
END_IF;

// --- Amplitude adjustment ---
IF "BtnAmpUp" AND NOT "DB_GenParams".prevAmpUp THEN
    "DB_GenParams".Amplitude := "DB_GenParams".Amplitude + #AMPLITUDE_STEP;
END_IF;
IF "BtnAmpDown" AND NOT "DB_GenParams".prevAmpDown THEN
    "DB_GenParams".Amplitude := "DB_GenParams".Amplitude - #AMPLITUDE_STEP;
END_IF;
"DB_GenParams".prevAmpUp   := "BtnAmpUp";
"DB_GenParams".prevAmpDown := "BtnAmpDown";

// Clamp amplitude to valid range
IF "DB_GenParams".Amplitude < 0.0 THEN
    "DB_GenParams".Amplitude := 0.0;
ELSIF "DB_GenParams".Amplitude > 100.0 THEN
    "DB_GenParams".Amplitude := 100.0;
END_IF;
```

> **Why manual edge detection instead of R_TRIG?**  
> The `R_TRIG` function block requires a persistent instance (static variable). Whether an OB supports static variables depends on the TIA Portal version and CPU firmware. Storing previous-state booleans in the Global DB is universally reliable, easy to debug in a Watch Table, and functionally identical to `R_TRIG`.

### Step 2.7 — Verify with Oscilloscope

1. Download and run.
2. Connect the oscilloscope to the **AQ0** output terminal (green connector) and ground.
3. Set the oscilloscope timebase to show 2–3 full periods (e.g., 500 ms/div for a 1 s period).
4. You should see a clean rising sawtooth ramp.
5. Verify the period: measure peak-to-peak time with oscilloscope cursors. It should match your `Period` setting.
6. Verify the amplitude: the signal should swing from approximately −10 V to +10 V at Amplitude = 100.0.
7. Press the period/amplitude buttons and confirm the waveform updates accordingly.
8. Test a period that is NOT a multiple of 20 ms (e.g., 0.15 s or 0.3 s) and confirm the waveform still has the correct average period — this validates your phase-remainder logic.

---

## TASK 3 — Tunable Generator (Full Program)

Task 3 extends the sawtooth generator into a complete, multi-waveform function generator with adjustable period, amplitude, and DC offset. The four waveforms required by the overall lab goal are: **sawtooth, triangular, sinusoidal, and rectangular (square)**.

### Step 3.1 — Extend the Global Data Block

Add these variables to `DB_GenParams`:

| Name | Data type | Initial value | Purpose |
|------|-----------|---------------|---------|
| `Shape` | Int | 1 | Waveform: 1=Sawtooth, 2=Triangle, 3=Sine, 4=Square |
| `Offset` | Real | 0.0 | DC offset in internal units (−100.0 to +100.0; 10.0 = 1 V) |
| `prevOffsetUp` | Bool | FALSE | Edge detection memory for offset increase button |
| `prevOffsetDown` | Bool | FALSE | Edge detection memory for offset decrease button |

### Step 3.2 — Add Remaining PLC Tags

| Name | Data type | Address | Comment |
|------|-----------|---------|---------|
| `BtnShapeBit0` | Bool | I0.0 | Waveform shape selector — bit 0 |
| `BtnShapeBit1` | Bool | I0.1 | Waveform shape selector — bit 1 |
| `BtnPeriodUp` | Bool | I0.2 | Increase period (rising edge) |
| `BtnPeriodDown` | Bool | I0.3 | Decrease period (rising edge) |
| `BtnAmpUp` | Bool | I0.4 | Increase amplitude (rising edge) |
| `BtnAmpDown` | Bool | I0.5 | Decrease amplitude (rising edge) |
| `BtnOffsetUp` | Bool | I0.6 | Increase DC offset (rising edge) |
| `BtnOffsetDown` | Bool | I0.7 | Decrease DC offset (rising edge) |
| `AnalogOutput` | Int | QW80 | DAC output (SB 1232 AQ) |

### Step 3.3 — Waveform Shape Selection Encoding

Two digital inputs encode the shape as a 2-bit value:

| I0.1 | I0.0 | Shape code | Waveform |
|------|------|------------|----------|
| 0 | 0 | 1 | Sawtooth (default) |
| 0 | 1 | 2 | Triangle |
| 1 | 0 | 3 | Sine |
| 1 | 1 | 4 | Square |

The encoding is read in the 250 ms input handler and stored in `DB_GenParams.Shape`. The 20 ms generator reads this value on every cycle and computes the appropriate waveform.

### Step 3.4 — Waveform Mathematics

All four waveforms are computed from the same `Phase` accumulator (0.0 to 1.0):

**Sawtooth (rising):**  
Linearly ramps from −A to +A, then drops back.
```
signal = (2 × Phase − 1) × Amplitude
```

**Triangle:**  
Ramps up from −A to +A in the first half-cycle, then back down to −A in the second.
```
IF Phase < 0.5 THEN
    signal = (4 × Phase − 1) × Amplitude
ELSE
    signal = (3 − 4 × Phase) × Amplitude
```
Verification: Phase=0 → (0−1)×A = −A ✓, Phase=0.25 → (1−1)×A = 0 ✓, Phase=0.5 → (2−1)×A = +A ✓, Phase=0.75 → (3−3)×A = 0 ✓, Phase→1.0 → (3−4)×A = −A ✓.

**Sine:**  
Standard sinusoidal waveform.
```
signal = Amplitude × SIN(2π × Phase)
```

**Square:**  
Full amplitude in the first half-cycle, negative in the second (50% duty cycle).
```
IF Phase < 0.5 THEN signal = +Amplitude
ELSE signal = −Amplitude
```

### Step 3.5 — Complete Generator OB Code (Replaces the Task 2 Version)

```pascal
// =====================================================
// OB_Generator [Cyclic Interrupt, 20 ms]
// Multi-waveform signal generator
// =====================================================

// --- Constants ---
#CYCLE_TIME_S := 0.02;         // 20 ms in seconds
#DAC_SCALE    := 276.48;       // 27648 / 100.0
#TWO_PI       := 6.2831853;    // 2 × π

// --- Phase accumulation ---
#phaseIncrement := #CYCLE_TIME_S / "DB_GenParams".Period;
"DB_GenParams".Phase := "DB_GenParams".Phase + #phaseIncrement;

IF "DB_GenParams".Phase >= 1.0 THEN
    "DB_GenParams".Phase := "DB_GenParams".Phase - 1.0;
END_IF;

// --- Waveform computation ---
CASE "DB_GenParams".Shape OF

    1:  // Sawtooth (rising)
        #rawSignal := (2.0 * "DB_GenParams".Phase - 1.0)
                      * "DB_GenParams".Amplitude;

    2:  // Triangle
        IF "DB_GenParams".Phase < 0.5 THEN
            #rawSignal := (4.0 * "DB_GenParams".Phase - 1.0)
                          * "DB_GenParams".Amplitude;
        ELSE
            #rawSignal := (3.0 - 4.0 * "DB_GenParams".Phase)
                          * "DB_GenParams".Amplitude;
        END_IF;

    3:  // Sine
        #rawSignal := "DB_GenParams".Amplitude
                      * SIN(#TWO_PI * "DB_GenParams".Phase);

    4:  // Square (50% duty cycle)
        IF "DB_GenParams".Phase < 0.5 THEN
            #rawSignal := "DB_GenParams".Amplitude;
        ELSE
            #rawSignal := -"DB_GenParams".Amplitude;
        END_IF;

    ELSE  // Fallback: treat unknown shape as sawtooth
        #rawSignal := (2.0 * "DB_GenParams".Phase - 1.0)
                      * "DB_GenParams".Amplitude;

END_CASE;

// --- Apply DC offset ---
"DB_GenParams".SignalOut := #rawSignal + "DB_GenParams".Offset;

// --- Clamp to internal range (±100.0) ---
IF "DB_GenParams".SignalOut > 100.0 THEN
    "DB_GenParams".SignalOut := 100.0;
ELSIF "DB_GenParams".SignalOut < -100.0 THEN
    "DB_GenParams".SignalOut := -100.0;
END_IF;

// --- Scale internal → DAC and write output ---
#dacValue := REAL_TO_INT("DB_GenParams".SignalOut * #DAC_SCALE);

IF #dacValue > 27648 THEN
    #dacValue := 27648;
ELSIF #dacValue < -27648 THEN
    #dacValue := -27648;
END_IF;

"AnalogOutput" := #dacValue;
```

**Temp variables for this OB:**

| Name | Data type |
|------|-----------|
| `CYCLE_TIME_S` | Real |
| `DAC_SCALE` | Real |
| `TWO_PI` | Real |
| `phaseIncrement` | Real |
| `rawSignal` | Real |
| `dacValue` | Int |

### Step 3.6 — Complete Input Handler OB Code

```pascal
// =====================================================
// OB_InputHandler [Cyclic Interrupt, 250 ms]
// Reads digital inputs, adjusts all generator parameters
// =====================================================

#PERIOD_STEP    := 0.1;     // seconds per press
#AMPLITUDE_STEP := 10.0;    // internal units per press (= 1.0 V)
#OFFSET_STEP    := 10.0;    // internal units per press (= 1.0 V)

// -------------------------------------------------------
// SHAPE SELECTION (combinational — no edge detection needed)
// I0.0 and I0.1 encode the shape as a 2-bit selector
// -------------------------------------------------------
IF NOT "BtnShapeBit1" AND NOT "BtnShapeBit0" THEN
    "DB_GenParams".Shape := 1;   // Sawtooth
ELSIF NOT "BtnShapeBit1" AND "BtnShapeBit0" THEN
    "DB_GenParams".Shape := 2;   // Triangle
ELSIF "BtnShapeBit1" AND NOT "BtnShapeBit0" THEN
    "DB_GenParams".Shape := 3;   // Sine
ELSE
    "DB_GenParams".Shape := 4;   // Square
END_IF;

// -------------------------------------------------------
// PERIOD ADJUSTMENT (rising-edge triggered)
// -------------------------------------------------------
IF "BtnPeriodUp" AND NOT "DB_GenParams".prevPeriodUp THEN
    "DB_GenParams".Period := "DB_GenParams".Period + #PERIOD_STEP;
END_IF;
IF "BtnPeriodDown" AND NOT "DB_GenParams".prevPeriodDown THEN
    "DB_GenParams".Period := "DB_GenParams".Period - #PERIOD_STEP;
END_IF;
"DB_GenParams".prevPeriodUp   := "BtnPeriodUp";
"DB_GenParams".prevPeriodDown := "BtnPeriodDown";

IF "DB_GenParams".Period < 0.1 THEN
    "DB_GenParams".Period := 0.1;
ELSIF "DB_GenParams".Period > 10.0 THEN
    "DB_GenParams".Period := 10.0;
END_IF;

// -------------------------------------------------------
// AMPLITUDE ADJUSTMENT (rising-edge triggered)
// -------------------------------------------------------
IF "BtnAmpUp" AND NOT "DB_GenParams".prevAmpUp THEN
    "DB_GenParams".Amplitude := "DB_GenParams".Amplitude + #AMPLITUDE_STEP;
END_IF;
IF "BtnAmpDown" AND NOT "DB_GenParams".prevAmpDown THEN
    "DB_GenParams".Amplitude := "DB_GenParams".Amplitude - #AMPLITUDE_STEP;
END_IF;
"DB_GenParams".prevAmpUp   := "BtnAmpUp";
"DB_GenParams".prevAmpDown := "BtnAmpDown";

IF "DB_GenParams".Amplitude < 0.0 THEN
    "DB_GenParams".Amplitude := 0.0;
ELSIF "DB_GenParams".Amplitude > 100.0 THEN
    "DB_GenParams".Amplitude := 100.0;
END_IF;

// -------------------------------------------------------
// OFFSET ADJUSTMENT (rising-edge triggered)
// -------------------------------------------------------
IF "BtnOffsetUp" AND NOT "DB_GenParams".prevOffsetUp THEN
    "DB_GenParams".Offset := "DB_GenParams".Offset + #OFFSET_STEP;
END_IF;
IF "BtnOffsetDown" AND NOT "DB_GenParams".prevOffsetDown THEN
    "DB_GenParams".Offset := "DB_GenParams".Offset - #OFFSET_STEP;
END_IF;
"DB_GenParams".prevOffsetUp   := "BtnOffsetUp";
"DB_GenParams".prevOffsetDown := "BtnOffsetDown";

IF "DB_GenParams".Offset < -100.0 THEN
    "DB_GenParams".Offset := -100.0;
ELSIF "DB_GenParams".Offset > 100.0 THEN
    "DB_GenParams".Offset := 100.0;
END_IF;
```

**Temp variables for this OB:**

| Name | Data type |
|------|-----------|
| `PERIOD_STEP` | Real |
| `AMPLITUDE_STEP` | Real |
| `OFFSET_STEP` | Real |

### Step 3.7 — OB1 (Main)

OB1 can remain empty or be used for optional diagnostics. The signal generation and input handling run entirely in their respective cyclic interrupt OBs, which execute independently of the main scan cycle.

```pascal
// =====================================================
// OB1 [Main] — intentionally minimal
// All signal generation occurs in OB_Generator (20 ms).
// All input handling occurs in OB_InputHandler (250 ms).
// =====================================================

// Optional: display current parameters for debugging.
// Open a Watch Table and monitor DB_GenParams variables instead.
```

---

## Complete Data Block Definition

Here is the final `DB_GenParams` Global Data Block with all variables:

```
DB_GenParams [Global DB]

    // === Signal Parameters ===
    Period          : Real   := 1.0       // Signal period in seconds [0.1 .. 10.0]
    Amplitude       : Real   := 100.0     // Peak amplitude, internal units [0.0 .. 100.0]
    Offset          : Real   := 0.0       // DC offset, internal units [-100.0 .. 100.0]
    Shape           : Int    := 1         // Waveform shape [1=Saw, 2=Tri, 3=Sin, 4=Sqr]

    // === Internal State ===
    Phase           : Real   := 0.0       // Phase accumulator [0.0 .. 1.0)
    SignalOut        : Real   := 0.0       // Final output signal [-100.0 .. 100.0]

    // === Edge Detection Memory (for InputHandler) ===
    prevPeriodUp    : Bool   := FALSE
    prevPeriodDown  : Bool   := FALSE
    prevAmpUp       : Bool   := FALSE
    prevAmpDown     : Bool   := FALSE
    prevOffsetUp    : Bool   := FALSE
    prevOffsetDown  : Bool   := FALSE
```

> **Important TIA Portal setting:** In the DB properties, set **Optimized block access** to **OFF** if you want to see absolute addresses in the Watch Table. For this lab either setting works, but non-optimized access makes debugging more transparent.

---

## Complete PLC Tag Table

| Name | Data type | Address | Comment |
|------|-----------|---------|---------|
| `BtnShapeBit0` | Bool | I0.0 | Waveform shape selector — low bit |
| `BtnShapeBit1` | Bool | I0.1 | Waveform shape selector — high bit |
| `BtnPeriodUp` | Bool | I0.2 | Increase period (+0.1 s per press) |
| `BtnPeriodDown` | Bool | I0.3 | Decrease period (−0.1 s per press) |
| `BtnAmpUp` | Bool | I0.4 | Increase amplitude (+1.0 V per press) |
| `BtnAmpDown` | Bool | I0.5 | Decrease amplitude (−1.0 V per press) |
| `BtnOffsetUp` | Bool | I0.6 | Increase DC offset (+1.0 V per press) |
| `BtnOffsetDown` | Bool | I0.7 | Decrease DC offset (−1.0 V per press) |
| `AnalogOutput` | Int | QW80 | Analog output — SB 1232 AQ channel 0 |

---

## Final Program Block Summary

| Block | Type | Cycle | Language | Purpose |
|-------|------|-------|----------|---------|
| OB1 (Main) | Program cycle | Default (~10–150 ms) | SCL | Empty or diagnostics only |
| `OB_Generator` | Cyclic Interrupt | **20 ms** | SCL | Phase accumulation, waveform math, DAC output |
| `OB_InputHandler` | Cyclic Interrupt | **250 ms** | SCL | Digital input reading, parameter adjustment |
| `DB_GenParams` | Global Data Block | — | — | All parameters, state, and edge-detection memory |

---

## Testing Checklist

### Sawtooth
- [ ] Clean linear ramp visible on oscilloscope
- [ ] Period matches the `Period` setting (measure with cursors)
- [ ] Amplitude = 100 produces ±10 V swing
- [ ] Amplitude = 50 produces ±5 V swing
- [ ] Period of 0.15 s (non-multiple of 20 ms) still has correct average period

### Triangle
- [ ] Symmetric up-down ramp, no flat spots
- [ ] Peak-to-peak matches 2 × Amplitude in volts

### Sine
- [ ] Smooth sinusoidal shape at longer periods (e.g., 1 s = 50 samples/cycle)
- [ ] Visibly stepped at short periods (e.g., 0.1 s = 5 samples/cycle) — this is expected

### Square
- [ ] Sharp transitions between +Amplitude and −Amplitude
- [ ] 50% duty cycle (equal high and low durations)

### Parameter Controls
- [ ] Shape switches instantly when toggling I0.0 / I0.1
- [ ] Period increases/decreases by 0.1 s per press
- [ ] Amplitude increases/decreases by 1.0 V per press
- [ ] Offset shifts the entire waveform up or down
- [ ] Signal is clamped when Amplitude + |Offset| would exceed ±10 V

---

## Known Limitations and Design Notes

**Sampling rate vs. signal quality:** With a 20 ms cycle, you get `Period / 0.02` samples per waveform cycle. At the minimum period of 0.1 s, that is only 5 samples. A sine wave at 0.1 s period will appear as a coarse 5-point stepped approximation — this is a fundamental consequence of the Nyquist theorem applied to the 50 Hz update rate, and is expected behavior.

**Floating-point drift:** The repeated `Phase := Phase - 1.0` operation over millions of cycles could theoretically accumulate floating-point error. In practice, with 32-bit REAL and 12-bit DAC resolution, this would take astronomical run times to become visible. For a more robust implementation in production, one could use an integer cycle counter and derive the phase from it, but this is unnecessary for a lab exercise.

**Smooth parameter changes:** Because the phase accumulator does not depend on absolute time — only on the ratio `CycleTime / Period` — changing the period mid-cycle does not cause glitches. The waveform simply accelerates or decelerates from its current position. Similarly, changing amplitude or offset takes effect on the very next 20 ms computation cycle, providing instant response.

**Offset + amplitude exceeding range:** If Amplitude = 80 and Offset = 50, the raw signal would range from −80+50 = −30 to +80+50 = 130. The clamping at ±100 (±10 V) clips the positive peaks. This is intentional — the lab specifies that internal signals must be limited to the <−100.0, 100.0> range. The user should be aware that extreme offset values will cause clipping.
