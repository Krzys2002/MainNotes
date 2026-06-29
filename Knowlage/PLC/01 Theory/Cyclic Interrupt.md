---
title: Cyclic Interrupt
tags:
  - #theory
  - #exam
  - #timer
---

# Cyclic Interrupt

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
Run code at a configured fixed interval independent of the main scan.

## Purpose
- Run code at a configured fixed interval independent of the main scan.

## When To Use
Use for precise periodic calculation, digital control, sampling, and timer-free pulse generation.

## Important Properties
- Siemens cyclic interrupt OBs execute at configured intervals.
- The sampling period must be known and documented.
- Keep interrupt logic short and deterministic.
- Shared variables need careful access rules.

## Limitations
- Interrupts can overload the CPU if called too often.
- Jitter and priority still exist.

## Common Mistakes
- Doing heavy HMI or communication logic in a cyclic interrupt.
- Forgetting to scale discrete equations by sample time.
- Assuming a timer and a cyclic interrupt have identical behavior.

## Related Concepts
- [[PLC Scan Cycle]]
- [[Discrete Approximation]]
- [[Periodic Signal Generation]]

## Practical Applications
- [[Cyclic Interrupt Pulse Generator]]
- [[Digital PI Controller]]
- [[Periodic Signal Generation]]
