---
title: Task 7 - Formula With Limits
tags:
  - #exam
  - #example
---

# Task 7 - Formula With Limits

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Original Scan
![[Attachments/Task Scans/T_7.jpg]]

## Problem Statement
For a valid real input x, determine y = x^2 + 5.0*x - 10.0. After calculation, limit y to the range -10.0 <= y <= 40.0.

## Analysis
- This is an ST-friendly formula task.
- The range limit applies to y after the polynomial is computed.
- Use REAL constants and LIMIT.

## Solution
- Y_raw := X * X + 5.0 * X - 10.0.
- Y := LIMIT(MN := -10.0, IN := Y_raw, MX := 40.0).

## Explanation
- This task belongs to the exam pattern practiced in the scanned task set.
- Prefer symbolic variables and clearly state assumptions such as input polarity, sample time, and analog range.

## Common Mistakes
- Ignoring stop/fault priority.
- Forgetting edge detection for per-press actions.
- Comparing unscaled analog raw values to engineering thresholds.
- Reusing one timer/counter/trigger instance for unrelated logic.

## Full Working Solution

### Mermaid Diagram
```mermaid
flowchart LR
    X --> Formula["x^2 + 5x - 10"]
    Formula --> Clamp["LIMIT -10..40"]
    Clamp --> Y
```

### Assumptions And I/O
- Names are symbolic and can be mapped to real PLC addresses in the tag table.
- The code is written in IEC 61131-3 Structured Text style; vendor syntax may need small adjustments.
- Safety functions shown in software are educational; real emergency-stop circuits require safety-rated hardware.

### Variable Declaration
```iecst
PROGRAM Task7_FormulaLimit
VAR_INPUT
    X : REAL;
END_VAR
VAR_OUTPUT
    Y     : REAL;
    Y_Raw : REAL;
END_VAR
```

### Structured Text Program
```iecst
(* Input section *)
(* X is a valid REAL number. *)

(* Work section *)
Y_Raw := X * X + 5.0 * X - 10.0;

(* Output section *)
Y := LIMIT(MN := -10.0, IN := Y_Raw, MX := 40.0);
```

### Test Checklist
- X = 0 gives Y = -10.
- Very large X gives Y = 40.
- The clamp is applied after the formula.

## Related Theory
- [[Structured Text (ST)]]
- [[Analog Scaling]]

## Related PLC Instructions
- [[LIMIT]]
- [[COMPARE]]

## Related Applications
- [[Formula Calculation and Clamping]]
