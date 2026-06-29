---
title: Sequential Machine
tags:
  - #application
  - #sfc
  - #exam
---

# Sequential Machine

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
Control multi-step or concurrent processes with clear start, finish, and restart conditions.

## Solution Strategy
- Define initial, running, waiting, finished, and reset states.
- Use SFC for parallel branches when two processes run concurrently.
- Set TotalFinish only after both branches finish.
- Restart both processes from a single TotalStart command.

## Required PLC Instructions
- [[SET]]
- [[RESET]]
- [[R_TRIG]]

## Related Theory
- [[Sequential Programming]]
- [[Sequential Function Chart (SFC)]]
- [[Function Blocks]]

## Solved Examples
- [[Example - Parallel SFC Processes]]

## Exam Tasks
- [[Task 12 - Parallel SFC Processes]]
