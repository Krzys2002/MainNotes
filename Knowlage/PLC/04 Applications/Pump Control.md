---
title: Pump Control
tags:
  - #application
---

# Pump Control

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Problem Pattern
Start and stop a pump from level/pressure demand while protecting the equipment.

## Solution Strategy
- Use start/stop thresholds with hysteresis.
- Add minimum run/off timers.
- Interlock with overload, dry-run, and manual mode.
- Expose state and alarms to HMI.

## Required PLC Instructions
- [[TON]]
- [[TOF]]
- [[SET]]
- [[RESET]]
- [[COMPARE]]

## Related Theory
- [[Analog Scaling]]
- [[Timers]]
- [[HMI and Manual Control]]

## Solved Examples
- [[Example - Pump With Hysteresis]]

## Exam Tasks
- No direct task yet.
