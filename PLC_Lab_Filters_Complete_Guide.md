# Complete Step-by-Step Guide: Implementation of Simple Digital Filters
## PLC Lab — Station 5 (Siemens S7-1200, TIA Portal)

---

## PHASE 0 — Prerequisites and Preparation

Before arriving at the lab, make sure you are familiar with the following from prior sessions:

- Creating and configuring a TIA Portal project for an S7-1200 controller (CPU 1214C DC/DC/DC, order no. 6ES7 214-1AG31-0XB0).
- Programming in Structured Text (SCL / ST).
- The difference between Functions (FC) — stateless — and Function Blocks (FB) — with instance data blocks that preserve state across calls.
- How ADC and DAC channels work on the S7-1200 (address mapping, value ranges).
- Creating and using Cyclic Interrupt Organization Blocks (OB30+).

---

## PHASE 1 — Hardware Configuration and Wiring

### Step 1.1 — Create a TIA Portal Project

1. Open TIA Portal. Create a new project.
2. Add the device: **CPU 1214C DC/DC/DC** (6ES7 214-1AG31-0XB0).
3. In **Device Configuration**, add the expansion module **Signal Board SB 1232 AQ 1×12 bit** (6ES7 232-4HA30-0XB0). This board provides one analog output channel (AQ0) at address **QW80**.

### Step 1.2 — Enable Clock Memory Bits

1. In **Device Configuration → CPU → Properties → System and clock memory**, check **Enable the use of clock memory byte** and note the assigned memory byte (typically MB0 or another byte you choose, e.g., MB100).
2. Clock memory bits provide toggling signals at various frequencies (10 Hz, 5 Hz, 2.5 Hz, 2 Hz, 1.25 Hz, 1 Hz, 0.625 Hz, 0.5 Hz), which are useful for generating the binary test signal in Task 1.

### Step 1.3 — Electrical Wiring

The S7-1200's built-in analog inputs:
- **IW64** → Analog Input AI0 (0–10 V, 10-bit, values 0–27648)
- **IW66** → Analog Input AI1 (0–10 V, 10-bit, values 0–27648)

The SB 1232 AQ analog output:
- **QW80** → Analog Output AQ0 (±10 V, 12-bit, values −27648 to +27648)

Wiring checklist:
1. **Connect all grounds together**: the analog input ground (2M), the analog output ground (0M on SB1232), and the digital output ground (3M) must all share a common reference with the controller's main ground.
2. **Build a voltage divider**: The digital output produces 24 V, but the analog input only tolerates up to 10 V. Use a potentiometric voltage divider (e.g., two resistors in series, such as 14 kΩ and 10 kΩ, or a potentiometer) between the digital output and the analog input to scale the 24 V signal down to below 10 V. **CRITICAL**: Never apply more than 10 V to the analog input — the absolute maximum is 35 VDC, but the usable measurement range ends at 10 V.
3. Connect the divided output to **AI0** (terminals for channel 0).
4. Connect an oscilloscope probe to the **AQ0** output and to the analog input to observe signal behavior during the lab.

### Step 1.4 — Download Hardware Configuration

1. Compile the hardware configuration (right-click the PLC → Compile → Hardware).
2. Download to the controller (right-click the PLC → Download to device → Hardware configuration).
3. Verify in the online view that the SB1232 AQ module is recognized and showing no errors.

---

## PHASE 2 — Define Global Tags

Create a PLC tag table (or use the default tag table) with meaningful symbolic names. Here is a recommended set:

| Tag Name         | Data Type | Address | Description                            |
| ---------------- | --------- | ------- | -------------------------------------- |
| `AI0_raw`        | Int       | IW64    | Raw analog input channel 0             |
| `AI1_raw`        | Int       | IW66    | Raw analog input channel 1             |
| `AQ0_out`        | Int       | QW80    | Analog output channel 0                |
| `DigOut_Signal`  | Bool      | Q0.0    | Digital output for binary signal gen   |
| `DigIn_Switch`   | Bool      | I0.0    | Digital input to select output channel |
| `ClockBit_1Hz`   | Bool      | M100.5  | 1 Hz clock memory bit (adjust address) |
| `ClockBit_0_5Hz` | Bool      | M100.7  | 0.5 Hz clock memory bit                |

