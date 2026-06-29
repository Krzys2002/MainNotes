---
title: PLC Scan Cycle
tags:
  - #theory
  - #plc
  - #exam
---

# PLC Scan Cycle

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
Explain how a PLC repeats input sampling, program execution, communication/diagnostics, and output update.

## Purpose
- Explain how a PLC repeats input sampling, program execution, communication/diagnostics, and output update.

## When To Use
Use this whenever timing, one-shot behavior, interrupts, or output races are confusing.

## Important Properties
- Inputs are usually copied into a process image before logic executes.
- Outputs are normally written after the logic scan, so a coil value is the result of the current scan.
- Fast events can be missed if their pulse width is shorter than the scan or input filter.
- Interrupt OBs or high-speed counters are used when normal cyclic execution is not deterministic enough.

## Limitations
- Do not assume code executes continuously between scans.
- Do not use scan-dependent toggles for accurate time unless a fixed cyclic interrupt is used.

## Common Mistakes
- Using a level signal where a rising edge is required.
- Expecting a timer to update while its instance is not called.
- Ignoring input filter time when diagnosing missed pulses.

## Related Concepts
- [[Cyclic Interrupt]]
- [[Edge Detection]]
- [[PLC Memory]]
- [[R_TRIG]]
- [[F_TRIG]]

## Practical Applications
- [[Debouncing Inputs]]
- [[Periodic Signal Generation]]
- [[High Speed Counting]]
