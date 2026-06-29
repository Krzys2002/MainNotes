---
title: LIMIT
tags:
  - #instruction
  - #structured-text
---

# LIMIT

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Clamp a numeric value between a minimum and maximum.

## Syntax
```iecst
LIMIT(MN := Min, IN := Value, MX := Max)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `MN` | `Numeric` | Minimum allowed value. |
| `IN` | `Numeric` | Input value. |
| `MX` | `Numeric` | Maximum allowed value. |

## Execution Behavior
- Returns MN if IN is lower.
- Returns MX if IN is higher.
- Otherwise returns IN unchanged.

## Timing Diagram
```text
Value --> LIMIT[-10..40] --> ClampedValue
```

## Common Mistakes
- Clamping before a formula when the requirement says clamp after.
- Using integer constants with REAL variables in strict tools.
- Hiding sensor fault values that should alarm.

## Ladder Example
```text
[ LIMIT MN:=-10.0 IN:=Y_raw MX:=40.0 OUT:=Y ]
```

## Structured Text Example
```iecst
Y := LIMIT(MN := -10.0, IN := X * X + 5.0 * X - 10.0, MX := 40.0);
```

## Applications
- [[Formula Calculation and Clamping]]
- [[Analog Threshold Classification]]
- [[PID Control in PLC]]

## Solved Tasks
- [[Task 7 - Formula With Limits]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