The exact clock memory bit addresses depend on which byte you assigned in Step 1.2. Consult the TIA Portal help for the standard mapping of clock frequencies to bit positions within the clock memory byte.

---

## PHASE 3 — Task 1: Input Signal Generator

This task has two sub-parts. Both generate test signals that will later be fed into the digital filters.

### Task 1, Part 1 — Binary Signal from Digital Output through Voltage Divider

**Goal**: Generate a periodic binary (square wave) signal at 0.5–1 Hz on a digital output, pass it through the voltage divider to an analog input, read it, normalize it, and output it on the analog output.

#### Step 3.1 — Generate the Binary Signal

**Option A — Using Clock Memory Bits (simplest approach):**

In **OB1 (Main)** or in a Cyclic Interrupt OB, simply assign a clock memory bit to the digital output:

```
// In OB1 or a cyclic OB — SCL
"DigOut_Signal" := "ClockBit_1Hz";   // 1 Hz square wave → Q0.0
```

This produces a 0.5 Hz toggling signal (1 Hz clock bit means 1 full cycle per second, i.e., 0.5 s high, 0.5 s low). If you want 0.5 Hz, use the 0.5 Hz clock memory bit instead.

**Option B — Using a Cyclic Interrupt with a Toggle Variable:**

1. Add a new Organization Block: right-click **Program Blocks → Add new block → Organization Block → Cyclic Interrupt**. Set the cycle time to, for example, 500 ms (for a 1 Hz toggle, each call flips state, giving a period of 1 s). Name it `OB_SignalGen`.
2. Write in SCL:

```
// OB_SignalGen — Cyclic Interrupt, period = 500 ms
"DigOut_Signal" := NOT "DigOut_Signal";
```

This toggles the digital output every 500 ms, producing a 1 Hz square wave.

#### Step 3.2 — Read and Normalize the Analog Input

The signal travels: Digital Output (0/24 V) → voltage divider → Analog Input (0 to ~10 V). The ADC produces a value in the range 0–27648 for 0–10 V. However, the lab requires normalization to the full range **⟨−100.0, 100.0⟩** corresponding to **⟨−10 V, +10 V⟩**.

Since the analog input only reads 0–10 V (unipolar), the raw values 0–27648 correspond to 0–10 V. But the normalization formula maps the full ±10 V range (i.e., ±27648 on the output side) to ±100.0.

The general normalization formula:

```
normalized_value := (INT_TO_REAL(raw_value) / 27648.0) * 100.0;
```

For the input (which is 0–10 V only, so 0–27648):

```
// Read and normalize — in a Cyclic Interrupt OB (e.g., 40 ms period)
VAR_TEMP
    rawInput : Int;
    normalizedInput : Real;
    outputValue : Int;
END_VAR

rawInput := "AI0_raw";
normalizedInput := (INT_TO_REAL(rawInput) / 27648.0) * 100.0;
// normalizedInput is now in the range [0.0 .. 100.0] for unipolar input
```

#### Step 3.3 — Output to Analog Output

To write a normalized value (range −100.0 to 100.0) back to the analog output (range −27648 to 27648):

```
outputValue := REAL_TO_INT(normalizedInput * 27648.0 / 100.0);
"AQ0_out" := outputValue;
```

#### Step 3.4 — Verify on Oscilloscope

Connect the oscilloscope to AQ0. You should see a square wave whose amplitude corresponds to the voltage divider setting. Adjust the potentiometer so the signal is visible and within range.

---

### Task 1, Part 2 — Sinusoidal Signal with Stochastic Disturbance

**Goal**: In a 40 ms cyclic interrupt, generate a sine wave (amplitude 0–100, period 0.1–10 s) and superimpose pseudo-random noise on it.

