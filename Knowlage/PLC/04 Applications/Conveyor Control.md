---
title: Conveyor Control
tags:
  - #application
  - #ladder
---

# Conveyor Control

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
Move items between stations with sensors, motor outputs, and jam detection.

## Solution Strategy
- Start downstream conveyors first and stop upstream first.
- Use photoeye sensors and timers for jam detection.
- Count parts with CTU if needed.
- Use state machine for multi-station systems.

## Required PLC Instructions
- [[TON]]
- [[CTU]]
- [[R_TRIG]]
- [[SET]]
- [[RESET]]

## Related Theory
- [[Sequential Programming]]
- [[Digital Inputs and Outputs]]
- [[Counters]]

## Solved Examples
- [[Example - Conveyor Jam Timer]]

## Exam Tasks
- No direct task yet.
