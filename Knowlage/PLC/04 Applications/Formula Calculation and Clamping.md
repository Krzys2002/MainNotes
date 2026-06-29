---
title: Formula Calculation and Clamping
tags:
  - #application
  - #structured-text
  - #exam
---

# Formula Calculation and Clamping

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
Calculate a numerical expression and limit the result to a required range.

## Solution Strategy
- Use REAL variables.
- Calculate the raw formula first.
- Use LIMIT to clamp the final value.
- Keep expression precedence readable with parentheses.

## Required PLC Instructions
- [[LIMIT]]
- [[COMPARE]]

## Related Theory
- [[Structured Text (ST)]]
- [[Analog Scaling]]

## Solved Examples
- [[Example - Polynomial Clamp]]

## Exam Tasks
- [[Task 7 - Formula With Limits]]