#### Step 3.5 — Create the Cyclic Interrupt OB for Signal Generation

1. Add a new **Organization Block → Cyclic Interrupt**, name it `OB_CyclicGen`, and set the cycle time to **40 ms** (= 0.040 s). This means T_s = 0.04 s.
2. You will need global data (or a Data Block) to store persistent variables between calls. Create a **Global Data Block** (e.g., `DB_SignalGen`) with these variables:

| Variable Name    | Data Type | Initial Value | Purpose                                |
|------------------|-----------|---------------|----------------------------------------|
| `amplitude`      | Real      | 50.0          | Sine amplitude (0.0 to 100.0)          |
| `period`         | Real      | 2.0           | Sine period in seconds (0.1 to 10.0)   |
| `phase`          | Real      | 0.0           | Current phase angle (radians)          |
| `R_prev`         | DInt      | 0             | Previous pseudo-random number          |
| `noiseAmplitude` | Real      | 10.0          | Amplitude of noise component           |
| `signalOut`      | Real      | 0.0           | Combined output signal                 |

#### Step 3.6 — Generate the Sinusoidal Signal

In `OB_CyclicGen` (SCL):

```
VAR_TEMP
    Ts : Real := 0.04;          // 40 ms sampling period
    omega : Real;
    sineValue : Real;
    phaseIncrement : Real;
END_VAR

// Calculate angular frequency and phase increment per sample
omega := 2.0 * 3.14159265 / "DB_SignalGen".period;
phaseIncrement := omega * Ts;

// Update phase
"DB_SignalGen".phase := "DB_SignalGen".phase + phaseIncrement;

// Keep phase within [0, 2*pi) to prevent numerical overflow
IF "DB_SignalGen".phase >= (2.0 * 3.14159265) THEN
    "DB_SignalGen".phase := "DB_SignalGen".phase - (2.0 * 3.14159265);
END_IF;

// Generate sine value
sineValue := "DB_SignalGen".amplitude * SIN("DB_SignalGen".phase);
```

#### Step 3.7 — Implement the Pseudo-Random Number Generator (LCG)

The lab provides the Linear Congruential Generator formula:

**R(n) = (R(n−1) × a + c) mod m**

With suggested parameters: **a = 239, c = 241, m = 251, R(1) = 0**.

This produces values in the range 0 to 250. You need to scale and shift them to get bipolar noise (e.g., centered around zero).

```
VAR_TEMP
    R_new : DInt;
    noiseValue : Real;
END_VAR

// LCG pseudo-random number generation
R_new := ("DB_SignalGen".R_prev * 239 + 241) MOD 251;
"DB_SignalGen".R_prev := R_new;

// Scale to bipolar: map [0, 250] → [-1.0, +1.0]
noiseValue := (DINT_TO_REAL(R_new) / 125.0) - 1.0;

// Scale by desired noise amplitude
noiseValue := noiseValue * "DB_SignalGen".noiseAmplitude;
```

#### Step 3.8 — Combine Sine and Noise, Output to DAC

```
"DB_SignalGen".signalOut := sineValue + noiseValue;

// Clamp to [-100.0, 100.0]
IF "DB_SignalGen".signalOut > 100.0 THEN
    "DB_SignalGen".signalOut := 100.0;
ELSIF "DB_SignalGen".signalOut < -100.0 THEN
    "DB_SignalGen".signalOut := -100.0;
END_IF;

// Convert to DAC range: [-100.0, 100.0] → [-27648, 27648]
"AQ0_out" := REAL_TO_INT("DB_SignalGen".signalOut * 27648.0 / 100.0);
```

#### Step 3.9 — Verify on Oscilloscope

Observe the AQ0 output on the oscilloscope. You should see a sinusoidal waveform with visible high-frequency noise superimposed. Adjust `amplitude`, `period`, and `noiseAmplitude` in the data block (using the watch table or online monitoring) to verify behavior.

