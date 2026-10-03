# Pipeline Hazards — Last-Minute Revision

Full theory [`NOTES.md`](NOTES.md) · ideal pipeline timing (no stalls): [`../07-INSTRUCTION-PIPELINING`](../07-INSTRUCTION-PIPELINING/).

## Three families
| Hazard | Cause | Cure |
|---|---|---|
| **Structural** | Two instructions need the same resource (one memory port, busy multi-cycle unit) | Duplicate resource, pipeline the unit, or stall |
| **Data** | Consumer needs a value the producer has not finished (RAW) | Forwarding, interlock, scheduling, renaming (WAR/WAW only OoO) |
| **Control** | Next PC unknown (branch/jump) | Resolve earlier, predict, delay slot, flush |

## Dependences vs hazards (in-order 5-stage)
```
RAW (read after write)   : real flow — ONLY data hazard here
WAR (write after read)   : anti-dependence — name clash, NOT a hazard in-order
WAW (write after write)  : output dependence — NOT a hazard in-order
RAR                      : not a dependence
```
WAR/WAW become hazards when instructions complete out of order or operands are read late.

## Must-remember formulas
```
total cycles = (N + k − 1) + stalls          k = 5  →  base N + 4
CPI = total / N   (short prog)    long-run: CPI → 1 + avg stalls per instruction

Single RAW stall:  stalls = max(0, H − d − U)     d = instruction distance

Ready-time:  X_1 = 3 ;  X_i = max(X_{i−1}+1, gates) ;  total = X_N + 2
  gate (no fwd, RF-A): X_p + 3     (no fwd, RF-B): X_p + 4
  gate (fwd, ALU): X_p + 1         (fwd, load): X_p + 2

Load-use (fwd):  adjacent use → 1 stall ;  ≥1 independent instr between → 0

Branch penalty:  P = r − 1   (resolved at end of stage r; IF=1…MEM=4)

CPI control:
  stall always        1 + f_b × P
  predict not taken   1 + f_b × p_t × P
  predict taken       1 + f_b × [p_t T_p + (1−p_t) P]
  dynamic (acc a)     1 + f_b × (1−a) × P
  delay slots (n)     1 + f_b × Σ(1 − u_j)

Speedup = (CPI_np / f_np) / (CPI_pipe / f_pipe)
Unified memory (long run): CPI = 1 + f_mem
```

## Distance table — adjacent (`d = 1`), RF-A
| Case | No fwd | Fwd |
|---|---:|---:|
| ALU → ALU | 2 | 0 |
| LOAD → ALU | 2 | **1** |
| ALU → branch (ID) | 2 | 1 |
| LOAD → branch (ID) | 3 | 2 |

## Timing picture (load-use, forwarding)
```
Cycle     1   2   3   4   5   6
LW R1         IF  ID  EX  MEM WB
ADD R3,R1         IF  ID  --  EX MEM WB
                              ^ 1 bubble
```

## Branch flush (predict not taken, resolve in EX, taken)
```
Cycle     1   2   3   4   5   6
BEQ           IF  ID  EX  MEM WB
wrong I+1         IF  ID  xx
wrong I+2             IF  xx
target L                  IF  ID  EX
```
Penalty = **2** cycles.

## 2-bit saturating counter
```
00,01 → predict N     10,11 → predict T
taken: s ← min(s+1,3)   not taken: s ← max(s−1,0)
```
Loop exit: 2-bit → ~1 miss/execution; 1-bit → ~2 misses/execution (steady state).

## Fast-solve checklist
1. State model: forwarding? RF-A or RF-B? branch resolve stage? unified memory?
2. List each instruction's D and S registers; classify RAW/WAR/WAW if asked.
3. For cycle count: ready-time method (not sum of isolated stalls).
4. Load immediately before user → check load-use (1 stall with fwd).
5. Branch: penalty = r − 1; policy (stall / PNT / predictor / delay slot).
6. CPI: `1 + Σ f_i s_i` — fractions are of **all** instructions.
7. Speedup: include clock ratio if frequencies differ.
8. Sanity: CPI ≥ 1; forwarding cannot remove every RAW stall.

## Top traps
- Dependence ≠ hazard (WAR/WAW in in-order pipe).
- Summing per-pair stalls in a chain.
- `P = r` instead of `r − 1`.
- Predict-not-taken: multiply by `p_t`.
- Load → store *data*: 0 stalls; load → store *address*: 1 stall.
- Filled delay slot that moves feeder next to branch (ID resolve) → no gain.
- Unified memory: +1 per load/store only when a fetch is still pending.
- Multi-cycle EX: unit is busy — not "free" with forwarding.
- 2-bit predictor initial state ignored in trace questions.

## High-frequency PYQ concepts (from mapping triage)
RAW-only hazard MCQ (2026); forwarding statements (2024 CS-1); MUL/DIV/ADD stall counting with forwarding (2021 Set-2, 2015 Set-2, 2007); CPI/speedup with stall fractions (2024 CS-2, 2020, 2014); branch predictor speedup (2022); anti-dependence classification (2015 Set-3); "all/always" statements on bypassing/renaming/prediction (2008, 2012); stage-split branch stall comparison (2014 Set-3).
