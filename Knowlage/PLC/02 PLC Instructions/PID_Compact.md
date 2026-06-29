---
title: PID_Compact
tags:
  - #instruction
  - #pid
---

# PID_Compact

> [!info] Source spine
- [[Presentations/06_PLC_lecture_2025_PID_1_6pp.pdf|PID 1 - Introduction]]
- [[Presentations/10_PLC_lecture_2025_PID_2.pdf|PID 2 - Tuning and response]]
- [[Presentations/11_PLC_lecture_2025_PID_3.pdf|PID 3 - Saturation and windup]]
- [[Presentations/12_PLC_lecture_2025_PID_in_PLC.pdf|PID in PLC]]
- [[Presentations/Brock_PID_control_4pp.pdf|PID control reference slides]]

## Purpose
Siemens technology object/block for PID control in S7-1200/S7-1500 style projects.

## Syntax
```iecst
PID_Compact(Setpoint, Input, ManualEnable, ManualValue, Output, ...)
```

## Parameters
| Parameter | Type | Meaning |
| --- | --- | --- |
| `Setpoint` | `REAL` | Desired process value. |
| `Input` | `REAL` | Measured process value. |
| `Output` | `REAL` | Controller output. |
| `Mode/Manual` | `BOOL/Enum` | Operating mode and manual handling. |

## Execution Behavior
- Executes PID algorithm with configured sample time and tuning parameters.
- Includes limits, tuning support, and status diagnostics.
- Should be called at a stable period.

## Timing Diagram
```text
SP/PV --> PID_Compact --> actuator command
```

## Common Mistakes
- Wrong sampling time.
- No output limits.
- No manual/auto transfer plan.
- Ignoring block status/error outputs.

## Ladder Example
```text
[ PID_Compact ]  SP, PV, limits, mode -> LMN
```

## Structured Text Example
```iecst
PID_Compact_1(Setpoint := SP, Input := PV, ManualEnable := ManualMode, ManualValue := ManualOut);
```

## Applications
- [[PID Control in PLC]]
- [[Temperature Measurement]]

## Solved Tasks
- [[Task 10 - PI Controller With Weighting]]
- [[Task 15 - HMI Drive Control]]

## Related
- [[PLC Instructions]]
- [[IEC 61131-3]]
