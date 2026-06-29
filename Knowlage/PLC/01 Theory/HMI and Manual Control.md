---
title: HMI and Manual Control
tags:
  - #theory
  - #application
  - #hmi
---

# HMI and Manual Control

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
Add operator commands, status display, and mode selection without breaking local safety logic.

## Purpose
- Add operator commands, status display, and mode selection without breaking local safety logic.

## When To Use
Use when a task asks to control a drive from HMI and show drive state.

## Important Properties
- Separate automatic commands from manual/HMI commands.
- Use mode arbitration so only one source controls the actuator at a time.
- Display command, feedback, fault, interlock, and running status separately.
- HMI commands should be momentary or acknowledged where appropriate.

## Limitations
- HMI must not bypass hardwired emergency stop or safety circuits.
- Network delay makes HMI unsuitable for fast safety actions.

## Common Mistakes
- Letting HMI start a motor after a stop without a fresh command.
- Displaying command as if it were actual feedback.
- No permissions or mode indication.

## Related Concepts
- [[Motor Start-Stop]]
- [[Emergency Stop]]
- [[Start-Stop Latch]]

## Practical Applications
- [[HMI Manual Control]]
- [[Alarm Handling]]
