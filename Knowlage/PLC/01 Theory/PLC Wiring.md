---
title: PLC Wiring
tags:
  - #theory
  - #hardware
  - #exam
---

# PLC Wiring

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
Represent safe electrical connections between field devices, PLC modules, relays, and actuators.

## Purpose
- Represent safe electrical connections between field devices, PLC modules, relays, and actuators.

## When To Use
Use for drawing input/output wiring and checking whether PLC logic matches real terminals.

## Important Properties
- Start buttons are commonly NO, stop buttons commonly NC.
- PNP sensors source current to a PLC input.
- Relay/contactors isolate PLC outputs from motor power circuits.
- Indicator lights are ordinary output loads but must still match voltage/current ratings.

## Limitations
- Wiring diagrams do not replace safety design.
- The PLC logic symbol is not always identical to the physical contact type.

## Common Mistakes
- No common/reference connection between sensor supply and PLC input module.
- No protection for inductive relay coils.
- No separation between control and power circuits.

## Related Concepts
- [[Digital Inputs and Outputs]]
- [[Emergency Stop]]
- [[PNP Sensor]]

## Practical Applications
- [[Motor Start-Stop]]
- [[Emergency Stop]]
