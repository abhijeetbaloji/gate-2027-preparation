# Pipeline Hazards — Shortcuts

Only shortcuts that are mathematically valid under the stated conditions. Full theory: [`NOTES.md`](NOTES.md); formulas: [`FORMULAS.md`](FORMULAS.md).

---

## S1. Total cycles = N + 4 + stalls (5-stage, no multi-cycle EX)
- **What it solves:** cycle count for a short program on the classic pipe.
- **When to use:** k = 5, one cycle per stage, first IF in cycle 1.
- **Why it works:** stall-free base is `5 + N − 1 = N + 4`; each bubble adds one cycle.
- **Example:** 8 instructions, 2 load-use stalls → `8 + 4 + 2 = 14`.
- **Limitation:** multi-cycle EX, unified memory, or control penalties need the ready-time method (S4) or simulation.

## S2. Single RAW stall: `max(0, H − d − U)`
- **What it solves:** stalls for one producer–consumer pair when nothing else is stalling.
- **When to use:** isolated dependence; state H (value ready) and U (operand used) from FORMULAS B1.
- **Why it works:** consumer would use the value at cycle `t + d + U`; it must wait until cycle `t + H`.
- **Example:** load → ALU, `d = 1`, forwarding: `H = 4`, `U = 2` → `max(0, 4 − 1 − 2) = 1`.
- **Limitation:** chains — earlier stalls shift distances; never sum isolated stalls (S4).

## S3. Distance table (memorise the `d = 1` column)
- **What it solves:** instant stall count for adjacent instructions.
- **When to use:** RF-A, classic 5-stage, full forwarding unless noted.

| Producer → consumer | No fwd RF-A | No fwd RF-B | Fwd |
|---|---:|---:|---:|
| ALU → ALU (EX) | 2 | 3 | 0 |
| LOAD → ALU (EX) | 2 | 3 | **1** |
| ALU → branch in ID | 2 | 3 | 1 |
| LOAD → branch in ID | 3 | 4 | 2 |

- **Limitation:** store *data* from load → 0 with forwarding; store *address* from load → 1.

## S4. Ready-time recurrence (sequences)
- **What it solves:** total cycles when several dependences interact.
- **When to use:** any program with more than one RAW or mixed load/ALU chain.
- **Why it works:** `X_i = max(X_{i−1}+1, gate over sources)`; total = `X_N + 2` (WB two cycles after EX).
- **Example:** `ADD; SUB R4,R1; AND R6,R1,R4; OR(indep)` no fwd RF-A → X = 3, 6, 9, 10 → **12 cycles**.
- **Limitation:** add branch/control waits and structural dead-fetch slots separately.

## S5. Load-use rule (one line)
- **What it solves:** the most common data stall with forwarding.
- **When to use:** load immediately followed by a user of the loaded register in EX.
- **Why it works:** value exists only at end of MEM; next instruction needs it at start of EX in the same cycle.
- **Example:** `LW R1,…; ADD R3,R1,R4` → 1 stall; insert one independent instruction → 0.
- **Limitation:** does not apply to store *data* (MEM→MEM forwarding works).

## S6. Branch penalty = r − 1 (not r)
- **What it solves:** flush count / control stall for one branch.
- **When to use:** branch resolved at end of stage `r` (IF=1, ID=2, EX=3, MEM=4).
- **Why it works:** `r − 1` instructions are already fetched behind the branch.
- **Example:** resolved in EX → penalty **2**; in ID → **1**.
- **Limitation:** predict-not-taken pays this only when taken; stall-always pays on every branch.

## S7. CPI from stall fractions: `1 + Σ f_i s_i`
- **What it solves:** effective CPI with mixed hazard types.
- **When to use:** ideal CPI 1; `f_i` = fraction of **all** instructions with event i.
- **Why it works:** average stall cycles per instruction add to ideal CPI.
- **Example:** 25 % loads, 40 % of loads stall 1 cycle → `1 + 0.25×0.40×1 = 1.10`.
- **Limitation:** multiply load fraction × immediate-use fraction; do not apply miss penalty to every instruction.

## S8. Speedup with different clocks: `(CPI_np/τ_np) / (CPI_pipe/τ_pipe)`
- **What it solves:** pipelined vs non-pipelined when frequency changes.
- **When to use:** any "speedup" comparing two machines on the same program.
- **Why it works:** time = IC × CPI / f; IC cancels in the ratio.
- **Example:** CPI 5 @ 2 GHz vs CPI 1.34 @ 1.6 GHz → `(5/2)/(1.34/1.6) = 2.985`.
- **Limitation:** finite N — use cycle counts, not asymptotic CPI.

