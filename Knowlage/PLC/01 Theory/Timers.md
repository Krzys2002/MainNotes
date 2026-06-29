---
title: Timers
tags:
  - #theory
  - #timer
  - #instruction
---

# Timers

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Definition
Represent elapsed-time behavior in cyclic PLC programs.

## Purpose
- Represent elapsed-time behavior in cyclic PLC programs.

## When To Use
Use timers for delayed start, delayed stop, pulse generation, watchdogs, and run-time limits.

## Important Properties
- IEC timers are function blocks with instance memory.
- Important signals are IN, PT, Q, and ET.
- TON delays a rising output, TOF delays a falling output, TP creates a fixed pulse.
- Timers must be called every scan where their state should evolve.

## Limitations
- Timer precision is bounded by scan time and timer resolution.
- Do not use a normal cyclic scan timer for high-frequency timing.

## Common Mistakes
- Reusing one timer instance for unrelated actions.
- Expecting ET to reset the same way for TON, TOF, and TP.
- Creating oscillator logic that depends on multiple assignments to the same bit.

## Related Concepts
- [[TON]]
- [[TOF]]
- [[TP]]
- [[Cyclic Interrupt]]

## Practical Applications
- [[Motor Run Time Limit]]
- [[Periodic Signal Generation]]
- [[Debouncing Inputs]]
