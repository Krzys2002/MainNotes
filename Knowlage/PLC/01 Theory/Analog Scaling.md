---
title: Analog Scaling
tags:
  - #theory
  - #application
  - #exam
---

# Analog Scaling

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Definition
Convert a raw analog input count into engineering units such as volts, percent, degrees, or pressure.

## Purpose
- Convert a raw analog input count into engineering units such as volts, percent, degrees, or pressure.

## When To Use
Use whenever comparisons depend on a physical signal instead of a raw ADC number.

## Important Properties
- Scaling is usually linear: engineering = low + normalized * span.
- A unipolar 0 to 10 V signal can map to 0.0 to 10.0 V or 0 to 100 percent.
- Apply limits before outputs if sensor faults can produce out-of-range values.
- Use hysteresis when thresholds switch physical outputs.

## Limitations
- Scaling does not filter noise.
- Thresholds near noisy signals can chatter without hysteresis or filtering.

## Common Mistakes
- Comparing raw counts to engineering thresholds.
- Using integer arithmetic where REAL is required.
- Forgetting the analog module's configured range.

## Related Concepts
- [[COMPARE]]
- [[LIMIT]]
- [[NORM_X]]
- [[SCALE_X]]
- [[Hysteresis]]

## Practical Applications
- [[Analog Threshold Classification]]
- [[Tank Filling]]
- [[Temperature Measurement]]
