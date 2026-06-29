---
title: Tank Filling
tags:
  - #application
  - #sfc
---

# Tank Filling

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
Fill, monitor, drain, and refill tanks using level sensors and valves.

## Solution Strategy
- Model empty/filling/full/draining as states.
- Use interlocks so fill and drain valves are not open incorrectly.
- Use SFC for two tanks or repeated cycles.
- Add timeout alarms for stuck sensors.

## Required PLC Instructions
- [[SET]]
- [[RESET]]
- [[TON]]

## Related Theory
- [[Sequential Programming]]
- [[Sequential Function Chart (SFC)]]
- [[Digital Inputs and Outputs]]

## Solved Examples
- [[Example - Tank Fill Sequence]]

## Exam Tasks
- [[Task 12 - Parallel SFC Processes]]
