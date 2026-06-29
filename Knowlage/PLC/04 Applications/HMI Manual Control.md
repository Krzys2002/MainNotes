---
title: HMI Manual Control
tags:
  - #application
  - #hmi
  - #exam
---

# HMI Manual Control

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
Allow HMI control of a drive and display drive status.

## Solution Strategy
- Create Auto/Manual mode.
- Use command arbitration so local stop and faults dominate.
- Display command, running feedback, fault, interlock, and mode.
- Require a fresh start command after mode changes or faults.

## Required PLC Instructions
- [[SET]]
- [[RESET]]
- [[COMPARE]]

## Related Theory
- [[HMI and Manual Control]]
- [[PLC Memory]]
- [[Emergency Stop]]

## Solved Examples
- [[Example - HMI Drive Command Arbitration]]

## Exam Tasks
- [[Task 15 - HMI Drive Control]]