---

## PHASE 4 — Task 2: First-Order Low-Pass Filter (LPF1)

### Theory Recap

The continuous-time first-order LPF transfer function is:

**G_LPF1(s) = ω_g / (s + ω_g) = 1 / (1 + sT)**

where **ω_g = 2π·f_g** is the cutoff angular frequency and **T = 1/ω_g** is the time constant.

Using the **Euler (forward difference) discretization** s = (1/T_s)(1 − z⁻¹), the discrete transfer function becomes:

**H_LPF1(z) = b₀ / (z⁻¹ + a₀)**

Leading to the **difference equation**:

**y(n) = (1/a₀) · (−y(n−1) + b₀ · x(n))**

Where the coefficients are:

- **a₀ = −(T + T_s) / T**  (note: T = 1/ω_g)
- **b₀ = −T_s / T**

Let's rewrite these more explicitly. Given f_g (cutoff frequency) and T_s (sampling period):

- ω_g = 2π · f_g
- T = 1 / ω_g
- a₀ = −(T + T_s) / T = −1 − T_s/T = −1 − T_s · ω_g
- b₀ = −T_s / T = −T_s · ω_g

So the recurrence is:

**y(n) = (1/a₀) · (−y(n−1) + b₀ · x(n))**

Which simplifies to:

**y(n) = [y(n−1) + T_s·ω_g · x(n)] / (1 + T_s·ω_g)**

This is the classic exponential smoothing / first-order IIR filter.

### Step 4.1 — Create the Function Block FB_LPF1

1. Right-click **Program Blocks → Add new block → Function Block (FB)**, name it `FB_LPF1`, language **SCL**.
2. Define the interface:

**Input Parameters (VAR_INPUT):**

| Name   | Type | Description                    |
|--------|------|--------------------------------|
| `x`    | Real | Current input sample x(n)      |
| `fg`   | Real | Cutoff frequency in Hz         |
| `Ts`   | Real | Sampling period in seconds     |

**Output Parameters (VAR_OUTPUT):**

| Name   | Type | Description                    |
|--------|------|--------------------------------|
| `y`    | Real | Current output sample y(n)     |

**Static Variables (VAR — these persist between calls):**

| Name      | Type | Initial Value | Description                  |
|-----------|------|---------------|------------------------------|
| `y_prev`  | Real | 0.0           | Previous output y(n−1)       |

3. Write the FB code in SCL:

```
// FB_LPF1 — First-Order Low-Pass Filter
VAR_TEMP
    omega_g : Real;
    T_filter : Real;
    a0 : Real;
    b0 : Real;
END_VAR

// Calculate filter coefficients
omega_g := 2.0 * 3.14159265 * #fg;
T_filter := 1.0 / omega_g;            // Time constant of the analog filter

a0 := -(T_filter + #Ts) / T_filter;   // a0 = -(1 + Ts*omega_g)
b0 := -(#Ts) / T_filter;              // b0 = -(Ts*omega_g)

// Difference equation: y(n) = (1/a0) * (-y_prev + b0 * x)
#y := (1.0 / a0) * (-#y_prev + b0 * #x);

// Store current output for next call
#y_prev := #y;
```

**Important note on the `#` prefix**: In TIA Portal SCL, the `#` prefix is used to reference the block's own interface variables (inputs, outputs, statics). Local temp variables may or may not need it depending on TIA Portal version; typically they do.

### Step 4.2 — Call FB_LPF1 in the Cyclic Interrupt

1. You will call the FB inside the 40 ms cyclic interrupt OB (`OB_CyclicGen` or a separate one). When you drag the FB into the OB, TIA Portal will prompt you to create an **Instance Data Block** (e.g., `DB_LPF1_Instance`).

2. In the cyclic interrupt OB, add the call:

