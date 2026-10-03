# Microprogrammed Control — Revision sheet

Depth is **syllabus-driven; no mapped PYQ** for this leaf ([PYQ.md](PYQ.md)). Full theory: [NOTES.md](NOTES.md). Formulas: [FORMULAS.md](FORMULAS.md).

## Definitions
- **Control store/memory:** ROM (or WCS) inside the CPU holding microinstructions; not user-addressable.
- **Microinstruction:** one row = control signals for one step + next-address information. **Micro-operation:** one transfer/ALU action. **Microroutine:** microinstruction sequence for one machine instruction.
- **CAR/µPC:** address of the microinstruction being read; width ⌈log₂ N⌉. **CDR/µIR:** holds the current microinstruction.
- **Fetch routine** is shared; at its end **MAP** (mapping ROM or opcode ‖ step bits) jumps to the execute routine; execute routines end by jumping back to fetch.
- **Sequencing modes:** increment, absolute jump, conditional branch (status bit), map, call/return (SBR), address modification.

## Must-remember formulas (1 K = 2¹⁰)
```
 CAR bits         = ⌈log₂ N⌉              absolute next-address field of a bits -> 2ᵃ words
 encoded field    = ⌈log₂ n⌉ (exactly one)   |   ⌈log₂ (n+1)⌉ (none allowed)       per group, then add
 horizontal width = signals + mode/cond + next-address
 control store    = N × W bits (+ mapping ROM = 2^(opcode bits) × CAR bits)
 N                = shared fetch (once) + Σ execute routines
 nano two-level   = M·⌈log₂ D⌉ + D·W       (flat = M·W; helps only if D ≪ M)
 t_µ non-overlap  = t_CS + t_dec + t_dp ;  overlapped = max(t_CS, t_dec + t_dp)
 CPI              = Σ fᵢ·µᵢ ;  T_instr = µ × t_µ
```

## Horizontal vs vertical (field-encoded in between)
| | Horizontal | Vertical / encoded |
|---|---|---|
| Word width | wide | narrow |
| Decoders | none/few | needed |
| Parallelism | high | low |
| Microinstructions needed | fewer | more |
| Speed | faster | slower |
| Total bits | compute N × W for both | compute N × W for both |

## Micro vs hardwired
Micro: flexible, easy to modify/debug, slower, needs ROM + sequencer, fits complex (CISC) ISAs. Hardwired: faster, rigid, hard for large irregular ISAs, typical of simple/RISC-style pipelined cores. See [sibling](../01-HARDWIRED/NOTES.md).

## Mini-1 reference (NOTES Section 4)
Fetch: `F0 PCout,MARin,Read,INC,Tin | F1 Tout,PCin | F2 MDRout,IRin,MAP`. ADD 3 words, LOAD 2, STORE 3, BZ 3 (1 if not taken). Encoded word 19 bits, horizontal 30; 14 words → 266 vs 420 bits.

## Fast-solve checklist
1. Is "none" allowed? "at most one" vs "exactly one"? 2. Group only mutually exclusive signals. 3. Ceil per group. 4. Add direct bits + condition + mode + next-address. 5. N: fetch once. 6. N × W; check units. 7. For comparisons compute both sides. 8. State the microcycle model.

## Top traps
Forgetting "+ none" (8 → 4 bits, 16 → 5); fetch counted per instruction; control memory ≠ main memory; vertical not always smaller in total; nanoprogramming only when D ≪ M; one bus source per step in a micro-op list; overlap formula only if stated.

## PYQ note
No PYQ is mapped to this leaf; nearby items live in the hardwired (2018 Q.5) and interrupt (2013 micro-operations) mappings.
