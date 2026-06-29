---
title: Reusable Function Block
tags:
  - #application
  - #iec61131
  - #structured-text
---

# Reusable Function Block

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Problem Pattern
Create reusable logic with state, inputs, outputs, and clear reset behavior.

## Solution Strategy
- Choose FUNCTION when no memory is required.
- Choose FUNCTION_BLOCK when internal state or instances are required.
- Declare typed VAR_INPUT and VAR_OUTPUT.
- Document edge cases such as n=0 or reset.

## Required PLC Instructions
- [[MOVE]]
- [[LIMIT]]

## Related Theory
- [[Function Blocks]]
- [[IEC 61131-3]]

## Solved Examples
- [[Example - Arithmetic Sequence Function]]

## Exam Tasks
- [[Task 8 - Arithmetic Sequence Block]]
