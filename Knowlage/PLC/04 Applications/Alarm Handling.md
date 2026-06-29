---
title: Alarm Handling
tags:
  - #application
  - #memory
---

# Alarm Handling

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
Detect, latch, acknowledge, and display abnormal conditions.

## Solution Strategy
- Use separate bits for condition active, alarm latched, acknowledged, and reset allowed.
- Latch alarms with SET and clear only when condition is gone and acknowledge/reset is received.
- Timestamp and classify alarms in real systems.

## Required PLC Instructions
- [[SET]]
- [[RESET]]
- [[R_TRIG]]
- [[F_TRIG]]

## Related Theory
- [[PLC Memory]]
- [[HMI and Manual Control]]
- [[Edge Detection]]

## Solved Examples
- [[Example - Latched Alarm With Acknowledge]]

## Exam Tasks
- No direct task yet.
