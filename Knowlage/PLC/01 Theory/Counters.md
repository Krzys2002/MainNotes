---
title: Counters
tags:
  - #theory
  - #counter
  - #instruction
---

# Counters

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
Count events detected by boolean transitions.

## Purpose
- Count events detected by boolean transitions.

## When To Use
Use counters for parts, pulses, edges, sequence steps, and repeated attempts.

## Important Properties
- IEC counters are function blocks with current value CV and preset PV.
- CTU counts up, CTD counts down, CTUD counts both directions.
- Count inputs are edge-sensitive in standard IEC behavior.
- Reset/load inputs define how the current value is initialized.

## Limitations
- Fast hardware pulses may require high-speed counter inputs.
- Counts can be lost if events occur faster than the scan can observe.

## Common Mistakes
- Counting a level manually without edge detection.
- Not resetting CV before a new production batch.
- Using signed/unsigned types inconsistently.

## Related Concepts
- [[CTU]]
- [[CTD]]
- [[CTUD]]
- [[R_TRIG]]
- [[High Speed Counting]]

## Practical Applications
- [[Parts Counting]]
- [[Shift Register]]
- [[Periodic Signal Generation]]
