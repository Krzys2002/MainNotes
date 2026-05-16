Autor: Krzysztof Sawicki and Michał Szerechowicz
## 1. Objective

The aim of this laboratory was to compare three control system implementations of an electric drive:

1. Direct control using torque–speed function  
2. Cascade control (PI speed + PI current) – analytical tuning  
3. Cascade control (PI speed + PI current) – manual tuning  

The comparison is based on torque response and current behavior under different load conditions.

---

## 2. Simulink Models

### 2.1 Model 1 – Torque Function Control

![[Set1Sim 1.png]]
Description:
- Control based on static relationship between speed and torque
- No feedback loop dynamics

---

### 2.2 Model 2 – Cascade Control (Analytical Tuning)

![[Set2Sim.png]]
Description:
- Two PI controllers:
  - Inner loop: current
  - Outer loop: speed
- Parameters calculated using given formulas

---

### 2.3 Model 3 – Cascade Control (Manual Tuning)

![[Set3Sim.png]]
Description:
- Same structure as Model 2
- Parameters tuned experimentally

---

## 3. Torque Equation

The control signal for Model 1 is defined as:

$$
y_1 = k_{\phi} \cdot W_{ref} + \frac{R \cdot T_L}{k_{\phi}}
$$

Where:
- \( $k_{\phi} = 1.5$ \)
- \( $R = 3$ \)

---

## 4. Torque Test Signals

The system was tested with three torque profiles:

$$
T_1 = \text{step}
$$

$$
T_2 = T_1 + \omega \cdot gain
$$

$$
T_3 = T_2 + (\omega \cdot gain)^2
$$

---

## 5. Torque Responses

### 5.1 Model 1 – Torque Function

![[Set1All.png]]

Observations:
- With ideal parameters have the best performance

---

### 5.2 Model 2 – Cascade (Manual)

![[Set2Step.png]]
![[Set2Prop.png]]
![[Set2Sqer.png]]

Observations:
- minimal over and under shoots

---

### 5.3 Model 3 – Cascade (Analytical)

![[Set3Step 1.png]]
![[Set3Prop 1.png]]
![[Set3Sqer.png]]

Observations:
- much larger over and under shoots then previous model 

---

## 6. Current Analysis

### 6.1 Model 1 – Torque Function

![[Set1Cur.png]]

Observations:
- current spike to near 40 A 

---

### 6.2 Model 2 – Cascade (Analytical)

![[Set2Cur.png]]

Observations:
- current is saturated at 10 A

---

### 6.3 Model 3 – Cascade (Manual)

![[Set3Cur.png]]

Observations:
- current is saturated at 10 A

---

## 7. Comparison

| Feature               | Model 1 (Torque) | Model 2 (Analytical) | Model 3 (Manual) |
| --------------------- | ---------------- | -------------------- | ---------------- |
| Stability             | Stable           | Stable               | Stable           |
| Torque tracking       | Best             | Very Good            | Good             |
| Current peaks         | >40A             | <10A                 | <10A             |
| Disturbance rejection | poor             | good                 | good             |
| Complexity            | complex          | simple               | simple           |

---

## 8. Conclusions

- The **cascade control (analytical tuning)** provides stable and predictable performance with good theoretical foundation.
- The **manual tuning approach** allows further optimization, often reducing overshoot and improving response time.
- Cascade structures significantly improve current control and protect against excessive torque.
- Proper tuning is essential for balancing speed of response and system stability.

---

## 9. Notes

- Sampling time: `dt = 0.00001`
- \( $T_p = 0.01$ \)

---