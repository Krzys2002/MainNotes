---
title: PID Control in PLC
tags:
  - #application
  - #pid
---

# PID Control in PLC

> [!info] Source spine
- [[Presentations/06_PLC_lecture_2025_PID_1_6pp.pdf|PID 1 - Introduction]]
- [[Presentations/10_PLC_lecture_2025_PID_2.pdf|PID 2 - Tuning and response]]
- [[Presentations/11_PLC_lecture_2025_PID_3.pdf|PID 3 - Saturation and windup]]
- [[Presentations/12_PLC_lecture_2025_PID_in_PLC.pdf|PID in PLC]]
- [[Presentations/Brock_PID_control_4pp.pdf|PID control reference slides]]

## Problem Pattern
Regulate a process using a PLC PID block or custom PI/PID algorithm.

## Solution Strategy
- Scale setpoint and process value into engineering units.
- Call the controller at a stable sample time.
- Set output limits and anti-windup behavior.
- Provide manual mode and status bits for HMI.

## Required PLC Instructions
- [[PID_Compact]]
- [[LIMIT]]
- [[SCALE_X]]

## Related Theory
- [[PID Control]]
- [[Discrete Approximation]]
- [[Analog Scaling]]

## Solved Examples
- [[Example - Digital PI Controller]]

## Exam Tasks
- [[Task 10 - PI Controller With Weighting]]
- [[Task 15 - HMI Drive Control]]
