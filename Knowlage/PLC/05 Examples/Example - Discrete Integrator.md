---
title: Example - Discrete Integrator
tags:
  - #example
  - #pid
  - #structured-text
---

# Example - Discrete Integrator

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
Approximate G(s)=k/(T*s) with k=2.5 and T=3 s.

## Solution
The continuous equation is dy/dt = (k/T) * u. Forward Euler gives y[k] = y[k-1] + Ts*(k/T)*u[k-1 or k].

## Explanation
- The sample time Ts must be in seconds.
- Use a cyclic interrupt for deterministic execution.
- Store Y between calls because it is the integrator state.

## Ladder Implementation
```text
Use FBD/ST for clarity.
```

## Structured Text Implementation
```iecst
(* Called every Ts seconds *)
Y := Y + Ts * (2.5 / 3.0) * U;
Y := LIMIT(MN := Y_Min, IN := Y, MX := Y_Max);
```

## Alternative Implementations
- Use vendor-provided function blocks where they reduce risk.
- Use SFC or an explicit state machine when the example grows into a sequence.

## Full Working Code

### Mermaid Diagram
```mermaid
flowchart LR
    U["Input u"] --> Gain["Ts * k/T"]
    Gain --> Sum["Add to previous Y"]
    Sum --> Y["Output y"]
    Y --> Memory["Stored state"]
    Memory --> Sum
```

### Assumptions And I/O
- The block is called at a fixed sample period Ts_s.
- G(s)=k/(T*s) is implemented as an accumulator.
- Y is retained as the integrator state.

### Variable Declaration
```iecst
FUNCTION_BLOCK FB_DiscreteIntegrator
VAR_INPUT
    U     : REAL;
    Ts_s  : REAL := 0.1;
    K     : REAL := 2.5;
    T_s   : REAL := 3.0;
    Reset : BOOL;
END_VAR
VAR_OUTPUT
    Y : REAL;
END_VAR
END_FUNCTION_BLOCK
```

### Structured Text Program
```iecst
(* Input section *)
(* U is the current sample. Ts_s is in seconds. *)

(* Work section *)
IF Reset THEN
    Y := 0.0;
ELSIF T_s > 0.0 THEN
    Y := Y + Ts_s * (K / T_s) * U;
END_IF;

(* Output section *)
(* Y is updated once per call. *)
```

### Test Checklist
- Reset sets Y to zero.
- A constant positive U makes Y ramp upward.
- Changing Ts_s changes the integration rate.

## Related Concepts
- [[Discrete Approximation]]
- [[Digital Approximation in PLC]]
- [[Task 9 - Digital Approximation]]
