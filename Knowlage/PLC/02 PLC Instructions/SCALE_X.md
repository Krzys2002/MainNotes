---
title: SCALE_X
tags:
  - #instruction
  - #analog
---

# SCALE_X

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Scale a normalized fraction to engineering units.

## Syntax
```iecst
SCALE_X(MIN := Low, VALUE := Norm, MAX := High)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `MIN` | `Numeric` | Engineering low. |
| `VALUE` | `REAL` | Normalized input. |
| `MAX` | `Numeric` | Engineering high. |

## Execution Behavior
- Maps 0.0 to MIN and 1.0 to MAX.
- Pair with NORM_X for raw analog inputs.
- Use REAL variables for predictable scaling.

## Timing Diagram
```text
0.0..1.0 --> SCALE_X --> 0.0..10.0 V
```

## Common Mistakes
- Skipping normalization.
- Forgetting to clamp out-of-range values.
- Using scale limits that do not match sensor calibration.

## Ladder Example
```text
[ SCALE_X MIN:=0.0 VALUE:=Norm MAX:=10.0 OUT:=Voltage ]
```

## Structured Text Example
```iecst
Voltage := SCALE_X(MIN := 0.0, VALUE := Norm, MAX := 10.0);
```

## Applications
- [[Analog Threshold Classification]]
- [[Temperature Measurement]]

## Solved Tasks
- [[Task 13 - Analog Threshold Outputs]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
