---
title: Sequential Function Chart (SFC)
tags:
  - #sfc
  - #iec61131
  - #exam
---

# Sequential Function Chart (SFC)

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Syntax
- Steps hold active state.
- Transitions define conditions between steps.
- Actions execute while their step is active.
- Branches express alternatives or parallel sequences.

## Strengths
- Best for sequential machines.
- Makes parallel process coordination explicit.
- Easy to discuss with state diagrams and process descriptions.

## Weaknesses
- Not ideal for dense arithmetic.
- Requires clear reset/fault behavior.
- Vendor support and action qualifiers differ.

## Best Use Cases
- Batch processes
- Tank filling
- Two concurrent processes
- Traffic lights

## Common Mistakes
- No initial step.
- No transition priority for alternatives.
- No timeout/fault transition from waiting states.

## Comparison With Other PLC Languages
SFC structures the high-level sequence; LD, ST, or FBD often implement each action or transition condition.

## Related
- [[IEC 61131-3]]
- [[Function Blocks]]
- [[Exam Preparation]]
