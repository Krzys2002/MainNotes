---
title: R_TRIG
tags:
  - #instruction
  - #exam
---

# R_TRIG

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Detect a rising edge and output TRUE for one scan.

## Syntax
```iecst
R_TRIG(CLK := Bool, Q => Bool)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `CLK` | `BOOL` | Input signal. |
| `Q` | `BOOL` | One-scan pulse on FALSE to TRUE transition. |

## Execution Behavior
- Stores previous CLK internally.
- Q TRUE for one call after CLK rises.
- Requires a separate instance for each signal.

## Timing Diagram
```text
CLK: __|----|___
Q  : __|_|______
```

## Common Mistakes
- Calling only when CLK is TRUE.
- Reusing one trigger instance for several buttons.
- No debounce before edge detection on mechanical contacts.

## Ladder Example
```text
| In1 |----[ R_TRIG Edge1 ]----( ShiftPulse )
```

## Structured Text Example
```iecst
Edge1(CLK := In1);
IF Edge1.Q THEN
    ShiftRegister := SHL(ShiftRegister, 1);
END_IF;
```

## Applications
- [[One Bit Shift Register]]
- [[Counter Pulse Counting]]
- [[Debouncing Inputs]]

## Solved Tasks
- [[Task 11 - One Bit Shift Register]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
