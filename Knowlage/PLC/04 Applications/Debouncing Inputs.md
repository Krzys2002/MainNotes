---
title: Debouncing Inputs
tags:
  - #application
  - #timer
---

# Debouncing Inputs

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
Prevent mechanical bounce or noisy inputs from generating multiple events.

## Solution Strategy
- Filter in hardware/module settings when possible.
- Use TON to require stable TRUE before accepting a press.
- Use edge detection after debounce, not before.
- Choose debounce time short enough for usability.

## Required PLC Instructions
- [[TON]]
- [[R_TRIG]]
- [[F_TRIG]]

## Related Theory
- [[Edge Detection]]
- [[PLC Scan Cycle]]
- [[Timers]]

## Solved Examples
- [[Example - Debounced Start Button]]

## Exam Tasks
- [[Task 11 - One Bit Shift Register]]
