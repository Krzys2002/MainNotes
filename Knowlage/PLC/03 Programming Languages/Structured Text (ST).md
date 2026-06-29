---
title: Structured Text (ST)
tags:
  - #structured-text
  - #iec61131
---

# Structured Text (ST)

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Syntax
- Pascal-like statements ending with semicolons.
- Assignment uses :=.
- Control structures include IF, CASE, FOR, WHILE, and REPEAT.
- FB calls use named parameters such as T1(IN := Start, PT := T#5s);

## Strengths
- Best for calculations, scaling, arrays, state machines, and reusable algorithms.
- Compact for exam math tasks.
- Easy to version and review as text.

## Weaknesses
- Less transparent to troubleshoot for simple wiring logic.
- Poor naming makes code opaque quickly.
- Vendor-specific libraries vary.

## Best Use Cases
- Analog scaling
- Formula calculation
- Digital controller equations
- State machines

## Common Mistakes
- Using = instead of := for assignment.
- Updating previous-sample variables too early.
- Calling timers conditionally and losing expected state updates.

## Comparison With Other PLC Languages
ST is denser and more expressive than LD/FBD; SFC remains clearer when the problem is mainly a sequence of steps.

## Related
- [[IEC 61131-3]]
- [[Function Blocks]]
- [[Exam Preparation]]
