# AC Induction Motor — Study Guide

A compact but thorough guide based on the whiteboard example. The lesson you photographed is about a **3-phase induction (asynchronous) motor**, which is the workhorse of industrial AC drives and almost certainly what your test covers.

---

## 1. The Motor on the Board

The nameplate data for the example motor:

| Symbol | Value             | Meaning                           |
| ------ | ----------------- | --------------------------------- |
| n_N    | 1390 rpm          | Rated (nominal) shaft speed       |
| P      | 0.55 kW           | Rated mechanical **output** power |
| V      | 230 / 400 V, Δ/Y  | Rated line voltage — delta / star |
| I      | 2.65 / 1.5 A, Δ/Y | Rated line current — delta / star |
| cos φ  | 0.75              | Rated power factor                |
| f      | 50 Hz             | Supply frequency (European grid)  |

Sanity check: 400/230 ≈ 1.74 ≈ √3 and 2.65/1.5 ≈ 1.77 ≈ √3. That's the signature of a dual Δ/Y nameplate.

---

## 2. Synchronous Speed

The stator windings, fed with 3-phase currents, produce a rotating magnetic field that spins at the **synchronous speed**:

$$n_s = \frac{60 \cdot f}{p} \quad [\text{rpm}]$$

- **f** = supply frequency (Hz)
- **p** = number of **pole pairs** (not poles; poles = 2p)

At 50 Hz:

| p   | Poles | n_s (rpm) |
| --- | ----- | --------- |
| 1   | 2     | 3000      |
| 2   | 4     | 1500      |
| 3   | 6     | 1000      |
| 4   | 8     | 750       |

**How to find p from a nameplate:** the rated speed must be just below some n_s in the table. Rated speed 1390 rpm sits just below 1500 rpm, so **p = 2** (4-pole motor).

In rad/s: $\omega_s = 2\pi f / p$

---

## 3. Slip

The rotor cannot spin at exactly n_s — if it did, there'd be no relative motion between the stator field and rotor bars, no induced EMF, no rotor current, no torque. So the rotor always lags, and this lag is the **slip**:

$$s = \frac{n_s - n}{n_s} $$

For the example motor:

$$s_N = \frac{1500 - 1390}{1500} = 0.0733 = \mathbf{7.33\%}$$

(Matches the board: s_N = 7.3%.)

### Operating regions (s ranges from −100% to 200% on the board)

| Slip range | n vs n_s | Mode |
|---|---|---|
| s < 0 | n > n_s | **Generator** (rotor driven above synchronous) |
| s = 0 | n = n_s | Ideal synchronous — no torque produced |
| 0 < s < 1 | 0 < n < n_s | **Motoring** (normal operation) |
| s = 1 | n = 0 | Standstill / starting condition |
| s > 1 | n < 0 | **Plugging** (rotor spun against the field — heavy braking) |

---

## 4. Star (Y) vs Delta (Δ) Connection

Each stator winding is internally designed for 230 V and 2.65 A. How you wire the three windings together determines what appears at the terminals:

**Delta (Δ):** windings form a closed triangle.
- U_line = U_phase = 230 V
- I_line = √3 · I_phase = √3 · 2.65 ≈ 2.65 × 1.732 — wait, here 2.65 A **is already the line current**; phase current is 2.65/√3 ≈ 1.53 A.
- Use Δ on a **230 V** grid.

**Star / Wye (Y):** windings share a common neutral point.
- U_line = √3 · U_phase = √3 · 230 = 400 V
- I_line = I_phase = 1.5 A
- Use Y on a **400 V** grid.

**Same motor, same power either way** — the connection just matches the winding to the available grid voltage.

### Star-delta starting (worth knowing)
A classic trick: start the motor in Y (each winding sees only 230 V instead of 400 V), then switch to Δ after it's spinning. Starting current is reduced by a factor of 3, at the cost of reduced starting torque.

---

## 5. Three-Phase Power — The Power Triangle

Using **line** voltage and current:

$$\boxed{S = \sqrt{3} \cdot U \cdot I} \quad \text{[VA, apparent power]}$$
$$\boxed{P = \sqrt{3} \cdot U \cdot I \cdot \cos\varphi = S\cos\varphi} \quad \text{[W, real power]}$$
$$\boxed{Q = \sqrt{3} \cdot U \cdot I \cdot \sin\varphi = S\sin\varphi} \quad \text{[VAR, reactive power]}$$

These form a right triangle (shown in image 7/8):

```
        S (apparent)
        /|
       / | Q (reactive)
      /  |
     /φ  |
    /____|
     P (real)
```

Key relations:
- **S² = P² + Q²**
- **cos φ = P / S** (the power factor)
- **sin φ = Q / S**

### Applied to the example (Y connection — the board uses Y)

$$S = \sqrt{3} \cdot 400 \cdot 1.5 = 1039.2 \approx \mathbf{1040~VA}$$
$$P_{el} = S \cdot \cos\varphi = 1040 \cdot 0.75 = \mathbf{780~W}$$
$$Q = S \cdot \sin\varphi = 1040 \cdot \sqrt{1-0.75^2} = 1040 \cdot 0.661 \approx 688~\text{VAR}$$

**P_el is the total electrical power the motor draws from the grid.** Not all of it comes out the shaft — the rest becomes heat.

---

## 6. Mechanical Side: Angular Speed and Torque

Convert rpm to rad/s with:

$$\omega = \frac{2\pi \cdot n}{60} = \frac{\pi n}{30}$$

For the example at rated speed:
$$\omega_N = \frac{2\pi \cdot 1390}{60} = 145.6 \text{ rad/s}$$

**Torque** links mechanical power and angular speed:

$$\boxed{T = \frac{P_{mech}}{\omega}}$$

