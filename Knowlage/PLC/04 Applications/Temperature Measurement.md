---
title: Temperature Measurement
tags:
  - #application
  - #pid
  - #analog
---

# Temperature Measurement

> [!info] Source spine
- [[Presentations/06_PLC_lecture_2025_PID_1_6pp.pdf|PID 1 - Introduction]]
- [[Presentations/10_PLC_lecture_2025_PID_2.pdf|PID 2 - Tuning and response]]
- [[Presentations/11_PLC_lecture_2025_PID_3.pdf|PID 3 - Saturation and windup]]
- [[Presentations/12_PLC_lecture_2025_PID_in_PLC.pdf|PID in PLC]]
- [[Presentations/Brock_PID_control_4pp.pdf|PID control reference slides]]

## Problem Pattern
Measure temperature and optionally regulate it with PID.

## Solution Strategy
- Know sensor type: RTD, thermocouple, thermistor, or digital sensor.
- Use suitable module and cold-junction/linearization where required.
- Scale to degrees before comparison or PID.
- Filter noisy signals carefully.

## Required PLC Instructions
- [[SCALE_X]]
- [[COMPARE]]
- [[PID_Compact]]

## Related Theory
- [[Analog Scaling]]
- [[PID Control]]

## Solved Examples
- [[Example - Temperature Alarm Threshold]]

## Exam Tasks
- [[Task 10 - PI Controller With Weighting]]
