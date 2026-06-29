---
title: PLC Instruction Reference
tags:
  - #cheat-sheet
  - #exam
---

# PLC Instruction Reference

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
- [[TON]] - On-delay timer. Turn Q on only after IN has been TRUE continuously for PT.
- [[TOF]] - Off-delay timer. Keep Q TRUE for PT after IN becomes FALSE.
- [[TP]] - Pulse timer. Generate a fixed-width TRUE pulse after a rising edge at IN.
- [[CTU]] - Count up on rising edges until the current value reaches preset PV.
- [[CTD]] - Count down on rising edges from a loaded preset value.
- [[CTUD]] - Count up and down in one function block.
- [[SET]] - Latch a boolean TRUE until another instruction resets it.
- [[RESET]] - Clear a latched boolean FALSE.
- [[MOVE]] - Copy a value from one variable to another.
- [[COMPARE]] - Evaluate relations such as less than, greater than, equality, and ranges.
- [[R_TRIG]] - Detect a rising edge and output TRUE for one scan.
- [[F_TRIG]] - Detect a falling edge and output TRUE for one scan.
- [[LIMIT]] - Clamp a numeric value between a minimum and maximum.
- [[NORM_X]] - Normalize a value from a physical/raw range to a 0.0 to 1.0 fraction.
- [[SCALE_X]] - Scale a normalized fraction to engineering units.
- [[SHL]] - Shift bits left in a byte, word, or integer value.
- [[PID_Compact]] - Siemens technology object/block for PID control in S7-1200/S7-1500 style projects.

## Related
- [[Exam Preparation]]
- [[PLC Instructions]]
