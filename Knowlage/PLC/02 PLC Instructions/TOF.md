---
title: TOF
tags:
  - #instruction
  - #timer
---

# TOF

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Off-delay timer. Keep Q TRUE for PT after IN becomes FALSE.

## Syntax
```iecst
TOF(IN := Bool, PT := Time, Q => Bool, ET => Time)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `IN` | `BOOL` | Condition to hold output. |
| `PT` | `TIME` | Off-delay time. |
| `Q` | `BOOL` | Output that drops after delay. |
| `ET` | `TIME` | Elapsed off-delay time. |

## Execution Behavior
- IN TRUE sets Q TRUE.
- When IN falls, timing starts.
- Q becomes FALSE after PT if IN stays FALSE.

## Timing Diagram
```text
IN: ___|-----|________
Q : ___|----------|___
ET:          0..PT
```

## Common Mistakes
- Using TOF to delay an output turn-on.
- Forgetting that IN TRUE immediately resets the off-delay.
- Using it for safety stops where immediate drop-out is required.

## Ladder Example
```text
| FanRequest |----[ TOF T_Off, PT=T#10s ]----( Fan )
```

## Structured Text Example
```iecst
T_Off(IN := FanRequest, PT := T#10s);
Fan := T_Off.Q;
```

## Applications
- [[Pump Control]]
- [[Alarm Handling]]

## Solved Tasks
- No direct solved task yet.

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