Rated shaft torque for the example:
$$T_N = \frac{P_{mech}}{\omega_N} = \frac{550}{145.6} = \mathbf{3.78~Nm}$$

(Board writes this as T_el = 3.78 Nm.)

---

## 7. Efficiency

$$\boxed{\eta = \frac{P_{mech}}{P_{el}} = \frac{\text{output}}{\text{input}}}$$

For the example:
$$\eta = \frac{550}{780} = 0.705 = \mathbf{70.5\%}$$

The missing 230 W shows up as:
- **Copper losses** — I²R heating in stator and rotor windings
- **Iron losses** — eddy currents and hysteresis in the core
- **Mechanical losses** — friction in bearings, windage
- **Stray losses** — miscellaneous

---

## 8. Torque–Slip Characteristic: Kloss Equation

The torque an induction motor produces depends on slip. The curve has a characteristic shape with a single maximum called the **pull-out** or **breakdown torque** T_max, occurring at the **critical slip** s_max.

**Kloss's equation** (simplified form, stator resistance neglected):

$$\boxed{\frac{T}{T_{max}} = \frac{2}{\dfrac{s}{s_{max}} + \dfrac{s_{max}}{s}}}$$

Board values: s_max = 20%, T_max = 10 Nm.

### Quick sanity checks
- At **s = s_max**: T/T_max = 2 / (1 + 1) = 1 ✓
- For **small s** (s ≪ s_max): s_max/s dominates, so T/T_max ≈ 2s/s_max. Torque is roughly **linear in s** — this is the **stable operating region**.
- For **large s** (s ≫ s_max): s/s_max dominates, so T/T_max ≈ 2s_max/s. Torque **falls** as slip grows — **unstable** region.

### Curve shape

```
   T
 T_max|      .──.
      |    ./    \.
      |   /        \.
      |  /           \.__
      | /               ─────
      |/_________________________
      0   s_max           1       s
       stable | unstable | starting
```

### Example: torque at a given slip
Using s_max = 20%, T_max = 10 Nm, at s = 10%:

$$\frac{T}{T_{max}} = \frac{2}{\frac{10}{20} + \frac{20}{10}} = \frac{2}{0.5 + 2} = \frac{2}{2.5} = 0.8$$

So T = 8 Nm.

At starting (s = 1):
$$\frac{T}{T_{max}} = \frac{2}{\frac{1}{0.2} + \frac{0.2}{1}} = \frac{2}{5 + 0.2} = \frac{2}{5.2} \approx 0.385$$

So T_start ≈ 3.85 Nm — significantly less than T_max. This is why induction motors can struggle to start under heavy loads.

---

## 9. Master Formula Sheet (memorize cold)

| Quantity | Formula |
|---|---|
| Synchronous speed | n_s = 60·f / p |
| Slip | s = (n_s − n) / n_s |
| Angular speed | ω = 2π·n / 60 |
| Apparent power (3-phase) | S = √3·U·I |
| Real power | P = √3·U·I·cos φ = S·cos φ |
| Reactive power | Q = √3·U·I·sin φ = S·sin φ |
| Power factor | cos φ = P / S |
| Power triangle | S² = P² + Q² |
| Torque | T = P_mech / ω |
| Efficiency | η = P_mech / P_el |
| Star: line vs phase | U_line = √3·U_ph,  I_line = I_ph |
| Delta: line vs phase | U_line = U_ph,  I_line = √3·I_ph |
| Kloss's equation | T/T_max = 2 / (s/s_max + s_max/s) |

---

## 10. Complete Worked Example (what the whiteboard walks through)

**Given:** n_N = 1390 rpm, P = 0.55 kW, 230/400 V Δ/Y, 2.65/1.5 A Δ/Y, cos φ = 0.75, f = 50 Hz.  
**Assume:** motor in Y connection on a 400 V grid, so use U = 400 V and I = 1.5 A.

**Step 1 — Synchronous speed / pole pairs.**  
Rated speed 1390 rpm is just below 1500 rpm, so n_s = 1500 rpm and **p = 2** (4 poles).

**Step 2 — Slip.**  
s_N = (1500 − 1390) / 1500 = **7.33 %**

**Step 3 — Apparent power.**  
S = √3 · 400 · 1.5 = **1040 VA**

**Step 4 — Real electrical input.**  
P_el = S · cos φ = 1040 · 0.75 = **780 W**

**Step 5 — Rated angular speed.**  
ω_N = 2π · 1390 / 60 = **145.6 rad/s**

**Step 6 — Rated shaft torque.**  
T_N = P_mech / ω_N = 550 / 145.6 = **3.78 Nm**

**Step 7 — Efficiency.**  
η = P_mech / P_el = 550 / 780 = **70.5 %**

That's the whole exercise. The test will almost certainly give you a similar nameplate and ask for some subset of these seven quantities — the method is always this sequence.

---

## 11. Test-Day Tips

1. **First thing: identify pole pairs.** From rated rpm, round up to the nearest 3000/1500/1000/750 to get n_s, then p = 60f/n_s.
2. **Watch Δ vs Y.** The numbers that go into S = √3·U·I are always **line** values — pick the U/I pair matching the actual connection.
3. **The √3 appears twice and that's it** — once in 3-phase power (S = √3·U·I) and once in the relation between line and phase quantities. Don't sprinkle it elsewhere.
4. **Units check:** ω in rad/s (not rpm!) when computing torque. Miss this and your torque is off by a factor of ~9.55.
5. **Efficiency is always output/input, always < 1.** If you get 140%, you mixed them up.
6. **For Kloss**: if asked for T at some s, just plug in. Don't try to derive it — the equation is all you need.
7. **Slip is dimensionless.** You can plug it in as a decimal (0.073) or percentage (7.3%) into Kloss — just be consistent on both sides of the fraction.