## S9. Predict-not-taken CPI: `1 + f_b × p_t × P`
- **What it solves:** average control stalls with static prediction.
- **When to use:** `f_b` = branch fraction of all instructions; `p_t` = fraction of branches taken.
- **Example:** `f_b = 0.20`, `p_t = 0.60`, `P = 2` → `1 + 0.24 = 1.24`.
- **Limitation:** predict-taken adds `T_p` term; dynamic prediction uses `(1 − a)` not `a`.

## S10. Dynamic predictor CPI: `1 + f_b × (1 − a) × P`
- **What it solves:** speedup from a branch predictor with accuracy `a`.
- **When to use:** correct predictions cost 0; wrong ones pay full penalty `P`.
- **Example:** `f_b = 0.30`, `a = 0.80`, `P = 2` → `1 + 0.30×0.20×2 = 1.12`.
- **Limitation:** does not remove `P`; deeper pipes make `(1−a)×P` hurt more.

## S11. 2-bit saturating counter — loop exit
- **What it solves:** misprediction count on a loop branch (taken n−1 times, then not taken).
- **When to use:** steady state after warm-up; states 00/01 predict N, 10/11 predict T.
- **Why it works:** needs two consecutive contrary outcomes to flip a strong state; loop exit is one contrary after many taken.
- **Example:** 8-iteration loop, many executions → **1 misprediction per loop execution** (exit only); 1-bit predictor → **2** (exit + first iteration of next run).
- **Limitation:** initial state matters; alternating `T N T N` can make 2-bit lose to 1-bit.

## S12. Unified memory: +1 dead fetch per load/store (long programs)
- **What it solves:** structural CPI from one memory port.
- **When to use:** IF and MEM share one port; large N.
- **Why it works:** each load/store in MEM blocks one fetch slot.
- **Example:** 25 % memory instructions → `CPI = 1.25`.
- **Limitation:** tail effect — load/store among the last instructions may cost 0.

## S13. Multi-cycle EX bound: `2 + Σ e_i + 1` (4-stage IF–ID–EX–WB)
- **What it solves:** total cycles when EX times dominate and forwarding is satisfied.
- **When to use:** non-pipelined EX unit, blocking in-order.
- **Example:** EX times 4, 3, 1, 1 → `2 + 9 + 1 = 12`.
- **Limitation:** if dependences force extra gaps beyond serial EX occupancy, schedule explicitly.

## S14. Forwarding worth it iff `(1+s_fwd)τ_fwd < (1+s_no)τ_no`
- **What it solves:** whether slower clock with fewer stalls wins.
- **When to use:** question gives both stall fractions and clock change.
- **Example:** no-fwd `(1.7)(1.4) = 2.38` ns/instr vs fwd `(1.3)(1.55) = 2.015` → **1.18×** faster.
- **Limitation:** compare products, not stall counts alone.

## S15. In-order 5-stage: only RAW is a data hazard
- **What it solves:** "which dependence causes a hazard?" MCQs.
- **When to use:** classic in-order pipeline, registers read in ID, written in WB.
- **Why it works:** WAR/WAW dependences exist in code but reads always precede later writes in this organisation.
- **Limitation:** out-of-order completion or late operand read → WAR/WAW become real.

---

## Do NOT use

| Tempting shortcut | Why it fails | Counterexample |
|---|---|---|
| Add isolated stall counts in a chain | Earlier stalls satisfy later dependences | `ADD;SUB R4,R1;AND R6,R1,R4` → sum of pairs gives 3, true extra is 2 |
| `P = r` for branch penalty | Counts one extra flush | EX resolution → penalty is **2**, not 3 |
| Forwarding removes all RAW stalls | Load-use bubble remains | `LW; ADD R3,R1,…` → always 1 stall |
| `CPI = 1 + f_b × P` under predict-not-taken | Penalty only on taken branches | `f_b=0.2, p_t=0.6, P=2` → 1.24, not 1.40 |
| One stall per load/store (unified memory) | Tail loads cost nothing | `ADD,SUB,OR,LW` (load last) → 8 cycles, not 9 |
| 2-bit predictor always beats 1-bit | Alternating patterns | `T N T N …` ×10 from weak NT → both miss all 10 |
| ID-resolution always better than EX | Operand may not be ready | Branch right after ALU producer: both cost 2 on taken path |