```
// Read and normalize analog input
VAR_TEMP
    rawInput : Int;
    normalizedInput : Real;
    filteredOutput : Real;
    outputValue : Int;
END_VAR

rawInput := "AI0_raw";
normalizedInput := (INT_TO_REAL(rawInput) / 27648.0) * 100.0;

// Call the first-order filter
"DB_LPF1_Instance"(
    x  := normalizedInput,
    fg := 2.0,           // Cutoff frequency — experiment with values
    Ts := 0.04,          // 40 ms sampling period
    y  => filteredOutput
);

// Output to DAC
outputValue := REAL_TO_INT(filteredOutput * 27648.0 / 100.0);
"AQ0_out" := outputValue;
```

### Step 4.3 — Test with the Binary (Step) Signal

1. First, use the binary signal from Task 1 Part 1 as the input. The voltage divider feeds the square wave to AI0.
2. Observe the output on the oscilloscope. You should see the step response of the first-order filter — an exponential rise and fall instead of sharp edges.
3. **Vary the cutoff frequency** `fg` and observe how it affects the step response:
   - Higher f_g → faster response, less smoothing
   - Lower f_g → slower response, more smoothing

### Step 4.4 — Test with the Sinusoidal Signal + Noise

1. Switch the input source to the internally generated sinusoidal signal with noise (from Task 1 Part 2). Instead of reading from AI0, pass `DB_SignalGen.signalOut` directly to the filter's `x` input.
2. Use the digital input switch (`I0.0`) to toggle between showing the filter input or the filter output on the analog output AQ0:

```
IF "DigIn_Switch" THEN
    // Show filtered output
    "AQ0_out" := REAL_TO_INT(filteredOutput * 27648.0 / 100.0);
ELSE
    // Show raw input (with noise)
    "AQ0_out" := REAL_TO_INT("DB_SignalGen".signalOut * 27648.0 / 100.0);
END_IF;
```

3. Compare both signals on the oscilloscope. The filter should attenuate the high-frequency noise while preserving the lower-frequency sinusoidal component. The effectiveness depends on the relationship between f_g, the sine frequency, and the noise bandwidth.

### Step 4.5 — (Optional) Cascaded First-Order Filters

To verify correct operation, cascade two instances of `FB_LPF1`:

1. Create a second instance data block (e.g., `DB_LPF1_Instance2`).
2. Feed the output of the first filter into the input of the second:

```
// First filter stage
"DB_LPF1_Instance"(
    x  := normalizedInput,
    fg := 2.0,
    Ts := 0.04,
    y  => intermediateOutput
);

// Second filter stage (cascaded)
"DB_LPF1_Instance2"(
    x  := intermediateOutput,
    fg := 2.0,
    Ts := 0.04,
    y  => filteredOutput
);
```

The cascaded result should show even more smoothing (steeper roll-off, equivalent to a second-order filter with −40 dB/decade at high frequencies, though with a different damping characteristic than a true second-order design).

---

## PHASE 5 — Task 3: Second-Order Low-Pass Filter (LPF2)

### Theory Recap

The continuous-time second-order LPF transfer function is:

**G_LPF2(s) = ω_g² / (s² + 2ξω_g·s + ω_g²)**

where ξ (xi) is the **damping factor** (ranging from 0 to 2).

After discretization using s = (1/T_s)(1 − z⁻¹), the discrete transfer function is:

**H_LPF2(z) = b₀ / (z⁻² + a₁·z⁻¹ + a₀)**

Leading to the **difference equation**:

**y(n) = (1/a₀) · (−y(n−2) − a₁·y(n−1) + b₀·x(n))**

Where the coefficients are:

- **a₁ = −2 − 2ξω_gT_s**
- **a₀ = 1 + 2ξω_gT_s + (ω_gT_s)²**
- **b₀ = (ω_gT_s)²**

### Step 5.1 — Create the Function Block FB_LPF2

1. Add a new **Function Block (FB)**, name it `FB_LPF2`, language **SCL**.
2. Define the interface:

**Input Parameters (VAR_INPUT):**

