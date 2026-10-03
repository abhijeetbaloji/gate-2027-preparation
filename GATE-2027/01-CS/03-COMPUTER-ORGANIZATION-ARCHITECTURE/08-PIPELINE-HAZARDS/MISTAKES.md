# Pipeline Hazards — Mistakes to Avoid

Theory: [`NOTES.md`](NOTES.md). Ideal-pipeline timing (no stalls): [`../07-INSTRUCTION-PIPELINING`](../07-INSTRUCTION-PIPELINING/).
This file lists *typical* errors; nothing here is a record of anyone's personal mistakes (see the empty table at the end).

## 1. Conceptual confusions

| Confusion | Reality |
|---|---|
| Any dependence is a pipeline hazard | In the in-order 5-stage pipe only **RAW** is a data hazard; WAR/WAW are name clashes that do not stall |
| RAR is a dependence type tested like RAW | Two reads never create a hazard |
| WAW is the same as anti-dependence | Anti = **WAR** (earlier reads, later writes); WAW = two writes to the same register |
| Forwarding eliminates all data hazards | Load-use still needs **1** bubble; late branch operands in ID may still stall |
| Forwarding needs no extra hardware | Requires muxes, bypass paths, and a forwarding unit |
| Predict-not-taken stalls on every branch | Penalty is paid only on **taken** branches |
| Stall-until-resolved and predict-not-taken have the same CPI | Stall-always: `1 + f_b P`; PNT: `1 + f_b p_t P` |
| Dynamic prediction removes the branch penalty `P` | It reduces how often `P` is paid: `1 + f_b (1−a) P` |
| Register renaming removes RAW hazards | Renaming removes **WAR/WAW** (false deps); RAW is real data flow |
| Delay slots are filled by hardware | The **compiler** (or assembler) places a legal instruction; it always executes |
| Structural hazard from one memory port adds 1 stall to every program | A load/store among the **last** instructions may block no pending fetch (tail effect) |
| Out-of-order issue is assumed in every pipeline question | Unless stated, use **in-order** classic 5-stage with RF read in ID, write in WB |

## 2. Formula mistakes

- Using `N × 5` or `5N` instead of `N + 4` for a stall-free 5-stage program.
- `CPI = 1 + stalls` on a **short** program — use `total cycles / N`.
- Adding isolated stall counts: `stall(I2) + stall(I3)` without scheduling the full sequence.
- Branch penalty `P = r` (stage number) instead of **`r − 1`**.
- PNT formula with `f_b × P` instead of `f_b × p_t × P`.
- Using fraction of **branches** where fraction of **all instructions** is required (`f_b`).
- Load-use CPI: `0.40 × 1` instead of `0.25 × 0.40 × 1` (load fraction × immediate-use fraction).
- Cache miss penalty applied to every instruction instead of `f_mem × miss_rate × penalty`.
- Speedup with different clocks: using CPI ratio only, forgetting `τ_np / τ_pipe`.
- Predictor speedup: double-counting penalty on wrong predictions (they pay the same `P` as no predictor).
- Delay-slot CPI: counting useful slot instructions as extra instructions **and** as stall cycles.
- Break-even predict-taken vs PNT: using `p_t > 0.5` instead of `p_t > P/(2P − T_p)`.

## 3. Numerical / calculation mistakes

- **RF-A vs RF-B:** same-cycle read after WB write changes no-forwarding stalls by **1** per dependence (`d=1` ALU→ALU: 2 vs 3).
- **Distance `d`:** counts instructions between producer and consumer, but after earlier stalls the **time** gap grows — recompute with ready-time.
- **Load-use:** stalling for store **data** from a preceding load (should be 0 with MEM→MEM forwarding).
- **Load-use:** no stall for store **address** from preceding load (should be 1).
- **Unified memory:** counting structural stalls without checking whether any instruction remains to fetch.
- **Multi-cycle EX:** treating MUL(3) as one cycle because "forwarding removes stalls" — the EX stage is still occupied 3 cycles.
- **Branch + data:** adding control and data penalties that **overlap** in the same cycle (schedule the sequence).
- **2-bit counter trace:** wrong initial state (00 vs 01 vs 11 changes miss count).
- **Percent vs fraction:** 20 % branches with 60 % taken → `0.20 × 0.60`, not `0.60`.
- Rounding NAT answers to wrong decimal places.

## 4. PYQ-derived traps (pattern; entry must exist in mapping; newest → oldest)

| Trap pattern | Kind of question | Entry |
|---|---|---|
| "Which dependence causes a data hazard?" — pick RAW, not "all except RAR" | dependence vs hazard | 2026 Q.16 |
| Forwarding cannot prevent **all** stalls; needs hardware | forwarding MSQ/MCQ | 2024 Q.30 (CS-1) |
| CPI speedup: data-stall % and control-stall % are fractions of **all** instructions | mixed hazard CPI | 2024 Q.58 (CS-2) |
| Predictor: correct predictions cost 0; speedup = CPI ratio | branch predictor | 2022 Q.61 |
| MUL/DIV/ADD: operand read in EX/OF, multi-cycle PO/EX, forwarding from PO | variable-latency sequence | 2021 Q.53 (Set-2), 2015 Q.53 (Set-2), 2007 Q.37 |
| Anti-dependence = WAR; "always creates stall" is false in-order | dependence statements | 2015 Q.49 (Set-3) |
| Stall fraction speedup: `k/(1 + f×s)` only when balanced, same clock, no overhead | CPI speedup | 2014 Q.43 (Set-1) |
| Stage split changes **both** branch penalty stage and clock period | design comparison | 2014 Q.43 (Set-3) |
| "Bypassing handles **all** RAW" / "renaming eliminates **all** WAR" / "prediction eliminates **all** control penalty" | absolute claims | 2008 Q.36, 2012 Q.20 |
| Memory + branch stalls in one CPI sum; miss penalty only on memory instructions | mixed stalls | 2020 Q.43 |
| Register renaming purpose — hazards, not address translation or compile-time allocation only | concept MCQ | 2012 Q.20 |
| Ideal pipeline timing (no hazards) filed in this mapping — belongs to topic 07 | adjacent entry | 2025 Q.56, 2023 Q.33, 2021 Q.53 (Set-1), 2018 Q.50, 2015 Q.55 (Set-1) |

## 5. Examination-time mistakes

- Not stating RF-A/RF-B, forwarding, or branch-resolve stage before counting cycles.
- Drawing no timing diagram for a sequence question (errors in stall placement).
- Picking "WAR" or "WAW" for hazard MCQs without checking the pipeline model.
- Forgetting that a **not-taken** branch under predict-not-taken costs **0** control stalls.
- Moving an instruction into a delay slot without checking dependence on the branch condition.
- Using the old branch-penalty formula after a pipeline redesign (2014 Set-3 style).
- Assuming initial predictor state when the question does not give it.
- Leaving speedup as a ratio when the question asks for execution time in ms/µs.

## 6. How to check yourself

1. Did I state forwarding, RF timing, and where branches resolve?
2. For sequences: did I use ready-time (max over sources), not sum of pairs?
3. Load followed immediately by user → did I add exactly 1 stall (with forwarding)?
4. Branch penalty = stages between IF and resolution minus 1?
5. CPI fractions: each `f_i` is a fraction of **all** instructions?
6. Speedup: did I include both CPI and clock frequency?
7. Hazard MCQ: in-order 5-stage → only RAW?
8. Does my cycle count equal `N + 4 + extra` (for classic 5-stage)?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
| | | | | | |
