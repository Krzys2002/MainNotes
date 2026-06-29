---
title: CTU
tags:
  - #instruction
  - #counter
---

# CTU

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Count up on rising edges until the current value reaches preset PV.

## Syntax
```iecst
CTU(CU := Bool, R := Bool, PV := Int, Q => Bool, CV => Int)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `CU` | `BOOL` | Count-up pulse input. |
| `R` | `BOOL` | Reset input. |
| `PV` | `INT` | Preset value. |
| `Q` | `BOOL` | TRUE when CV >= PV. |
| `CV` | `INT` | Current count. |

## Execution Behavior
- Each CU rising edge increments CV.
- R resets CV to zero.
- Q is TRUE when CV reaches or exceeds PV.

## Timing Diagram
```text
CU: _|_|_|_|_
CV: 0 1 2 3 4
Q : ______|---  if PV=3
```

## Common Mistakes
- Counting every scan by feeding a level into custom add logic.
- No reset between batches.
- Using CTU for very fast pulses instead of hardware counter.

## Ladder Example
```text
| Sensor |----[ CTU C1, PV=10 ]----( BatchDone )
```

## Structured Text Example
```iecst
C1(CU := SensorPulse, R := ResetCount, PV := 10);
BatchDone := C1.Q;
```

## Applications
- [[Parts Counting]]
- [[Counter Pulse Counting]]

## Solved Tasks
- No direct solved task yet.

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
