---
title: Task 14 - Variable Output Pulse Mode
tags:
  - #exam
  - #example
---

# Task 14 - Variable Output Pulse Mode

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
![[Attachments/Task Scans/T_14-15.jpg]]

## Problem Statement
Transform the program from Task 13 so that, depending on the input value, the switching mode of OutA is changed. For example, use PWM with constant period or variable signal period.

## Analysis
- The analog value should map to timing behavior.
- PWM uses constant period and variable duty cycle.
- Variable period keeps pulse width or duty relation and changes cycle time.

## Solution
- Scale input to a duty value or period value.
- Use a cyclic time base and compare phase time to duty/period.
- Keep OutB/OutC behavior clearly defined if OutA changes from static to pulsed.

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
    RawAI --> Scale["Scale to Voltage"]
    Scale --> Duty["Map to duty 0..100 percent"]
    Duty --> PWM["PWM phase compare"]
    PWM --> OutA
```

### Assumptions And I/O
- Names are symbolic and can be mapped to real PLC addresses in the tag table.
- The code is written in IEC 61131-3 Structured Text style; vendor syntax may need small adjustments.
- Safety functions shown in software are educational; real emergency-stop circuits require safety-rated hardware.

### Variable Declaration
```iecst
PROGRAM Task14_VariablePWM
VAR_INPUT
    RawAI  : INT;
    Enable : BOOL;
END_VAR
VAR_OUTPUT
    Voltage : REAL;
    OutA    : BOOL;
END_VAR
VAR
    Norm        : REAL;
    DutyPercent : REAL;
    Tick        : INT;
END_VAR
```

### Structured Text Program
```iecst
(* Input section *)
Norm := NORM_X(MIN := 0, VALUE := RawAI, MAX := 27648);
Norm := LIMIT(MN := 0.0, IN := Norm, MX := 1.0);
Voltage := SCALE_X(MIN := 0.0, VALUE := Norm, MAX := 10.0);

(* Work section *)
(* Called every 100 ms. Period = 2 s = 20 ticks. *)
IF Enable THEN
    Tick := Tick + 1;
    IF Tick >= 20 THEN
        Tick := 0;
    END_IF;
ELSE
    Tick := 0;
END_IF;

DutyPercent := LIMIT(MN := 0.0, IN := Voltage * 10.0, MX := 100.0);

(* Output section *)
OutA := Enable AND (INT_TO_REAL(Tick) < DutyPercent / 5.0);
```

### Test Checklist
- Voltage 0 V gives 0 percent duty.
- Voltage 5 V gives about 50 percent duty.
- Voltage 10 V gives 100 percent duty.
- The period remains constant at 2 s.

## Related Theory
- [[Analog Scaling]]
- [[Timers]]
- [[Cyclic Interrupt]]

## Related PLC Instructions
- [[TP]]
- [[COMPARE]]
- [[SCALE_X]]

## Related Applications
- [[Analog Threshold Classification]]
- [[Periodic Signal Generation]]
