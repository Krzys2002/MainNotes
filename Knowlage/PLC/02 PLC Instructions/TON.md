---
title: TON
tags:
  - #instruction
  - #timer
---

# TON

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
On-delay timer. Turn Q on only after IN has been TRUE continuously for PT.

## Syntax
```iecst
TON(IN := Bool, PT := Time, Q => Bool, ET => Time)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `IN` | `BOOL` | Timer enable input. |
| `PT` | `TIME` | Preset delay. |
| `Q` | `BOOL` | TRUE after elapsed time reaches PT. |
| `ET` | `TIME` | Elapsed time while IN is TRUE. |

## Execution Behavior
- IN FALSE resets Q to FALSE and ET to zero.
- IN TRUE starts timing.
- Q becomes TRUE when ET >= PT and stays TRUE while IN remains TRUE.

## Timing Diagram
```text
IN: ___|--------|____
ET:    0..PT----0
Q : _______|----|____
```

## Common Mistakes
- Using TON for a fixed-width pulse. Use TP instead.
- Not calling the same timer instance every scan.
- Expecting Q to stay TRUE after IN becomes FALSE.

## Ladder Example
```text
| Start |----[ TON T1, PT=T#5s ]----( MotorAllowed )
```

## Structured Text Example
```iecst
T1(IN := Start, PT := T#5s);
MotorAllowed := T1.Q;
```

## Applications
- [[Motor Run Time Limit]]
- [[Debouncing Inputs]]
- [[Periodic Signal Generation]]

## Solved Tasks
- [[Task 3 - Motor Run Time Limit]]
- [[Task 4 - Motor Light Flashing]]
- [[Task 5 - Timed Output Pattern]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
