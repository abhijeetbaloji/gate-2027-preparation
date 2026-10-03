# Sequential Circuits — Previous Year Questions

Question text stays in the mapping file. This page follows the `Paper` line. Stored answers are `VERIFICATION REQUIRED`. Diagrams are not redrawn here.

Mapping file: `../../../13-PYQ-TOPIC-MAPPING/02-DIGITAL-LOGIC/02-DESIGN-OF-COMBINATIONAL-AND-SEQUENTIAL-CIRCUITS/02-SEQUENTIAL-CIRCUITS/questions.md`

Papers: `../../../12-PYQ/`.

## Recognizable sequential stems

| Paper | Question | Type | Pattern |
|-------|----------|------|---------|
| GATE 2026 CS-1 | Q.37 | MCQ | 2-bit saturating up/down counter; next-state behaviour |
| GATE 2025 CS-1 | Q.60 | NAT | D flip-flop circuit; number of distinct states reached |
| GATE 2025 CS-2 | Q.34 | NAT | 4-bit ripple counter; period at the last flip-flop versus frequency |
| GATE 2023 CS | Q.21 | MCQ | Mux output fed back; which sequential element that matches |
| GATE 2023 CS | Q.43 | MCQ | T and D flip-flops; state after a stated run from a given start |
| GATE 2021 CS Set-1 | Q.28 | MCQ | 3-bit T counter; sequence from \(PQR=000\) |
| GATE 2021 CS Set-2 | Q.28 | MCQ | Synchronous circuit that rewrites a bit string; FSM behaviour |
| GATE 2018 CS | Q.22 | NAT | Two positive-edge D flip-flops; number of states |
| GATE 2017 CS Session 2 | Q.42 | MCQ | 2-bit saturating up counter built with T flip-flops; expressions for \(T\) |
| GATE 2016 CS-1 | Q.8 | NAT | Minimum JK flip-flops for the repeating sequence \(0,1,0,2,0,3\) |
| GATE 2015 CS, 7 February Shift 1 | Q.21 | MCQ | 4-bit Johnson counter from 0000; which sequence |
| GATE 2015 CS, 7 February Shift 1 | Q.53 | MCQ | D flip-flop output tied to both J and K; trace |
| GATE 2015 CS, 7 February Shift 2 | Q.17 | NAT | Minimum JK flip-flops for \((0,0,1,1,2,2,3,3)\) |
| GATE 2014 CS SET-2 | Q.7 | MCQ | \(n\)-bit counter into an \(n\)-to-\(2^n\) decoder; what the pair equals |
| GATE 2014 CS SET-3 | Q.45 | MCQ | Synchronous JK circuit from 0000; state over the following clocks |
| GATE 2011 CS | Q.51 | MCQ | Counter reset to 0; how many distinct \(PQR\) values appear |
| GATE 2009 CS | Q.27 | MCQ | Two-state FSM table; output trace from a given start |
| GATE 2007 CS | Q.36 | MCQ | Counter with clear, load, and count; behaviour of a stated wiring |

## Combinational questions stored in this file

| Paper | Question | Why it is listed here in the mapping | Where it belongs |
|-------|----------|--------------------------------------|------------------|
| GATE 2014 CS SET-3 | Q.8 | `if (x) y=a; else y=b` | Combinational: a 2-to-1 mux |
| GATE 2007 CS | Q.34 | One mux and one inverter for any function of \(n\) variables | Combinational: mux size \(2^{n-1}\)-to-1 |

## Rows that are not sequential design

The file also contains pipeline speedup, interrupts, cache hit time, hashing, semaphores, a C recursive counter, threads, the secant method, a stack in a processor, a software life-cycle matching question, and a TCP initial-sequence-number clock. Those stems are not flip-flop or FSM questions. They are not used as frequency evidence for this topic.

Examples: GATE 2026 CS-1 Q.60 and GATE 2026 CS-2 Q.57 (pipeline), GATE 2025 CS-1 Q.11 (interrupt), GATE 2025 CS-2 Q.55 (cache), GATE 2023 CS Q.20 (hashing) and Q.22 (threads), GATE 2021 CS Set-1 Q.46 (semaphore), GATE 2018 CS Q.21 (C recursion), GATE 2017 CS Session 2 Q.7 (threads), GATE 2015 Shift 2 Q.51 (secant) and Q.54 (stack), GATE 2010 CS Q.22 (software life cycle), GATE 2009 CS Q.47 (TCP).

## Gap

No recognizable flip-flop stem is stored for 2024, 2022, 2020, 2019, 2013, 2012, 2010, or 2008. That is a statement about this file.
