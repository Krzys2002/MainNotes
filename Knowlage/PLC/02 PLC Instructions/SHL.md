---
title: SHL
tags:
  - #instruction
  - #memory
  - #exam
---

# SHL

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Shift bits left in a byte, word, or integer value.

## Syntax
```iecst
SHL(IN := Value, N := Count)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `IN` | `Bit string/integer` | Value to shift. |
| `N` | `INT` | Number of bit positions. |

## Execution Behavior
- Moves bits toward the more significant side.
- Zeros enter from the right.
- Use wrap logic if the leftmost bit must return to the rightmost position.

## Timing Diagram
```text
0000_0001 --SHL 1--> 0000_0010
```

## Common Mistakes
- No rising edge, causing many shifts per button press.
- No wrap at the left end.
- Using signed types where bit behavior is unclear.

## Ladder Example
```text
[ SHL IN:=QB0 N:=1 OUT:=QB0 ]
```

## Structured Text Example
```iecst
QB0 := SHL(IN := QB0, N := 1);
```

## Applications
- [[One Bit Shift Register]]

## Solved Tasks
- [[Task 11 - One Bit Shift Register]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
