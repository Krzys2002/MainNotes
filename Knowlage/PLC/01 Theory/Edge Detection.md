---
title: Edge Detection
tags:
  - #theory
  - #instruction
  - #exam
---

# Edge Detection

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
Convert a signal transition into a one-scan pulse.

## Purpose
- Convert a signal transition into a one-scan pulse.

## When To Use
Use edge detection when one action must happen once per press, pulse, or event.

## Important Properties
- A rising edge is FALSE to TRUE.
- A falling edge is TRUE to FALSE.
- Edge detectors need memory of the previous input state.
- R_TRIG and F_TRIG are standard function blocks.

## Limitations
- A one-scan pulse can be too short for another asynchronous system.
- Input bounce can create multiple edges.

## Common Mistakes
- Using a pushbutton level to shift a bit every scan.
- Reusing one trigger instance for several signals.
- Calling the trigger conditionally so its memory is not updated.

## Related Concepts
- [[R_TRIG]]
- [[F_TRIG]]
- [[Debouncing Inputs]]
- [[PLC Scan Cycle]]

## Practical Applications
- [[One Bit Shift Register]]
- [[Start-Stop Latch]]
- [[Counter Pulse Counting]]
