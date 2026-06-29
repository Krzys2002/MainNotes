---
title: Discrete Approximation
tags:
  - #theory
  - #pid
  - #exam
---

# Discrete Approximation

> [!info] Source spine
- [[Presentations/06_PLC_lecture_2025_PID_1_6pp.pdf|PID 1 - Introduction]]
- [[Presentations/10_PLC_lecture_2025_PID_2.pdf|PID 2 - Tuning and response]]
- [[Presentations/11_PLC_lecture_2025_PID_3.pdf|PID 3 - Saturation and windup]]
- [[Presentations/12_PLC_lecture_2025_PID_in_PLC.pdf|PID in PLC]]
- [[Presentations/Brock_PID_control_4pp.pdf|PID control reference slides]]

## Definition
Convert a continuous transfer function or differential equation into cyclic PLC calculations.

## Purpose
- Convert a continuous transfer function or differential equation into cyclic PLC calculations.

## When To Use
Use for digital filters, PI/PID algorithms, integrators, and plant approximations.

## Important Properties
- Choose a sample time Ts first.
- Forward Euler approximates derivatives/integrals using the current or previous sample.
- Backward Euler is often more stable for simple PLC implementations.
- Difference equations must store previous inputs and outputs.

## Limitations
- Large Ts can destabilize or distort the model.
- Continuous tuning values may not behave the same after discretization.

## Common Mistakes
- Forgetting initial conditions.
- Using seconds in formulas while Ts is configured in milliseconds.
- Updating history variables before calculating the new output.

## Related Concepts
- [[Cyclic Interrupt]]
- [[PID Control]]
- [[Digital PI Controller]]

## Practical Applications
- [[Digital Approximation in PLC]]
- [[Digital PI Controller]]
