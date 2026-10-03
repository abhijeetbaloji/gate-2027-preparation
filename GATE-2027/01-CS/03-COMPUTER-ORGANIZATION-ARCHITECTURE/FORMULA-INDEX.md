# COA — Formula Index

Cross-topic index into each folder's `FORMULAS.md`. Every entry states **when** it applies; full derivations and examples are in the linked file.

**Conventions (whole COA section):** 1 K = 2¹⁰; iron law `CPU time = IC × CPI × τ`; pipeline `k + N − 1` cycles when stall-free; cache split `tag | index | offset`.

---

## 01 — Instruction Set

[`01-INSTRUCTION-SET/FORMULAS.md`](01-INSTRUCTION-SET/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A1 | bits = ⌈log₂ n⌉ | Opcode, register, mode field widths |
| A2 | immediate bits = L − fixed fields | 2025/2016 immediate NATs |
| A3 | Signed/unsigned range of w bits | Offset/literal limits |
| B1 | Program bytes = N × ⌈instruction bits / 8⌉ | 2016 byte-aligned size |
| C1–C2 | Format bit → opcode width per type | 2024 R/I split |
| D1–D2 | Expanding opcode space fraction | 2020, 2026 max-opcode NATs |
| E2 | PC-relative reach ≈ 2^(w−1) × instruction size | Branch range |
| F2–F3 | Stack depth; Sethi–Ullman register labels | Expression evaluation machines |
| G1 | Spill ≥ peak live − k registers | 2013 register-pressure (code in paper) |
| H1 | CPU time = IC × CPI × τ | Performance bridge to pipelining |

---

## 02 — Addressing Modes

[`02-ADDRESSING-MODES/FORMULAS.md`](02-ADDRESSING-MODES/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A1–A7 | EA for immediate, direct, indirect, base, index, scaled, auto-inc/dec | Mode identification and memory refs |
| B1 | Branch target = PC_updated + offset | PC-relative branches |
| B2 | Reach of signed w-bit offset | Range MCQs |
| C1 | Opcode bits = L − mode − registers − literal | 2024 CS2 opcode NAT |
| D2 | Cycles per mode in a stated fetch model | Timing comparison |
| E | Array/record/pointer address arithmetic | Base+index examples |

---

## 03 — Arithmetic and Logic Unit

[`03-ARITHMETIC-AND-LOGIC-UNIT/FORMULAS.md`](03-ARITHMETIC-AND-LOGIC-UNIT/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| B3 | Ripple delay Θ(n) gate delays | vs CLA comparison |
| B6–B7 | CLA delay Θ(log n) with fan-in ≤ 2 | 2016 Q33 |
| C2 | Overflow V = C_in(MSB) ⊕ C_out(MSB) | Signed add MCQs (often in DL PYQs) |
| F2 | Booth: count bit-pair changes + 1 | Multiplication NATs |
| G1–G2 | Restoring / non-restoring step counts | Division traces |
| H | IEEE add/mul steps (normalise, round) | FP ALU (bridge to DL) |
| I | Single-bus micro-op ordering | 2020 datapath MCQ |

---

## 04 — Control Unit

### Hardwired

[`04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/FORMULAS.md`](04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| B1 | Step counter bits = ⌈log₂ steps⌉ | Control hardware counting |
| B3 | One-hot: n flip-flops for n states | vs encoded FSM |
| C2–C5 | Multi-cycle CPI; clock ≥ slowest path | Timing comparison |
| C8 | Ideal pipeline k+N−1 (bridge) | vs hardwired multi-cycle |

### Microprogrammed

[`04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/FORMULAS.md`](04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A1 | CAR width = ⌈log₂ microinstructions⌉ | Control store addressing |
| B1 | Encoded field = ⌈log₂(n+1)⌉ | Horizontal vs vertical width |
| C2 | ROM bits = words × width | Control-store size NATs |
| D1 | Nanostore + microstore size | Two-level control |
| E2 | Machine instruction time = μ-steps × μ-cycle | CPI in microcycles |

---

## 05 — Memory Interfacing and Hierarchy

### Performance

[`05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/FORMULAS.md`](05-MEMORY-INTERFACING-AND-HIERARCHY/01-PERFORMANCE/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A2 | Block time = first word + (B−1) × subsequent | Miss penalty |
| B1–B2 | Interleaved memory bandwidth | Low/high-order interleaving |
| C1 | Hierarchical AMAT: T = H₁T₁ + (1−H₁)(T₁+…) | **State model explicitly** |
| C1 alt | Simultaneous: T = H₁T₁ + (1−H₁)H₂T₂ + … | L1/L2 parallel lookup |
| C3 | Global vs local miss ratio conversion | Multi-level cache |
| F1 | CPI_eff = CPI_base + refs/instr × m × penalty | CPU + memory stalls |
| E1 | Break-even hit ratio from two AMATs | 2022-style solve-backwards |

### Cache Memory Mapping

[`05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/FORMULAS.md`](05-MEMORY-INTERFACING-AND-HIERARCHY/02-CACHE-MEMORY-MAPPING/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A1 | offset = log₂B; index = log₂(#sets); tag = A − index − offset | **Start every cache problem here** |
| B1 | tag_SA = tag_DM + log₂k | 2026 tag relation |
| C1 | Tag storage = lines × tag bits | 2025 tag-directory NAT |
| C2 | Memory = 2^(tag+index+offset); cache = lines × B | Field-width MCQs |
| E2 | Max cache from one address→line constraint | 2026 NAT |
| F2 | Simulate LRU/FIFO per set | P,Q,R,S loops |
| G | 3C misses: compulsory, capacity, conflict | Classification |
| H | AMAT with cache hit time + miss penalty | Overlaps Performance C1 |

---

## 06 — I/O Interface

### Interrupt

[`06-IO-INTERFACE/01-INTERRUPT/FORMULAS.md`](06-IO-INTERFACE/01-INTERRUPT/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| F4 | Polling CPU fraction = f_poll / f_cpu | 2023-style NAT |
| F6–F7 | Interrupt fraction = events × cost / time | CPU load |
| F10 | Crossover: f_int = f_poll (break-even rate) | PIO vs interrupt |
| F13 | Saved PC = next instruction address | Return-address MCQs |
| F20 | Daisy-chain grant delay = n × t_prop | Priority hardware |

### DMA

[`06-IO-INTERFACE/02-DMA/FORMULAS.md`](06-IO-INTERFACE/02-DMA/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| rate-from-fraction | Device rate = f_cpu × fraction × bytes/cycle | 2024 CS2, 2021 |
| burst-vs-stealing | Block time vs per-cycle steal | Mode comparison MCQs |
| acquisitions | Bursts = ⌈file size / count register⌉ | 2016 CS-1 NAT |
| break-even | Block size where DMA beats interrupt overhead | Design choice |
| bandwidth | Peak = bus width × clock | Bus sizing |

---

## 07 — Instruction Pipelining

[`07-INSTRUCTION-PIPELINING/FORMULAS.md`](07-INSTRUCTION-PIPELINING/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| F1 | Cycles = k + N − 1 (no stalls) | Basic pipeline NAT |
| F9–F11 | Speedup = Nk/(k+N−1); asymptotic → k | Speedup MCQs |
| F17 | τ = max(stage delay) + latch overhead | Clock period |
| F18 | Split stage → new τ = max(a,b)+overhead | 2016 split-stage |
| F23 | Iron law (same as ISA H1) | CPI/time chains |
| F25 | CPI_pipe = 1 + stall fraction | With simple stall input |

---

## 08 — Pipeline Hazards

[`08-PIPELINE-HAZARDS/FORMULAS.md`](08-PIPELINE-HAZARDS/FORMULAS.md)

| ID | Formula / rule | Typical GATE use |
|----|----------------|------------------|
| A1 | Total = (k+N−1) + stalls | After trace |
| B1 | stalls = max(0, H − (d+U)) | Single dependence |
| B2 | Distance table (d=1,2,3) | Quick lookup |
| B3 | Load-use: 1 stall with forwarding | Most common data hazard |
| C1 | Unified memory: +1 cycle per load/store MEM | Structural |
| D1 | Branch penalty P = resolution_stage − 1 | Control hazard |
| D2 | CPI = 1 + f_b × (policy terms) | Branch prediction |
| E2 | 2-bit predictor: 1 mispredict/loop vs 2 for 1-bit | Predictor MCQs |
| F1 | CPI = 1 + Σ f_i s_i | Mixed stalls |
| F3 | Speedup = (CPI_np τ_np)/(CPI_pipe τ_pipe) | With clock change |

**Register-file assumption:** B1–B2 tables assume **RF-A** (write first half, read second half) unless the question states RF-B. See [`08-PIPELINE-HAZARDS/NOTES.md` §1](08-PIPELINE-HAZARDS/NOTES.md).

---

## Quick topic → formula map (exam drill)

| If the question mentions… | Open first |
|---------------------------|------------|
| Opcode, immediate, instruction size | 01-A, 01-D |
| Effective address, branch offset | 02-A, 02-B |
| CLA delay, Booth, datapath steps | 03-B, 03-F, 03-I |
| Control store, microinstruction width | 04-micro B, C |
| AMAT, interleaving, chip select | 05-perf C, B |
| Tag, index, hit/miss trace | 05-cache A–F |
| Polling vs interrupt CPU % | 06-int F4–F7 |
| DMA rate, burst, count register | 06-DMA |
| k+N−1, speedup, clock period | 07-F1, F9, F17 |
| Stalls, forwarding, branch CPI | 08-B, 08-D |

---

## Related formula sheets outside COA

| Subject | Path |
|---------|------|
| Fixed-point / Booth / overflow PYQs | [`../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/`](../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/) |
| TLB / page fault effective time | [`../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/`](../08-OPERATING-SYSTEMS/08-MEMORY-MANAGEMENT-AND-VIRTUAL-MEMORY/) |
| Global formula dump | [`../17-FORMULAS/COA/`](../17-FORMULAS/COA/) (if populated) |