| Name   | Type | Description                        |
|--------|------|------------------------------------|
| `x`    | Real | Current input sample x(n)          |
| `fg`   | Real | Cutoff frequency in Hz             |
| `xi`   | Real | Damping factor (0.0 to 2.0)        |
| `Ts`   | Real | Sampling period in seconds         |

**Output Parameters (VAR_OUTPUT):**

| Name   | Type | Description                        |
|--------|------|------------------------------------|
| `y`    | Real | Current output sample y(n)         |

**Static Variables (VAR):**

| Name      | Type | Initial Value | Description                    |
|-----------|------|---------------|--------------------------------|
| `y_prev1` | Real | 0.0           | Previous output y(n−1)         |
| `y_prev2` | Real | 0.0           | Output two steps back y(n−2)   |

3. Write the FB code in SCL:

```
// FB_LPF2 — Second-Order Low-Pass Filter
VAR_TEMP
    omega_g : Real;
    wTs : Real;         // omega_g * Ts
    a0 : Real;
    a1 : Real;
    b0 : Real;
    y_new : Real;
END_VAR

// Calculate intermediate values
omega_g := 2.0 * 3.14159265 * #fg;
wTs := omega_g * #Ts;

// Calculate coefficients
a1 := -2.0 - 2.0 * #xi * wTs;
a0 := 1.0 + 2.0 * #xi * wTs + (wTs * wTs);
b0 := wTs * wTs;

// Difference equation: y(n) = (1/a0) * (-y(n-2) - a1*y(n-1) + b0*x(n))
y_new := (1.0 / a0) * (-#y_prev2 - a1 * #y_prev1 + b0 * #x);

// Shift the memory: y(n-2) ← y(n-1), y(n-1) ← y(n)
#y_prev2 := #y_prev1;
#y_prev1 := y_new;

// Output
#y := y_new;
```

### Step 5.2 — Call FB_LPF2 in the Cyclic Interrupt

Create an instance data block (e.g., `DB_LPF2_Instance`) and call it in the 40 ms cyclic interrupt:

```
"DB_LPF2_Instance"(
    x  := normalizedInput,     // or the generated sinusoidal signal
    fg := 2.0,                  // Cutoff frequency — experiment
    xi := 0.707,                // Damping factor — try different values
    Ts := 0.04,                 // 40 ms
    y  => filteredOutput
);
```

### Step 5.3 — Experiment with the Damping Factor ξ

The damping factor ξ dramatically affects the filter's behavior:

- **ξ = 0.0 (undamped)**: Oscillatory — the filter will ring indefinitely. In practice, avoid this as it can cause instability.
- **ξ = 0.1–0.3 (underdamped)**: Strong overshoot and ringing in the step response, sharp resonance peak near f_g in the frequency response.
- **ξ = 0.707 (≈ 1/√2, Butterworth)**: Maximally flat passband. This is the classic "optimal" damping for a second-order filter — no overshoot in the frequency response, mild overshoot in step response.
- **ξ = 1.0 (critically damped)**: No oscillation, fastest response without overshoot.
- **ξ = 1.5–2.0 (overdamped)**: Very sluggish response, effectively acts like a stronger low-pass.

Test with the step signal first to observe these characteristics, then with the noisy sinusoidal signal.

### Step 5.4 — Use the Channel Selection Switch

Just as in Task 2, use the digital input to toggle between filter input and filter output on the analog output:

```
IF "DigIn_Switch" THEN
    "AQ0_out" := REAL_TO_INT(filteredOutput * 27648.0 / 100.0);
ELSE
    "AQ0_out" := REAL_TO_INT(inputSignal * 27648.0 / 100.0);
END_IF;
```

Compare both traces on the oscilloscope.

---

## PHASE 6 — Complete Program Structure Summary

Here is the recommended block organization for the final project:

