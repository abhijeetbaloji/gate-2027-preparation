# Instruction Pipelining — Shortcuts

Only shortcuts that are mathematically valid under the stated conditions. Full theory: [`NOTES.md`](NOTES.md); formulas: [`FORMULAS.md`](FORMULAS.md).

---

## S1. Cycle count = N + (k − 1)
- **What it solves:** total cycles for N instructions, k stages, no stalls.
- **When to use:** whenever the pipe starts empty, one instruction per cycle.
- **Why it works:** one instruction leaves per cycle after the first leaves at cycle k; so "N cycles + the k − 1 cycles of fill".
- **Example:** k = 6, N = 100 → 105 cycles; at a 2 ns clock → 210 ns.
- **Limitation:** each stall cycle adds exactly one more cycle only if it stalls the whole front of the pipe; multi-cycle stage or taken-branch bubbles are added on top (S6, S9).

## S2. Sanity bound: speedup ≤ k, CPI ≥ 1
- **What it solves:** instant detection of arithmetic slips.
- **When to use:** same technology, balanced or unbalanced stages, scalar pipeline.
- **Why it works:** the pipeline overlaps at most k instructions; unbalanced stages or register overhead only lower the speedup.
- **Example:** an answer "speedup 6.2" for a 5-stage pipeline is wrong, whatever the working.
- **Limitation:** when the pipelined clock is *faster* than the non-pipelined clock (pipeline built on a better technology) or the baseline is not "k cycles", speedup can exceed k; V4 questions with different frequencies can break it.

## S3. Asymptotic speedup = (sum of stage delays) ÷ (max stage + overhead)
- **What it solves:** "steady state", "very large N", "ideal conditions" speedup.
- **When to use:** non-pipelined time = Σ t_i with no registers (variant B), or d = 0.
- **Why it works:** per-instruction time falls from Σ t_i to T_p once the pipe is full.
- **Example:** stages 90, 130, 110, 70 ps, d = 10 ps → 400/140 = 2.86.
- **Limitation:** if the question defines the non-pipelined time differently (variant C/E), use that definition.

## S4. Throughput change = ratio of clock periods
- **What it solves:** "% increase in throughput" after a redesign; frequency changes.
- **When to use:** zero stalls, same k+N−1 behaviour, large N.
- **Why it works:** throughput = 1 / T_p.
- **Example:** clock 600 ps → 450 ps: 600/450 − 1 = 33.3 % increase (not 25 %, which would be 1 − 450/600).
- **Limitation:** for finite N the fill adds a small effect; "throughput" in a steady-state sense ignores it. Never mix "% time saved" with "% throughput gained".

## S5. Instructions completed in C cycles = C − k + 1
- **What it solves:** how many instructions have retired (left WB) after C cycles; the cycle the i-th finishes (k + i − 1).
- **When to use:** stall-free, empty start, plenty of instructions.
- **Why it works:** the first retires at cycle k, then one per cycle.
- **Example:** k = 6, T = 0.8 ns, 1 µs → 1250 cycles → 1245 completed.
- **Limitation:** stalls or N < C − k + 1 break it; the answer is capped at N.

## S6. One slow stage: add Σ(c_i − 1) to k + N − 1
- **What it solves:** total cycles when exactly one stage (e.g. EX) takes more than one cycle for some instructions and nothing else stalls.
- **When to use:** one multi-cycle stage, in order.
- **Why it works:** that stage is back-to-back busy; every extra cycle there delays the whole stream by one.
- **Example:** k = 6, N = 80, EX = 1 (×50), 2 (×20), 5 (×10): 85 + 20 + 40 = 145.
- **Limitation:** invalid for two multi-cycle stages or data-dependent stalls — use the table method (NOTES §7.2).

## S7. Only the longest stage matters when splitting; check ties
- **What it solves:** new clock/frequency after splitting or speeding up a stage.
- **When to use:** any redesign question.
- **Why it works:** T_p = max + d. If two stages tie for the maximum, improving one of them leaves the clock unchanged.
- **Example:** stages 5, 8, 8, 4 ns: splitting one 8 into 4 + 4 leaves the clock at 8 ns; splitting both gives 5.
- **Limitation:** remember every new stage pays d; the second-largest stage becomes the new limit as soon as the first is below it.

## S8. Speedup from CPI and frequency in one line
- **What it solves:** pipelined versus multi-cycle comparisons.
- **When to use:** same IC.
- **Why it works:** time per instruction = CPI/f.
- **Example:** CPI_np = 4.05 at 2 GHz; CPI_pipe = 1.3 at 1.6 GHz → (4.05/2)/(1.3/1.6) = 2.49.
- **Limitation:** stalls belong only to CPI_pipe; if N is small, use (k + N − 1)/N instead of 1.

