---
title: Function Blocks
tags:
  - #theory
  - #iec61131
  - #application
---

# Function Blocks

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
Encapsulate logic with private memory and typed inputs/outputs.

## Purpose
- Encapsulate logic with private memory and typed inputs/outputs.

## When To Use
Use FBs for reusable behavior that needs state: timers, counters, PID, motion blocks, or custom machine modules.

## Important Properties
- Each FB call needs instance data.
- Inputs are copied into the block, outputs are produced by the block, and internal variables persist.
- Multi-instance FBs let one FB contain instances of other FBs.
- FBs are the natural home for reusable machine functions.

## Limitations
- FB state can hide behavior if names and reset paths are poor.
- Changing instance data layout may require downloads/reinitialization.

## Common Mistakes
- Using a function where persistent memory is required.
- Sharing one FB instance across multiple devices.
- No explicit reset input for stateful behavior.

## Related Concepts
- [[IEC 61131-3]]
- [[Reusable Function Block]]
- [[TON]]
- [[CTU]]
- [[PID_Compact]]

## Practical Applications
- [[Pump Control]]
- [[Alarm Handling]]
- [[Reusable Function Block]]
