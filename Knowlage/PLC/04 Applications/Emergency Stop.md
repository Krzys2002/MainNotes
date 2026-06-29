---
title: Emergency Stop
tags:
  - #application
  - #hardware
  - #exam
---

# Emergency Stop

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
Stop hazardous motion safely.

## Solution Strategy
- Use certified safety hardware for real emergency stop circuits.
- Use PLC logic only for indication, reset requests, and non-safety interlocks unless a safety PLC is used.
- Design stop-dominant software behavior.

## Required PLC Instructions
- [[RESET]]

## Related Theory
- [[Digital Inputs and Outputs]]
- [[PLC Wiring]]
- [[HMI and Manual Control]]

## Solved Examples
- [[Example - Stop Priority Motor Latch]]

## Exam Tasks
- [[Task 1 - PLC Wiring Diagram]]
- [[Task 2 - Start Stop Motor]]