## S9. Stall-fraction speedup for a balanced, overhead-free, same-clock pipeline: S = k / (1 + stalls per instruction)
- **What it solves:** "x % of instructions suffer y stall cycles" with balanced stages and no register overhead.
- **When to use:** non-pipelined time = k × T_p (V1 world) and N large.
- **Why it works:** T_np/T_p = k and CPI_pipe = 1 + s.
- **Example:** k = 8, 10 % of instructions lose 3 cycles → s = 0.3 → 8/1.3 = 6.15.
- **Limitation:** invalid with unbalanced stages, register overhead, different clocks or different non-pipelined CPI — use F12 instead.

## S10. Minimum depth for a target asymptotic speedup: k ≥ S*/(1 − S*·d/T)
- **What it solves:** "smallest number of equal stages for speedup ≥ S*" with register overhead d.
- **When to use:** T = total combinational delay, equal splitting.
- **Why it works:** requires T/k + d ≤ T/S*. If S*·d ≥ T it is impossible (ceiling T/d).
- **Example:** T = 90, d = 3, S* = 10 → 10/(1 − 1/3) = 15 stages; k = 14 gives 9.55 (below 10).
- **Limitation:** round k **up**; verify by plugging k and k − 1.

## S11. Half the ideal speedup arrives at N = k − 1
- **What it solves:** quick estimates of how large N must be.
- **When to use:** V1; balanced stages.
- **Why it works:** N k/(k + N − 1) = k/2 ⇔ N = k − 1. For 90 % of ideal, N = 9(k − 1).
- **Example:** k = 8: N = 7 → S = 4; N = 63 → S = 7.2.
- **Limitation:** V1 only.

## S12. Frequency ranking: smallest maximum stage wins
- **What it solves:** "which design has the highest peak frequency".
- **When to use:** same overhead for all (or d = 0).
- **Why it works:** f = 1/(max + d).
- **Example:** designs with maxima 1.6, 1.4, 0.9, 0.95 ns → third is fastest even though the fourth is deeper.
- **Limitation:** different overheads per design must be added before comparing.

## S13. Unit conversions that avoid slips
- 1 ns ↔ 1 GHz (f in GHz = 1 / T in ns); 500 ps = 2 GHz; 2.5 GHz = 0.4 ns; 1 µs = 1000 ns.
- Keep 10^8 factors symbolic until the end (counts of 10^8 instructions × cycles → 10^8 × cycles).
- **Limitation:** MHz ↔ µs similarly (1 MHz = 1 µs).

## S14. Percent-change algebra for processor comparisons
- "x % less time" → T_2 = (1 − x) T_1 ; "y % higher CPI" → CPI_2 = (1 + y) CPI_1.
- Then f_2 = f_1 (1 + y)/(1 − x) for the same IC.
- **Example:** 30 % less time, 25 % more CPI, f_1 = 1 GHz → f_2 = 1.25/0.70 = 1.786 GHz.
- **Limitation:** different instruction counts change the formula (include IC).

---

## Do NOT use

1. **"Speedup = number of stages."** Counterexample: stages 2, 2, 2, 6 ns → asymptotic speedup 12/6 = 2, not 4.
2. **"Time = N × slowest stage."** Counterexample: k = 5, N = 3, T = 2 ns → (5 + 3 − 1)·2 = 14 ns, not 6 ns.
3. **"Clock = average stage delay"** or "= sum / k". The slowest stage sets the clock; the average ignores it.
4. **"Pipelining reduces the time to execute one instruction."** It never does, versus the non-pipelined unit.
5. **"After splitting the longest stage the clock becomes the half."** Counterexample: stages 700, 400, 500, 300; split 700 → 450 + 250: the clock is 500 (the old third stage), not 450.
6. **"S = Nk/(N + k)"** (off by one). Counterexample N = 1: it gives 0.5 instead of 1.
7. **"Add the register overhead to the non-pipelined time too"** unless the question says the non-pipelined machine has registers.
8. **"S = k/(1 + stalls)" in general.** It fails the moment stages are unbalanced or clocks differ (S9 conditions).
9. **"Divide time by CPI"** — CPU time = IC × CPI × clock period, not IC × clock / CPI.
10. **"Add every extra cycle of every stage to k + N − 1."** That is only valid when a single stage is slow. Counterexample: the 4×4 table of NOTES Example 8 has extra cycles 1 + 2 + 1 + 2 = 6, so the naive total is 7 + 6 = 13, but the true totals are 12 (blocking) and 11 (buffered), because the slow stages overlap with each other's waiting.
