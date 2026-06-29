---
title: MOVE
tags:
  - #instruction
  - #memory
---

# MOVE

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Copy a value from one variable to another.

## Syntax
```iecst
MOVE(IN := Source, OUT => Destination)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `IN` | `ANY` | Source value. |
| `OUT` | `ANY` | Destination variable of compatible type. |

## Execution Behavior
- When enabled, OUT receives IN.
- For simple types it is a direct copy.
- Vendor variants exist for blocks, arrays, and variants.

## Timing Diagram
```text
Source --> MOVE --> Destination
```

## Common Mistakes
- Copying between incompatible types.
- Using MOVE where scaling or conversion is required.
- Overwriting a memory value before it is used later in the scan.

## Ladder Example
```text
[ MOVE IN:=RawAnalog OUT:=RawSaved ]
```

## Structured Text Example
```iecst
RawSaved := RawAnalog;
```

## Applications
- [[Analog Threshold Classification]]
- [[One Bit Shift Register]]

## Solved Tasks
- [[Task 11 - One Bit Shift Register]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
