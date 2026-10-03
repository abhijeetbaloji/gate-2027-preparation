# Instruction Pipelining — Last-Minute Revision

Full theory [`NOTES.md`](NOTES.md) · hazards/stall counting: [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/).

## Definitions
- **Pipeline:** k stages separated by registers; up to k instructions in flight; one enters/leaves per cycle in steady state.
- **Latency** of one instruction = k·T_p (never below the non-pipelined time). **Throughput** = 1/T_p (steady state).
- **Clock:** T_p = max(stage delay) + register overhead d; f = 1/T_p.
- **Stages (classic):** IF, ID/RF, EX, MEM, WB. Pipeline registers (IF/ID, ID/EX, EX/MEM, MEM/WB) carry instruction, operands/ALU result, destination register number and control bits.
- **Ideal CPI = 1.** CPI_pipe = 1 + stall cycles per instruction.

## Must-remember formulas
```
cycles  = k + N − 1                       time = (k + N − 1)·T_p
i-th instruction completes at cycle k+i−1;  completed in C cycles = C − k + 1
Speedup (same clock, non-pipe = k cycles)  : S = N·k / (k + N − 1)    → k
Speedup (general)                           : S = N·T_np / ((k+N−1)·T_p)
Asymptotic (steady state)                   : S_∞ = T_np / T_p = Σt_i / (max t_i + d)   (non-pipe has no registers)
Efficiency η = S/k  (V1: N/(k+N−1));  half of ideal speedup at N = k − 1
CPI form : S = (CPI_np/f_np) / (CPI_pipe/f_pipe);   CPU time = IC·CPI/f
One multi-cycle stage : cycles = (k+N−1) + Σ(c_i − 1)
Taken branch, no prediction, resolved in stage r : cycles = p + r + m + k − 2
Balanced k stages with overhead : S_∞ = kT/(T + kd) → ceiling T/d ;   min k for S* : k ≥ S*/(1 − S*d/T)
MAL ≥ max X's in a row;  forbidden latencies = differences of X's in the same row
```

## Gantt picture
```
cycle :   1   2   3   4   5   6   7   8
I1    :  IF  ID  EX  ME  WB                   k = 5, N = 4 → 8 cycles = 5 + 4 − 1
I2    :      IF  ID  EX  ME  WB
I3    :          IF  ID  EX  ME  WB
I4    :              IF  ID  EX  ME  WB
```

## Non-pipelined time — state the assumption
| Variant | T_np | T_p |
|---|---|---|
| zero overhead | Σ t_i | max t_i |
| overhead only in pipeline (standard) | Σ t_i | max t_i + d |
| same clock, k cycles | k cycles | 1 cycle |
| given directly / CPI & f | as stated | from stages / f |

## Fast-solve checklist
1. Write k, N, stage delays, d, stalls, mix. 2. T_p = max + d (do not add d twice). 3. Cycles = k + N − 1 (+ stalls). 4. Convert units last. 5. Speedup = non-pipelined time / pipelined time (steady state: per-instruction ratio). 6. Sanity: S ≤ k, CPI ≥ 1, latency ≥ T_np. 7. Redesign (split/replicate) → recompute the max over the **new** stage list.

## Top traps
- N·k·T instead of (k + N − 1)·T; off by one.
- "Speedup = k" for unbalanced stages or finite N.
- Using Σ delays or the average as the clock.
- Forgetting the new stage's register overhead after a split; the next-slowest stage may now limit.
- Adding stalls to the non-pipelined CPI; ignoring different clocks.
- Throughput increase % = ratio − 1 (not 1 − ratio).
- Two multi-cycle stages: do not use the one-stage closed form.
- ps/ns/µs and 10^8 slips.

## Frequently tested concepts (from the mapped PYQs and the sibling mapping)
Highest frequency from stage delays; split the slowest stage (throughput %, frequency); steady-state speedup with register delay; total time for N instructions with latch/buffer delay (incl. a taken branch); variable-cycle stage cycle counts; CPI/time/frequency algebra; mix → clock period; reservation-table MAL (one mapped entry).
