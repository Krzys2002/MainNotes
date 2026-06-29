---
title: SET
tags:
  - #instruction
  - #ladder
---

# SET

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Purpose
Latch a boolean TRUE until another instruction resets it.

## Syntax
```iecst
SET Coil or S coil
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `Condition` | `BOOL` | When TRUE, the target bit is set. |
| `Target` | `BOOL` | Latched bit. |

## Execution Behavior
- A TRUE condition writes the target TRUE.
- The target remains TRUE after the condition becomes FALSE.
- A RESET path must deliberately clear it.

## Timing Diagram
```text
SetPulse: _|_|____
Bit     : __|----- until Reset
```

## Common Mistakes
- No reset condition.
- Set and reset in multiple networks without clear priority.
- Using SET for outputs that should fail safe.

## Ladder Example
```text
| Start |----(S MotorLatch)
| Stop  |----(R MotorLatch)
```

## Structured Text Example
```iecst
IF Start THEN MotorLatch := TRUE; END_IF;
IF Stop THEN MotorLatch := FALSE; END_IF;
```

## Applications
- [[Start-Stop Latch]]
- [[Motor Start-Stop]]
- [[Sequential Machine]]

## Solved Tasks
- [[Task 2 - Start Stop Motor]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
