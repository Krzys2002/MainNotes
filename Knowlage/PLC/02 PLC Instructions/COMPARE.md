---
title: COMPARE
tags:
  - #instruction
  - #application
---

# COMPARE

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Evaluate relations such as less than, greater than, equality, and ranges.

## Syntax
```iecst
A < B, A <= B, A = B, A >= B, A > B, A <> B
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `A` | `Numeric/BOOL` | Left operand. |
| `B` | `Numeric/BOOL` | Right operand. |
| `Result` | `BOOL` | Comparison output. |

## Execution Behavior
- The comparison output is TRUE when the relation is satisfied.
- Use combined comparisons for ranges.
- REAL equality should be avoided for noisy analog values.

## Timing Diagram
```text
Input ----[ < 2.0 ]---- OutA
```

## Common Mistakes
- No hysteresis around analog thresholds.
- Using equality with floating point process values.
- Leaving gaps or overlaps between ranges.

## Ladder Example
```text
| AnalogValue < 2.0 |----( OutA )
```

## Structured Text Example
```iecst
OutA := Voltage < 2.0;
OutB := (Voltage >= 2.0) AND (Voltage <= 8.0);
OutC := Voltage > 8.0;
```

## Applications
- [[Analog Threshold Classification]]
- [[Alarm Handling]]
- [[Tank Filling]]

## Solved Tasks
- [[Task 7 - Formula With Limits]]
- [[Task 13 - Analog Threshold Outputs]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
