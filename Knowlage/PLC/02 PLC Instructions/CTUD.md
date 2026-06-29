---
title: CTUD
tags:
  - #instruction
  - #counter
---

# CTUD

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Count up and down in one function block.

## Syntax
```iecst
CTUD(CU := Bool, CD := Bool, R := Bool, LD := Bool, PV := Int, QU => Bool, QD => Bool, CV => Int)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `CU` | `BOOL` | Count-up pulse input. |
| `CD` | `BOOL` | Count-down pulse input. |
| `R` | `BOOL` | Reset to zero. |
| `LD` | `BOOL` | Load preset. |
| `PV` | `INT` | Preset value. |
| `QU` | `BOOL` | CV >= PV. |
| `QD` | `BOOL` | CV <= 0. |
| `CV` | `INT` | Current count. |

## Execution Behavior
- CU rising edge increments CV.
- CD rising edge decrements CV.
- R and LD define initialization behavior.
- QU and QD report upper/lower limits.

## Timing Diagram
```text
CU/CD events change CV up or down; QU when CV>=PV, QD when CV<=0.
```

## Common Mistakes
- Letting CU and CD happen in the same scan without defining priority.
- Not documenting limits.
- Sharing one counter between unrelated axes/items.

## Ladder Example
```text
[ CTUD PositionCount, CU=ForwardPulse, CD=ReversePulse, PV=100 ]
```

## Structured Text Example
```iecst
PositionCount(CU := ForwardPulse, CD := ReversePulse, R := Reset, LD := Load, PV := 100);
```

## Applications
- [[Parts Counting]]
- [[Position Tracking]]

## Solved Tasks
- No direct solved task yet.

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
