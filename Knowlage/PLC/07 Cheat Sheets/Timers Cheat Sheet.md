---
title: Timers Cheat Sheet
tags:
  - #cheat-sheet
  - #exam
---

# Timers Cheat Sheet

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Quick Review
- TON: on-delay. IN TRUE for PT, then Q TRUE.
- TOF: off-delay. IN FALSE starts delayed drop of Q.
- TP: pulse. Rising edge creates Q TRUE for PT.
- PT is preset time; ET is elapsed time.
- Call timer instances every scan where they should update.
- Use cyclic interrupt for precise repeated timing.

## Related
- [[Exam Preparation]]
- [[PLC Instructions]]
