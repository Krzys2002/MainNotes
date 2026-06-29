---
title: Periodic Signal Generation
tags:
  - #application
  - #timer
  - #exam
---

# Periodic Signal Generation

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
Generate repeated output pulses or blinking signals.

## Solution Strategy
- For simple blinking, use a timer-driven state bit.
- For precise timing, use a cyclic interrupt and an elapsed counter.
- For fixed pulse width, use TP.
- Reset timers and counters when enable input is FALSE.

## Required PLC Instructions
- [[TON]]
- [[TP]]
- [[R_TRIG]]

## Related Theory
- [[Timers]]
- [[Cyclic Interrupt]]
- [[PLC Scan Cycle]]

## Solved Examples
- [[Example - 2 Second Blinker]]
- [[Example - Two Output Timing Pattern]]

## Exam Tasks
- [[Task 4 - Motor Light Flashing]]
- [[Task 5 - Timed Output Pattern]]
- [[Task 6 - Cyclic Interrupt Timing]]
