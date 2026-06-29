---
title: PID Control
tags:
  - #theory
  - #pid
  - #application
---

# PID Control

> [!info] Source spine
- [[Presentations/06_PLC_lecture_2025_PID_1_6pp.pdf|PID 1 - Introduction]]
- [[Presentations/10_PLC_lecture_2025_PID_2.pdf|PID 2 - Tuning and response]]
- [[Presentations/11_PLC_lecture_2025_PID_3.pdf|PID 3 - Saturation and windup]]
- [[Presentations/12_PLC_lecture_2025_PID_in_PLC.pdf|PID in PLC]]
- [[Presentations/Brock_PID_control_4pp.pdf|PID control reference slides]]

## Definition
Regulate a process variable toward a setpoint by proportional, integral, and derivative action.

## Purpose
- Regulate a process variable toward a setpoint by proportional, integral, and derivative action.

## When To Use
Use for temperature, level, flow, pressure, speed, and many continuous industrial variables.

## Important Properties
- P responds to present error, I removes steady-state error, D adds damping/prediction.
- A digital PID needs a fixed sample time.
- Output saturation can create integrator windup.
- Industrial PID blocks include manual/automatic mode, limits, alarms, and tuning support.

## Limitations
- Poor for processes with large dead time unless tuned conservatively.
- Noise makes derivative action risky.

## Common Mistakes
- No anti-windup when the actuator saturates.
- Using scan time instead of a fixed control period.
- Changing manual/auto mode without bumpless transfer.

## Related Concepts
- [[PID_Compact]]
- [[Discrete Approximation]]
- [[Analog Scaling]]
- [[LIMIT]]

## Practical Applications
- [[PID Control in PLC]]
- [[Temperature Measurement]]
- [[Digital PI Controller]]
