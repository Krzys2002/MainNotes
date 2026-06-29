---
title: CTD
tags:
  - #instruction
  - #counter
---

# CTD

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Count down on rising edges from a loaded preset value.

## Syntax
```iecst
CTD(CD := Bool, LD := Bool, PV := Int, Q => Bool, CV => Int)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `CD` | `BOOL` | Count-down pulse input. |
| `LD` | `BOOL` | Load preset into CV. |
| `PV` | `INT` | Preset starting value. |
| `Q` | `BOOL` | TRUE when CV <= 0. |
| `CV` | `INT` | Current count. |

## Execution Behavior
- LD loads CV with PV.
- Each CD rising edge decrements CV.
- Q indicates the count has reached zero.

## Timing Diagram
```text
CD: _|_|_|_
CV: 3 2 1 0
Q : ______|-
```

## Common Mistakes
- Forgetting to load before counting.
- Assuming reset semantics are identical to CTU.
- Allowing CV to go below zero without checking vendor behavior.

## Ladder Example
```text
| ItemUsed |----[ CTD Stock, PV=20 ]----( Empty )
```

## Structured Text Example
```iecst
Stock(CD := ItemUsed, LD := LoadStock, PV := 20);
Empty := Stock.Q;
```

## Applications
- [[Parts Counting]]

## Solved Tasks
- No direct solved task yet.

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
