---
title: Digital Inputs and Outputs
tags:
  - #theory
  - #hardware
  - #exam
---

# Digital Inputs and Outputs

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
Connect binary sensors, pushbuttons, lamps, relay coils, and contactors to PLC modules.

## Purpose
- Connect binary sensors, pushbuttons, lamps, relay coils, and contactors to PLC modules.

## When To Use
Use for wiring tasks and for deciding whether PLC logic should use NO or NC conditions.

## Important Properties
- Inputs read field signals such as pushbuttons and PNP inductive sensors.
- Outputs drive small loads directly or larger loads through relays/contactors.
- A stop pushbutton is often wired NC so a broken wire behaves like a stop condition.
- Output modules have current, voltage, isolation, and protection limits.

## Limitations
- A PLC output is not a substitute for a safety contactor or safety relay.
- Inductive loads need proper suppression and ratings.

## Common Mistakes
- Drawing the stop button as NO in logic when the electrical device is NC.
- Driving a motor directly from a PLC output.
- Mixing PNP/NPN sensor assumptions.

## Related Concepts
- [[Emergency Stop]]
- [[Start-Stop Latch]]
- [[PLC Wiring]]
- [[PNP Sensor]]

## Practical Applications
- [[Motor Start-Stop]]
- [[Emergency Stop]]
- [[Pump Control]]
