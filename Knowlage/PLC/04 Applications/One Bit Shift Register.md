---
title: One Bit Shift Register
tags:
  - #application
  - #memory
  - #exam
---

# One Bit Shift Register

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
Turn on exactly one bit in QB0 and shift it left on each rising edge, wrapping from the leftmost bit to the rightmost bit.

## Solution Strategy
- Initialize the byte to 2#00000001.
- Use R_TRIG on the input.
- If the current value is 2#10000000, wrap to 2#00000001.
- Otherwise shift left by one.

## Required PLC Instructions
- [[R_TRIG]]
- [[SHL]]
- [[MOVE]]

## Related Theory
- [[Edge Detection]]
- [[PLC Memory]]

## Solved Examples
- [[Example - Running Light Byte]]

## Exam Tasks
- [[Task 11 - One Bit Shift Register]]
