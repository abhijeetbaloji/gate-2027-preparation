# Instruction Pipelining — Mistakes to Avoid

Theory: [`NOTES.md`](NOTES.md). Hazard-specific mistakes (forwarding, stall counting, register-file timing): [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/).
This file lists *typical* errors; nothing here is a record of anyone's personal mistakes (see the empty table at the end).

## 1. Conceptual confusions

| Confusion | Reality |
|---|---|
| Pipelining makes one instruction finish faster | Latency never drops versus the non-pipelined unit; throughput rises. |
| Number of stages = speedup | Only for balanced stages, zero overhead, N → ∞. |
| More stages is always better | Register overhead caps S_∞ at T/d; hazards penalise depth; the clock is set by the slowest stage. |
| The clock is the average (or sum) of the stage delays | Clock = max stage + register overhead. |
| Speeding up any stage speeds up the pipeline | Only the slowest stage matters; ties need all tied stages improved. |
| Pipeline registers are only "storage" | They also bound the minimum cycle by setup + clock-to-Q and carry the control bits and destination register number. |
| Instructions that skip a stage finish early | In a fixed-length pipeline every instruction passes every stage; unused stages are idle slots (that is why ideal CPI = 1). |
| Superscalar and pipelined are the same | Superscalar issues several per cycle (CPI < 1); a scalar pipeline has CPI ≥ 1. |
| Instruction pipeline = arithmetic pipeline | Same timing formula, different purpose (different instructions vs operand stream through one unit). |

## 2. Formula mistakes

- Using N·k·T_p (no overlap) or (k + N)·T_p, or (N − 1)·T_p.
- Using the V1 speedup Nk/(k + N − 1) when different times are given (V2 needed).
- Adding register overhead to the non-pipelined time (variant B says no) or forgetting it on the pipelined clock.
- Computing S_∞ as k when the stages are unbalanced.
- Efficiency η = S/k mistaken for utilisation of the bottleneck stage.
- Percent increase = new/old instead of (new/old − 1) × 100; throughput increase confused with time reduction (1 − new/old).
- After splitting: not adding d for the new register; using the half of the old maximum as the new clock without checking the other stages.
- CPI_pipe = 1 + stalls but stalls added to CPI_np.
- CPU time = IC × clock / CPI (inverted).
- Clock period of a mix program = time / instruction count (should divide by total cycles).
- One-multi-cycle-stage formula applied with two multi-cycle stages.
- Efficiency/speedup for finite N assumed equal to the asymptote.

## 3. Numerical / calculation mistakes

- **Off-by-one:** k + N − 1; a single instruction takes exactly k cycles; "completed by cycle C" = C − k + 1.
- ps ↔ ns ↔ µs ↔ s (a factor of 1000 is easy to lose); "time in microseconds" asked for a nanosecond calculation.
- GHz ↔ ns: 1 GHz = 1 ns; 2.5 GHz = 0.4 ns; MHz ↔ µs.
- 10^8-scale counts: keep exponents; the mix total must equal the stated instruction count.
- Decimal GHz/ns vs binary K/M (not interchangeable; clock rates are decimal).
- Rounding intermediate values too early (carry fractions: e.g. 4/1.3, 7/6).
- Ceil/floor: smallest integer k meeting a target → round **up**, then verify k and k − 1.
- Percent-of-instructions × stall cycles: 20 % × 3 = 0.6 cycles per instruction, not 6.
- In Gantt tables, forgetting that a blocked instruction still occupies its stage.
- Mis-reading the cycles table (rows = instructions, columns = stages) when rebuilding a schedule.
- Reservation table: only adjacent X's considered; forgetting the OR with the original collision vector after a shift.

## 4. PYQ-derived traps (pattern, with entries that exist in the mapping; newest → oldest)

| Trap pattern | Kind of question | Entry |
|---|---|---|
| Powers of ten and per-class CPI × count, clock period asked | instruction mix → clock | 2025 Q.61 (CS-2) |
| Dependence direction: first access then second access defines RAW/WAR/WAW | dependence labelling | 2024 Q.31 (CS2) |
| Next-slowest stage becomes the limit after a split; "% throughput increase" wording | split a stage | 2016 Q.32 (CS-1) |
| Stage latencies as ratio equalities; ignoring register delay as stated | split a stage → frequency | 2016 Q.33 (CS-2) |
| Reservation table: non-adjacent forbidden latencies, average over the cycle | non-linear pipeline | 2015 Q.48 (table missing in mapping) |
| Percent algebra for CPI and time; same instruction count | processor comparison | 2014 Q.55 (Set-1) |
| Deepest pipeline ≠ highest frequency | peak frequency | 2014 Q.9 (Set-3) |
| Buffer delay per stage, branch skipping instructions, which stage resolves the branch | taken branch, total time | 2013 (Booklets A–D, same question) |
| Register delay: in the pipeline clock but not in the non-pipelined sum | steady-state speedup | 2011 Q.41 |
| Blocking/overlap in a cycle table, repeated loop iterations | cycle count from table | 2009 Q.28 (table incomplete in mapping) |
| Delay slot must be an instruction independent of the branch condition | delay slot | 2008 Q.77 |
| Treating a "which operation must precede which" question as arithmetic | TLB position | 2008 Q.38 |

Similar traps appear in the sibling mapping's ideal-model questions (latch delay added once per cycle, variable-cycle PO/EX stage, stall-fraction speedup with different clocks); see [`PYQ.md`](PYQ.md) §5.

## 5. Examination-time mistakes

- Starting arithmetic before stating the assumption on the non-pipelined time and register overhead.
- Not drawing a small Gantt for cycle-table or branch questions (invisible blocking).
- Reading "one instruction per cycle" as "one cycle per instruction for the whole instruction".
- Rounding to the wrong number of decimals (NAT) or giving the ratio instead of the percent.
- Leaving a unit conversion to the end and then forgetting it.
- Assuming forwarding or half-cycle register-file behaviour in a hazard-free question (not needed here; belongs to the sibling).
- Skipping the sanity checks S ≤ k, CPI ≥ 1.

## 6. How to check yourself

1. Did I identify the slowest stage after any redesign?
2. Did I add the register overhead exactly once per cycle and not to the non-pipelined sum (unless told)?
3. Is the cycle count k + N − 1 (plus stalls), and does N = 1 give k?
4. Do my units agree (ns vs ps vs µs; GHz vs ns)?
5. Is S ≤ k, CPI_pipe ≥ 1, latency ≥ T_np?
6. Did I use the right speedup variant (same clock / different time / CPI-f / steady state)?
7. If a stage is multi-cycle: is it only one stage (closed form) or should I draw a table?
8. Are the stall cycles per instruction computed as fraction × cycles?

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
