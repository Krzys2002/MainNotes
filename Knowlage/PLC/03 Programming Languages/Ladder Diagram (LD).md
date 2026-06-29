---
title: Ladder Diagram (LD)
tags:
  - #ladder
  - #iec61131
---

# Ladder Diagram (LD)

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Syntax
- Rungs flow left to right from power rail to coil.
- Contacts examine boolean values; coils assign boolean outputs.
- Function blocks such as TON and CTU appear as boxes inside networks.

## Strengths
- Excellent for relay-style boolean logic.
- Easy for electricians to inspect online.
- Good for interlocks, permissives, and start/stop circuits.

## Weaknesses
- Awkward for complex math and arrays.
- Large sequences become hard to follow without structure.
- Multiple coils for one output can create last-write-wins bugs.

## Best Use Cases
- Motor interlocks
- Safety permissives
- Simple timer/counter logic

## Common Mistakes
- Duplicating output coils in different rungs.
- Using seal-in logic without stop priority.
- Forgetting that NC contact in logic means NOT of the variable.

## Comparison With Other PLC Languages
LD is more visual than ST and less block-oriented than FBD. Use SFC or a state machine for long sequences.

## Related
- [[IEC 61131-3]]
- [[Function Blocks]]
- [[Exam Preparation]]
