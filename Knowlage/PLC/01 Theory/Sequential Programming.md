---
title: Sequential Programming
tags:
  - #theory
  - #sfc
  - #exam
---

# Sequential Programming

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
Model a machine as states, transitions, actions, and interlocks.

## Purpose
- Model a machine as states, transitions, actions, and interlocks.

## When To Use
Use for machines that must do steps in a controlled order.

## Important Properties
- Each state has actions and permitted transitions.
- The active state is stored explicitly as a step bit or enum.
- Parallel branches handle concurrent processes.
- SFC is an IEC language designed for this structure.

## Limitations
- Poorly defined reset and fault states make sequences unsafe.
- Complex alternatives need careful priority rules.

## Common Mistakes
- Driving outputs directly from many unrelated rungs instead of from the active state.
- No initial step after restart.
- No timeout or fault escape for stuck sensors.

## Related Concepts
- [[Sequential Function Chart (SFC)]]
- [[State Machine]]
- [[SET]]
- [[RESET]]

## Practical Applications
- [[Sequential Machine]]
- [[Traffic Lights]]
- [[Tank Filling]]
