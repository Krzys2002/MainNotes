---
title: Example - Polynomial Clamp
tags:
  - #example
  - #structured-text
  - #exam
---

# Example - Polynomial Clamp

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Problem Statement
Compute y = x^2 + 5x - 10 and limit y to -10..40.

## Solution
Use REAL math and LIMIT after calculation.

## Explanation
- The clamp applies to final y, not to x.
- Use REAL constants to avoid integer truncation.
- This task is naturally solved in ST.

## Ladder Implementation
```text
[ MUL x x ] + [ MUL 5.0 x ] - 10.0 -> LIMIT
```

## Structured Text Implementation
```iecst
Y_raw := X * X + 5.0 * X - 10.0;
Y := LIMIT(MN := -10.0, IN := Y_raw, MX := 40.0);
```

## Alternative Implementations
- Use vendor-provided function blocks where they reduce risk.
- Use SFC or an explicit state machine when the example grows into a sequence.

## Full Working Code

### Mermaid Diagram
```mermaid
flowchart LR
    X["X REAL"] --> Formula["X*X + 5*X - 10"]
    Formula --> Limit["LIMIT -10..40"]
    Limit --> Y["Y"]
```

### Assumptions And I/O
- X is a valid REAL number.
- The formula is evaluated first.
- Only the final result Y is clamped.

### Variable Declaration
```iecst
PROGRAM PolynomialClamp
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
(* X is already a REAL engineering value. *)

(* Work section *)
Y_Raw := X * X + 5.0 * X - 10.0;
Y := LIMIT(MN := -10.0, IN := Y_Raw, MX := 40.0);

(* Output section *)
(* Y and Y_Raw are exposed for monitoring. *)
```

### Test Checklist
- X = 0 gives Y_Raw = -10 and Y = -10.
- Large positive X clamps Y to 40.
- Use REAL constants such as 5.0 and 10.0.

## Related Concepts
- [[Formula Calculation and Clamping]]
- [[LIMIT]]
- [[Task 7 - Formula With Limits]]
