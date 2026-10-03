# Instruction Pipelining — Formulas

Symbols: k = stages, N = instructions, t_i = combinational delay of stage i, d = pipeline-register overhead per stage, T_p = pipeline clock, T_np = non-pipelined time per instruction, f = 1/T_p, CPI = cycles per instruction, IC = instruction count.
Units: keep ps / ns / µs / s consistent; GHz = 10^9 Hz; 1 K = 2^10 for memory sizes (not used for clock rates).
Derivations and worked examples: [`NOTES.md`](NOTES.md). Hazard-related stall counting: [`../08-PIPELINE-HAZARDS`](../08-PIPELINE-HAZARDS/).

---

## A. Cycle counts and time

### F1. Total cycles for N instructions
```
cycles = k + N − 1
```
- **Applies:** k-stage linear pipeline, in order, one instruction enters per cycle, no stalls, starts empty.
- **Why:** first instruction needs k cycles; each of the other N − 1 finishes exactly one cycle after its predecessor.
- **Example:** k = 4, N = 10 → 13 cycles.
- **Misuse:** N·k (no overlap), k + N (off by one), forgetting stalls.

### F2. Execution time
```
time = (k + N − 1) × T_p            T_p = max(t_i) + d
```
- **Example:** k = 5, N = 1000, T_p = 200 ps → 1004 × 200 ps = 200.8 ns.
- **Misuse:** using Σt_i or the average as T_p; unit slip (ps → ns ÷ 1000).

### F3. Completion cycle and completed-by-cycle count
```
i-th instruction completes at cycle  k + i − 1
instructions completed within C cycles (C ≥ k−1, started empty, no stalls, enough instructions) = C − k + 1  (0 if C < k)
```
- **Example:** k = 5: the 7th completes at cycle 11; by cycle 30, 26 are complete.
- **Misuse:** answering C (ignores the fill).

### F4. Busy stages in cycle c (stall-free)
```
c            for 1 ≤ c ≤ k       (fill)
k            for k ≤ c ≤ N       (steady)
N + k − c    for N ≤ c ≤ N+k−1   (drain)       (assumes N ≥ k)
```
- **Example:** k = 5, N = 10: cycle 3 → 3 busy; cycle 12 → 3 busy.

### F5. Latency of one instruction
```
latency = k × T_p      (≥ T_np; pipelining never reduces it relative to the non-pipelined unit)
```

### F6. One multi-cycle stage (closed form)
```
cycles = (k + N − 1) + Σ (c_i − 1) = k − 1 + Σ c_i
```
- **Applies:** exactly one stage takes c_i cycles for instruction i; all others 1 cycle; in order; stall-free otherwise; the slow stage is not internally pipelined.
- **Why:** the slow stage is busy back to back; the other k − 1 stage-times appear once as fill/drain.
- **Example:** k = 5, N = 60 with c = 1 (×40), 2 (×15), 4 (×5) → 64 + 15 + 15 = 94 cycles.
- **Misuse:** with ≥ 2 multi-cycle stages; use the recurrence of NOTES §7.2.

### F7. General in-order schedule with per-stage cycle table
```
Blocking :  start[i][s] = max( finish[i][s−1], start[i−1][s+1] )     (previous instruction leaves s when it enters s+1)
Buffered :  start[i][s] = max( finish[i][s−1], finish[i−1][s] )
finish[i][s] = start[i][s] + t[i][s]        total = finish[N][k]
```
- Use when two or more stages are multi-cycle or when a table of cycles is given. State the model; blocking ≥ buffered.

### F8. Taken branch with fetch stalling until resolution (stage-level timing only)
```
cycles = p + r + m + k − 2     (branch = p-th executed instruction, resolved at end of stage r, m instructions executed from the target on)
penalty = r − 1 cycles per taken branch
```
- **Example:** k = 5, p = 3, r = 3, m = 3 → 12 cycles.
- **Misuse:** assuming r without reading the question; wrong-path instructions do not add completed work.

---

## B. Speedup, efficiency, throughput

### F9. Speedup, same clock, non-pipelined = k cycles per instruction (V1)
```
S = N·k / (k + N − 1)       S < k for finite N, S → k
```
- **Example:** k = 6, N = 30 → 180/35 = 5.14.
- **Misuse:** replacing k + N − 1 by k + N (gives 5.0).

### F10. Speedup with different times (V2)
```
S = N·T_np / ((k + N − 1)·T_p)
```
- **Example:** T_np = 36 ns, T_p = 8 ns, k = 5, N = 25 → 900/232 = 3.88.
- **Misuse:** using k in the numerator instead of T_np/T_p.

### F11. Asymptotic (steady-state) speedup (V3)
```
S_∞ = T_np / T_p          = Σ t_i / (max t_i + d)         [overhead only in the pipelined design]
balanced, d = 0 :  S_∞ = k
```
- **Example:** t = 120, 180, 150, 90, 160 ps, d = 20 ps → 700/200 = 3.5.
- **Misuse:** quoting k; adding d to the non-pipelined sum unless told so.

### F12. CPI / frequency speedup (V4)
```
S = (CPI_np / f_np) / (CPI_pipe / f_pipe)        CPI_pipe = 1 + stall cycles per instruction
```
- **Example:** CPI_np = 4.2 at 1.6 GHz; CPI_pipe = 1.3 at 1.25 GHz → 2.625 ns / 1.04 ns = 2.52.
- **Misuse:** adding stalls to CPI_np; forgetting that the two clocks differ.

### F13. Efficiency
```
η = S / k            (V1: η = N / (k + N − 1))
```
- **Why:** busy stage-slots N·k out of k·(k + N − 1) available.

