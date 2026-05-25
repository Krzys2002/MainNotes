## 1. Idea of BLDC Motor Operation

A **Brushless DC Motor (BLDC)** is a synchronous electric motor powered from a DC source through an electronic inverter. Unlike a classical DC motor, the BLDC motor does not use brushes and a mechanical commutator. Instead, electronic switching performs commutation.

### Main Components
- **Stator**
  - Three-phase windings
  - Creates rotating magnetic field
- **Rotor**
  - Permanent magnets
- **Inverter**
  - Electronic commutator using MOSFETs/IGBTs
- **Position Detection**
  - Hall sensors or sensorless estimation

### Operating Principle
1. DC voltage is converted into 3-phase AC-like waveforms.
2. The inverter energizes stator phases in sequence.
3. The stator magnetic field rotates.
4. Rotor permanent magnets follow the rotating field.
5. Torque is produced due to interaction between:
   - stator magnetic field,
   - rotor magnetic field.

BLDC motors usually use:
- **Trapezoidal back-EMF**
- **120° conduction**
- Six-step commutation

### Advantages
- High efficiency
- High torque density
- Low maintenance
- No brush wear
- High speed capability
- Quiet operation

### Typical Applications
- Electric vehicles
- Drones
- Robotics
- Fans and pumps
- CNC machines

---

# 2. Electric Schematic of BLDC Motor and 3-Phase Inverter

## Basic Structure

```text
      DC Supply
         |
      +--+--+
      |     |
   3-Phase Inverter
 (6 MOSFET Bridge)
      |  |  |
      A  B  C
       \ | /
      BLDC Motor
```

## Three-Phase Inverter

The inverter contains:
- 3 half-bridges,
- 6 MOSFETs,
- gate drivers.

Each phase:
- upper transistor → high-side switch,
- lower transistor → low-side switch.

### Typical Switching Sequence

| Step | High Side | Low Side |
|---|---|---|
| 1 | A+ | B− |
| 2 | A+ | C− |
| 3 | B+ | C− |
| 4 | B+ | A− |
| 5 | C+ | A− |
| 6 | C+ | B− |

This sequence repeats every electrical revolution.

---

# 3. Equations of Electrical and Mechanical Part of BLDC Model

## Electrical Equation

$$
v_k(t)=Ri_k(t)+L\frac{di_k(t)}{dt}+e_k(t)
$$

Where:
- $v_k$— phase voltage,
- $i_k$ — phase current,
- $R$ — phase resistance,
- $L$ — phase inductance,
- $e_k$ — back EMF.

---

## Mechanical Equation

$$
T_{em}(t)=J\frac{d\omega_m(t)}{dt}+B\omega_m(t)+T_L(t)
$$

Where:
- $T_{em}$ — electromagnetic torque,
- $J$ — moment of inertia,
- $B$ — viscous friction coefficient,
- $\omega_m$ — rotor speed,
- $T_L$ — load torque.

---

## Electromagnetic Torque
$$
T_{em}=\sum_{k=a,b,c} T_{em,k}
$$

Single phase torque:

$$
T_{em,k}=i_k(t)k_T(\theta_e)
$$

Back EMF:

$$
e_k(t)=k_e(\theta_e)\omega_m(t)
$$

---

## Electrical Angle

$$
\omega_e(t)=\frac{p}{2}\omega_m(t)
$$

Where:
- $p$ — number of poles.

---

# 4. Basic Commutation Method for BLDC (Hall Sensors)

## Hall Sensor Commutation

Three Hall sensors detect rotor position every 60 electrical degrees.

### Hall Sensor Outputs

| Hall State | Active Phases |
|---|---|
| 001 | A+ B− |
| 101 | A+ C− |
| 100 | B+ C− |
| 110 | B+ A− |
| 010 | C+ A− |
| 011 | C+ B− |

### Features
- Simple implementation
- Reliable startup
- Good low-speed performance
- Widely used in industry

### Disadvantages
- Torque ripple
- Acoustic noise
- Lower efficiency compared to sinusoidal control

---

# 5. Advanced Methods of BLDC Control

## 5.1 Extended Angle Method

### Idea
Instead of strict 120° commutation, conduction angle is extended:
- 150°
- 180°

### Advantages
- Reduced torque ripple
- Better efficiency
- Smoother current

### Disadvantages
- More complex timing
- Increased switching overlap

---

## 5.2 Sensorless Control

### Principle
Rotor position estimated from:
- Back-EMF
- Flux observer
- Sliding mode observer
- PLL estimator

### Benefits
- No Hall sensors
- Lower cost
- Higher reliability

### Problems
- Difficult startup
- Weak low-speed estimation

---

## 5.3 Sinusoidal Control

### Principle
Instead of trapezoidal commutation:
- sinusoidal currents are generated,
- often using PWM and FOC.

### Advantages
- Very smooth torque
- Low acoustic noise
- High efficiency

### Disadvantages
- Requires precise rotor position
- Higher computational complexity

### Usually Implemented With
- PMSM motors
- FOC (Field Oriented Control)

---

# 6. Scalar Control of BLDC/PMSM Machine with V/f Characteristics

## Idea of V/f Control

$$
\frac{V}{f}=const
$$

Magnetic flux:

$$
\phi \propto \frac{V}{f}
$$

If frequency increases:
- voltage must also increase.

---

## Regions of Operation

### 1. Low Frequency Region
- Additional voltage boost needed
- Compensates stator resistance drop

### 2. Constant Flux Region
- Constant V/f ratio
- Rated torque available

### 3. Field Weakening Region
- Voltage saturated
- Flux decreases
- Torque decreases

---

## Angle Generator

In scalar control, rotor electrical angle is generated from frequency.

$$
Angle_{pu}=Angle_{pu}+StepAngleMax\cdot Freq
$$

---

# 7. Texas Instruments Experiment Book – Laboratory 1B

## Purpose of Lab 1B

Lab 1B:
- verifies hardware integrity,
- tests PWM and ADC operation,
- implements open-loop scalar V/f control.

---

## Main Features
- Open-loop control
- No FAST estimator
- Angle generator used
- V/f profile generation
- PWM testing
- ADC testing

### Modules Used
- PWM
- ADC
- Clarke transform
- Park transform
- SVGEN

---

## Important Files

| File | Purpose |
|---|---|
| angle_gen.c | Angle generator |
| vs_freq.c | V/f profile |
| hal.h | Hardware abstraction |
| user.h | Motor parameters |

---

## PWMDAC Monitoring

The lab allows visualization of:
- PWM waveforms,
- phase currents,
- voltages,
- generated angle.

Example monitored signals:
- SVGEN output,
- phase current,
- phase voltage,
- angle generator output.

---

# 8. Comparison of BLDC Control Methods

| Method | Sensors | Complexity | Torque Ripple | Efficiency |
|---|---|---|---|---|
| Six-step Hall | Hall sensors | Low | High | Medium |
| Extended angle | Hall/sensorless | Medium | Medium | Better |
| Sensorless | No | Medium/High | Medium | High |
| Sinusoidal | Encoder/observer | High | Very low | Very high |
| FOC | Encoder/sensorless | Very high | Minimal | Excellent |

---

# 9. Key Takeaways

- BLDC motors use electronic commutation instead of brushes.
- Three-phase inverter controls motor phases.
- Hall sensors provide simple commutation.
- Sensorless and sinusoidal methods improve efficiency and smoothness.
- V/f scalar control is simple and useful for testing and low-cost systems.
- TI InstaSPIN provides advanced BLDC/PMSM control solutions and laboratory exercises for implementation.