```
Program Blocks
├── Main [OB1]
│   └── (Optional: binary signal generator using clock memory bits)
│
├── OB_CyclicGen [OB30 — Cyclic Interrupt, 40 ms]
│   ├── Sinusoidal signal generation + LCG noise
│   ├── Analog input reading and normalization
│   ├── Call FB_LPF1 (via DB_LPF1_Instance)
│   ├── Call FB_LPF2 (via DB_LPF2_Instance)
│   ├── (Optional) Call second FB_LPF1 for cascade (via DB_LPF1_Instance2)
│   └── Channel selection and analog output writing
│
├── FB_LPF1 [Function Block]
│   └── First-order low-pass filter algorithm
│
├── FB_LPF2 [Function Block]
│   └── Second-order low-pass filter algorithm
│
├── DB_SignalGen [Global Data Block]
│   └── Stores amplitude, period, phase, R_prev, noiseAmplitude, signalOut
│
├── DB_LPF1_Instance [Instance DB for FB_LPF1]
├── DB_LPF1_Instance2 [Instance DB for cascaded FB_LPF1] (optional)
└── DB_LPF2_Instance [Instance DB for FB_LPF2]
```

---

## PHASE 7 — Testing and Evaluation Checklist

Use this checklist during the lab session to ensure everything works:

**Task 1 — Signal Generator:**
- [ ] Binary signal (0.5–1 Hz) appears on digital output Q0.0
- [ ] Voltage divider reduces 24 V to <10 V at AI0
- [ ] Normalized signal correctly maps to ⟨−100.0, 100.0⟩ range
- [ ] Analog output AQ0 reproduces the binary signal (observable on scope)
- [ ] Sinusoidal signal generates with correct amplitude and period
- [ ] LCG noise is visible superimposed on the sine wave
- [ ] Combined signal observable on oscilloscope via AQ0

**Task 2 — First-Order Filter:**
- [ ] FB_LPF1 is implemented as a Function Block with static memory
- [ ] Step response shows exponential behavior (no sharp edges)
- [ ] Changing f_g visibly alters the step response speed
- [ ] Noisy sine filtered — noise reduced, sine preserved
- [ ] Channel switch toggles between input/output on AQ0
- [ ] (Bonus) Cascaded two LPF1 sections work correctly

**Task 3 — Second-Order Filter:**
- [ ] FB_LPF2 is implemented as a Function Block with two static memory elements
- [ ] Step response shows characteristic second-order behavior
- [ ] Different ξ values produce visibly different responses (underdamped, critically damped, overdamped)
- [ ] Noisy sine filtered effectively
- [ ] All signals properly rescaled for the analog output

---

## Common Pitfalls and Troubleshooting

**"My analog output is always 0"** — Check that the SB1232 AQ module is configured in the device configuration and that the hardware configuration has been downloaded. Verify the output address is QW80. Also confirm the ground connection between AQ0M and the controller ground.

**"The filter output is unstable or blowing up"** — This typically happens when T_s is too large relative to the filter time constant (1/ω_g). Ensure that the cutoff frequency is not too high relative to the sampling rate. As a rule of thumb, f_g should be well below 1/(2·T_s) = 12.5 Hz for T_s = 40 ms. Also double-check the coefficient formulas — a sign error will cause instability.

**"The LCG generates the same sequence every time"** — That is expected behavior for a deterministic pseudo-random generator with a fixed seed. This is acceptable for the lab. If you want variation, change the initial seed R(1).

**"Type mismatch errors in SCL"** — The S7-1200 is strict about types. Use `INT_TO_REAL()`, `REAL_TO_INT()`, `DINT_TO_REAL()` etc. for all conversions. The analog I/O addresses (IW64, QW80) are of type `Int` (16-bit signed integer).

**"The second-order filter oscillates wildly with ξ = 0"** — This is mathematically correct: zero damping means pure oscillation at the natural frequency. Increase ξ to at least 0.1 for practical use.

**"The instance data block does not retain values"** — In TIA Portal, right-click the instance DB and ensure that **"Optimized block access"** is enabled (default in newer TIA Portal versions). Also make sure variables are in the **Static** section of the FB, not in Temp.
