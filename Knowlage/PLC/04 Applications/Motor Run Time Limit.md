---
title: Motor Run Time Limit
tags:
  - #application
  - #timer
  - #exam
---

# Motor Run Time Limit

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
Allow the motor to run for at most 5 minutes after Start.

## Solution Strategy
- Latch the run request on Start.
- Run a TON while Motor is TRUE.
- Reset the latch when Stop is pressed or the timer Q becomes TRUE.
- Document whether pressing Start after timeout is allowed immediately.

## Required PLC Instructions
- [[TON]]
- [[RESET]]

## Related Theory
- [[Timers]]
- [[Start-Stop Latch]]
- [[PLC Scan Cycle]]

## Solved Examples
- [[Example - Five Minute Motor Limit]]

## Exam Tasks
- [[Task 3 - Motor Run Time Limit]]
