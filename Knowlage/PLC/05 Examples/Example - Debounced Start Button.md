---
title: Example - Debounced Start Button
tags:
  - #example
  - #timer
---

# Example - Debounced Start Button

> [!info] Source spine
- [[Presentations/02_PLC_lecture_2025_4pp-2.pdf|Lecture 02 - Counters and literals]]
- [[Presentations/03_PLC_lecture_2023.pdf|Lecture 03 - Structuring tasks and interrupts]]
- [[Presentations/04_PLC_lecture_2025.pdf|Lecture 04 - LD programming issues]]
- [[Presentations/05_PLC_lecture_2025_ST_6pp.pdf|Lecture 05 - Structured Text]]
- [[Presentations/07_PLC_lecture_2025_hardware_6pp.pdf|Lecture 07 - Hardware]]
- [[Presentations/08_PLC_lecture_2025_SFC_6pp.pdf|Lecture 08 - SFC]]
- [[Presentations/09_PLC_lecture_2025_discret_6pp.pdf|Lecture 09 - Discrete control]]
- [[Presentations/PLC_lecture_2025_communication_ASi_IOLink.pdf|Communication - S7-1200, AS-i, IO-Link]]

## Problem Statement
Accept Start only after it has been stable for 30 ms.

## Solution
Use TON for debounce, then R_TRIG for a clean pulse.

## Explanation
- The timer filters short bounce.
- The edge detector makes one command pulse.
- Hardware input filters may already provide this.

## Ladder Implementation
```text
StartRaw -> TON Debounce 30ms -> R_TRIG StartEdge
```

## Structured Text Implementation
```iecst
Debounce(IN := StartRaw, PT := T#30ms);
StartEdge(CLK := Debounce.Q);
StartPulse := StartEdge.Q;
```

## Alternative Implementations
- Use vendor-provided function blocks where they reduce risk.
- Use SFC or an explicit state machine when the example grows into a sequence.

## Full Working Code

### Mermaid Diagram
```mermaid
flowchart LR
    Raw["Raw button"] --> TON["TON 30 ms"]
    TON --> Edge["R_TRIG"]
    Edge --> Pulse["StartPulse"]
```

### Assumptions And I/O
- The raw pushbutton may bounce.
- The signal must be stable TRUE for 30 ms.
- The final output is one scan wide.

### Variable Declaration
```iecst
PROGRAM DebouncedStartButton
VAR_INPUT
    StartRaw : BOOL;
END_VAR
VAR_OUTPUT
    StartStable : BOOL;
    StartPulse  : BOOL;
END_VAR
VAR
    Debounce  : TON;
    StartEdge : R_TRIG;
END_VAR
```

### Structured Text Program
```iecst
(* Input section *)
Debounce(IN := StartRaw, PT := T#30ms);
StartStable := Debounce.Q;

(* Work section *)
StartEdge(CLK := StartStable);

(* Output section *)
StartPulse := StartEdge.Q;
```

### Test Checklist
- Short bounce pulses under 30 ms do not create StartPulse.
- Holding StartRaw TRUE produces only one StartPulse.
- StartStable remains TRUE while the button is stably pressed.

## Related Concepts
- [[Debouncing Inputs]]
- [[TON]]
- [[R_TRIG]]
