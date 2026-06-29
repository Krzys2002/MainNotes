---
title: TP
tags:
  - #instruction
  - #timer
---

# TP

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Pulse timer. Generate a fixed-width TRUE pulse after a rising edge at IN.

## Syntax
```iecst
TP(IN := Bool, PT := Time, Q => Bool, ET => Time)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `IN` | `BOOL` | Trigger input. |
| `PT` | `TIME` | Pulse duration. |
| `Q` | `BOOL` | Pulse output. |
| `ET` | `TIME` | Elapsed pulse time. |

## Execution Behavior
- A rising edge starts the pulse.
- Q stays TRUE for PT.
- Further IN changes do not usually extend the pulse until the timer resets.

## Timing Diagram
```text
IN: ___|--|___|------
Q : ___|------|______
          PT
```

## Common Mistakes
- Expecting TP to retrigger continuously while IN is held TRUE.
- Using one TP instance for two pulse sources.
- Using scan toggles when a pulse timer is clearer.

## Ladder Example
```text
| Edge |----[ TP Pulse, PT=T#2s ]----( OutB )
```

## Structured Text Example
```iecst
Pulse(IN := EdgeSignal, PT := T#2s);
OutB := Pulse.Q;
```

## Applications
- [[Periodic Signal Generation]]
- [[Output Pulse Width Modulation]]

## Solved Tasks
- [[Task 5 - Timed Output Pattern]]
- [[Task 14 - Variable Output Pulse Mode]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
