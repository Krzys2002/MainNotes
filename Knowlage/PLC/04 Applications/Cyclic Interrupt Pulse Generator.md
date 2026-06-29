---
title: Cyclic Interrupt Pulse Generator
tags:
  - #application
  - #timer
  - #exam
---

# Cyclic Interrupt Pulse Generator

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
Generate the same pattern as timer logic using a fixed cyclic interrupt.

## Solution Strategy
- Configure a known interrupt period, for example 100 ms.
- Increment an elapsed tick counter only while enabled.
- Use modulo arithmetic to decide output windows.
- Reset counters and outputs when disabled.

## Required PLC Instructions
- [[COMPARE]]
- [[MOVE]]

## Related Theory
- [[Cyclic Interrupt]]
- [[Discrete Approximation]]
- [[PLC Scan Cycle]]

## Solved Examples
- [[Example - Cyclic Interrupt Pulse Pattern]]

## Exam Tasks
- [[Task 6 - Cyclic Interrupt Timing]]
