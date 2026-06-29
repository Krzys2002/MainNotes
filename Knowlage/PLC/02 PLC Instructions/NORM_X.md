---
title: NORM_X
tags:
  - #instruction
  - #analog
---

# NORM_X

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Normalize a value from a physical/raw range to a 0.0 to 1.0 fraction.

## Syntax
```iecst
NORM_X(MIN := Low, VALUE := In, MAX := High)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `MIN` | `Numeric` | Lower bound. |
| `VALUE` | `Numeric` | Input value. |
| `MAX` | `Numeric` | Upper bound. |

## Execution Behavior
- Computes fraction of VALUE within the input range.
- Usually paired with SCALE_X.
- Can produce values outside 0..1 unless limited.

## Timing Diagram
```text
Raw 0..27648 --> NORM_X --> 0.0..1.0
```

## Common Mistakes
- Using wrong module raw range.
- No LIMIT after normalization.
- Integer division in custom code.

## Ladder Example
```text
[ NORM_X MIN:=0 VALUE:=Raw MAX:=27648 OUT:=Norm ]
```

## Structured Text Example
```iecst
Norm := NORM_X(MIN := 0, VALUE := RawAI, MAX := 27648);
```

## Applications
- [[Analog Threshold Classification]]
- [[Temperature Measurement]]

## Solved Tasks
- [[Task 13 - Analog Threshold Outputs]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
