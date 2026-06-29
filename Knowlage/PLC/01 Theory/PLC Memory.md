---
title: PLC Memory
tags:
  - #theory
  - #memory
  - #iec61131
---

# PLC Memory

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
Describe where PLC values live: inputs, outputs, memory bits, data blocks, temporary variables, and retentive memory.

## Purpose
- Describe where PLC values live: inputs, outputs, memory bits, data blocks, temporary variables, and retentive memory.

## When To Use
Use this when deciding whether a value must persist, be shared, or be local to one block.

## Important Properties
- I/Q areas represent physical input/output process images.
- Memory bits are convenient but become hard to maintain in larger projects.
- Data blocks and symbolic tags are preferred in modern Siemens projects.
- Retentive tags keep values through stop/start or power loss, depending on CPU configuration.

## Limitations
- Retentive memory is limited and should not be used for everything.
- Temporary variables are lost after the block call.

## Common Mistakes
- Using absolute addresses everywhere instead of symbolic names.
- Forgetting that an FB needs instance memory for timers, counters, and internal states.
- Making safety-relevant state retentive without a deliberate reset strategy.

## Related Concepts
- [[Data Blocks]]
- [[Retentive Memory]]
- [[Function Blocks]]
- [[IEC 61131-3]]

## Practical Applications
- [[Start-Stop Latch]]
- [[Sequential Machine]]
- [[HMI Manual Control]]
