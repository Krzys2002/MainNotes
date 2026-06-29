---
title: F_TRIG
tags:
  - #instruction
---

# F_TRIG

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Detect a falling edge and output TRUE for one scan.

## Syntax
```iecst
F_TRIG(CLK := Bool, Q => Bool)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `CLK` | `BOOL` | Input signal. |
| `Q` | `BOOL` | One-scan pulse on TRUE to FALSE transition. |

## Execution Behavior
- Stores previous CLK internally.
- Q TRUE for one call after CLK falls.
- Use when a release or loss of signal must trigger logic.

## Timing Diagram
```text
CLK: __|----|___
Q  : ______|_|__
```

## Common Mistakes
- Using falling edge for stop safety logic that should be level-sensitive.
- Missing edges because the trigger is not called every scan.
- No debounce.

## Ladder Example
```text
| RunFeedback |----[ F_TRIG LostRun ]----( AlarmSet )
```

## Structured Text Example
```iecst
LostRun(CLK := RunFeedback);
IF LostRun.Q THEN Alarm := TRUE; END_IF;
```

## Applications
- [[Alarm Handling]]
- [[Edge Detection]]

## Solved Tasks
- No direct solved task yet.

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