### F14. Required N for a target efficiency / half speed
```
N = f·(k − 1)/(1 − f)    for η = f ;     half of ideal speedup (S = k/2) at N = k − 1
```
- **Example:** k = 5, f = 0.9 → N = 36; N = 4 → S = 2.5.

### F15. Throughput
```
throughput = N / ((k + N − 1)·T_p)  →  1 / T_p   (instructions per unit time)
throughput increase (%) after a redesign = (T_p,old / T_p,new − 1) × 100
```
- **Example:** 700 ps → 500 ps: 40 %.
- **Misuse:** reporting the ratio instead of the percent increase; using 1 − T_new/T_old (that is the time reduction).

### F16. Stage utilisation (steady state)
```
U_i = t_i / T_p     (fraction of the cycle stage i does useful work; the bottleneck stage has U = (T_p − d)/T_p)
```

---

## C. Clock period and stage design

### F17. Pipeline clock and frequency
```
T_p = max(t_1 … t_k) + d         f = 1 / T_p        (1 ns ↔ 1 GHz, 1 ps ↔ 1 THz)
```
- **Misuse:** adding d to every stage and then summing; adding d when delays "already include" it.

### F18. After splitting stage j into stages of delays a and b
```
T_p,new = max( all other t_i , a , b ) + d         f ratio = T_p,old / T_p,new
```
- **Example:** 700, 400, 500, 300 ps; split 700 → 450 + 250: new max 500 (not 450).
- **Misuse:** forgetting that another stage may now limit; ignoring d for the new register.

### F19. Frequency from stage ratios
```
f_new = 1 / ( new longest stage ),   where the old longest stage = 1/f_old and the others scale by their ratio
```
- **Example:** ratios 5 : 8 : 6 : 4 at 2.5 GHz, split the 8 → new longest is the 6-unit stage: 0.30 ns → 3.33 GHz.

### F20. Balanced stages with overhead, depth k
```
T_p = T/k + d          S_∞(k) = k·T / (T + k·d)        ceiling  S_∞ → T/d as k → ∞
k needed for S_∞ ≥ S* :   k ≥ S* / (1 − S*·d/T)      (needs S* < T/d)  → equivalently T/k + d ≤ T/S*
```
- **Example:** T = 90 ns, d = 3 ns: k = 10 → 7.5; k = 15 → 10 (S* = 10: 10/(1 − 1/3) = 15); ceiling 30.
- **Derivation check:** S*·(T/k + d) ≤ T ⇒ T/k ≤ T/S* − d ⇒ k ≥ T / (T/S* − d) = S* / (1 − S*·d/T).

### F21. Simple optimal-depth model (concept)
```
time/instruction = (T/k + d)(1 + p(k − 1))       k* = √( T(1 − p) / (d·p) )
```
- p = fraction of instructions causing a flush of k − 1 cycles. Example: T = 64, d = 1, p = 0.1 → k* = 24, 12.1 ns.
- Not a standard GATE formula; use only when a question states this model.

### F22. Replicated stage
```
effective delay of a stage replicated m times = t / m      (independent consecutive instructions)
```
- **Example:** 4, 10, 5 ns with the 10-ns stage doubled → clock 5 ns; 100 instructions: (4 + 99)·5 = 515 ns.

---

## D. CPI and the iron law

### F23. Iron law
```
CPU time = IC × CPI × T_clk = IC × CPI / f
```

### F24. Multi-cycle (non-pipelined) CPI from a mix
```
CPI_np = Σ_j (fraction_j × cycles_j)          [or Σ count_j × cycles_j over IC]
```
- **Example:** 0.5×4 + 0.3×5 + 0.1×4 + 0.1×3 = 4.2.

### F25. Pipelined CPI
```
CPI_pipe = 1 + Σ_j (fraction of instructions affected_j × stall cycles_j)       (large N)
CPI_pipe (finite N) = (k + N − 1)/N + stalls per instruction
```
- **Example:** 15 % of instructions lose 2 cycles → 1.3. Never below 1 for a scalar pipeline.

### F26. Clock period from mix and total time
```
total cycles = Σ count_j × CPI_j          T_clk = (execution time) / (total cycles)
```
- **Example:** 17.5 × 10^8 cycles in 4.2 s → 2.4 ns.

### F27. Frequency from CPI and time ratios
```
f_2 = f_1 × (CPI_2 / CPI_1) × (T_1 / T_2)       (same IC)
```
- **Example:** f_1 = 1 GHz, CPI_2 = 1.25·CPI_1, T_2 = 0.70·T_1 → f_2 = 1.786 GHz.
- **Misuse:** treating "30 % less time" as ÷1.3 or inverting the CPI ratio.

### F28. Superscalar ideal CPI (concept)
```
w-issue ideal CPI = 1 / w
```

---

## E. Non-linear pipeline (reservation table)

### F29. Forbidden latencies and collision vector
```
forbidden latencies F = { |x − y| : x ≠ y marks in the same row of the reservation table }
collision vector C = (C_{n−1} … C_1),  C_j = 1 iff j ∈ F ;  n = number of columns
state transition on allowed latency p (p < n):  next = (state >> p) OR C ;   p ≥ n → back to the start state C
```

### F30. Minimum average latency
```
average latency of a cycle (p_1 … p_m) = (p_1 + … + p_m) / m          MAL = min over valid cycles
lower bound:  MAL ≥ max number of X's in one row
```
- **Example (NOTES §7.3):** F = {2, 3, 5}, C = 10110, cycles (1,6) → 3.5, (4) → 4, MAL = 3.5 (lower bound 3).

---

## F. Arithmetic pipeline

### F31. Stream of operand pairs through a k-stage arithmetic unit
```
time = (k + N − 1) × T_p            non-pipelined = N × k × T_p (same total delay)
```
- **Example:** k = 4, T_p = 2 ns, N = 100 → 206 ns vs 800 ns.
