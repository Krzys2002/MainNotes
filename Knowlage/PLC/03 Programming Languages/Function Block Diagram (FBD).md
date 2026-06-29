---
title: Function Block Diagram (FBD)
tags:
  - #fbd
  - #iec61131
---

# Function Block Diagram (FBD)

> [!info] Source spine
- [[Books/Programmable Logic Controllers A Practical Approach to IEC 61131-3 using CoDeSys by Dag H. Hanssen.pdf|Hanssen - IEC 61131-3 with CODESYS]]
- [[Books/Programmable Logic Controllers by Frank Petruzella.pdf|Petruzella - PLC textbook]]
- [[Books/S7-1200_Programming_guideline.pdf|Siemens S7-1200 programming guideline]]
- [[Books/s71200_system_manual_en-US_en-US.pdf|Siemens S7-1200 system manual]]
- [[Books/General_Functions_for_Simatic.pdf|Siemens general functions for SIMATIC]]

## Syntax
- Signals connect between boxes representing functions or function blocks.
- Execution order is normally inferred by data flow or network order.
- Boolean, arithmetic, timers, counters, and custom FBs can be wired together.

## Strengths
- Good for signal processing and controller block composition.
- Visual representation matches control block diagrams.
- Useful for PID, filters, scaling, and reusable FB networks.

## Weaknesses
- Complex boolean conditions can become tangled.
- Execution order can be less obvious than ST.
- Large diagrams are hard to diff and review.

## Best Use Cases
- PID block integration
- Analog signal chains
- Function block composition

## Common Mistakes
- Crossed connections without clear labels.
- Using one FB instance for multiple signals.
- Ignoring EN/ENO behavior where available.

## Comparison With Other PLC Languages
FBD is more data-flow oriented than LD and more visual than ST. It pairs well with function blocks.

## Related
- [[IEC 61131-3]]
- [[Function Blocks]]
- [[Exam Preparation]]
