---
title: Analog Threshold Classification
tags:
  - #application
  - #analog
  - #exam
---

# Analog Threshold Classification

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
Turn on one of three outputs based on analog voltage ranges.

## Solution Strategy
- Scale raw input to volts.
- Use non-overlapping comparisons.
- Add hysteresis if the physical signal is noisy.
- Make exactly one output TRUE at a time.

## Required PLC Instructions
- [[NORM_X]]
- [[SCALE_X]]
- [[COMPARE]]
- [[LIMIT]]

## Related Theory
- [[Analog Scaling]]
- [[Digital Inputs and Outputs]]

## Solved Examples
- [[Example - Three Range Analog Output]]

## Exam Tasks
- [[Task 13 - Analog Threshold Outputs]]
- [[Task 14 - Variable Output Pulse Mode]]
