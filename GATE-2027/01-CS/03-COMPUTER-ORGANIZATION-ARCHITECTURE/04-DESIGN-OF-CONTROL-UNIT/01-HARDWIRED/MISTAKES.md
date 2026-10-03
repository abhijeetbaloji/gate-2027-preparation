# Hardwired Control — Mistakes to Avoid

These are *generic, anticipated* error patterns, written from the concepts in [NOTES.md](NOTES.md). They are not a record of any student's own mistakes; the personal log is the empty table at the end.

---

## 1. Conceptual confusions

| Mistake | Correct idea | NOTES |
|---|---|---|
| "Hardwired" means the processor cannot run different programs | Only the *control logic* is fixed; the ISA is fixed, programs vary | §2 |
| Thinking a hardwired unit reads a control word / has a control memory | Control memory is the defining store of microprogrammed control | §12 |
| Believing fetch depends on the opcode | Opcode is unknown during fetch; fetch is identical for all instructions | §5.2 |
| Treating decode as a separate clock step | In the NOTES model decoding is combinational off IR and takes no step | §4 rule 7 |
| Thinking flags and DMA/interrupt lines generate all control signals | They only qualify specific terms/sequences | §13 |
| Equating "more steps" with "slower machine" | Time = CPI × T_clk; shorter clock may compensate | §11, Shortcut S7 |
| Thinking multi-cycle is always faster than single-cycle | Depends on stage balance, overhead and mix | §11 |
| Confusing a truth-table ROM addressed by (opcode, step) with a microprogram store | The ROM has no sequencing/next-address; order comes from the counter | §8.4 |
| "Hardwired is better because it's faster" | It is faster but harder to design/modify for large ISAs | §12.1 |
| Assuming RISC features are independent facts to memorise | They support each other (simple decode ↔ pipelining ↔ hardwired) | §12.2 |

## 2. Formula mistakes

- Step-counter bits as ⌊log₂ N⌋ or N − 1; correct is ⌈log₂ N⌉ with N = steps of the **longest** instruction including fetch (FORMULAS B1).
- State-register bits using the longest instruction instead of **all** distinct states when the design is a one-state-per-state FSM (B2).
- One-hot counted as ⌈log₂ N⌉ (it is N flip-flops) (B3).
- Decoder gate count taking the number of inputs instead of outputs used, or forgetting that an n-input AND is n − 1 two-input gates (B4).
- ROM size: **adding** address bits and signal count, or reporting bits when bytes are asked (B5).
- Clock period: adding parallel decoder delays; forgetting clk→Q or setup; adding an ALU term to a step that has none (C4).
- CPI: unweighted average; applying the memory wait to every step; truncating L = ⌈T_mem/T_clk⌉ (C2, C3).
- Control equation: factoring a common step through a fetch term (`(T1 + LDA + STA)·T4`); putting a flag on the whole `PCin` (A1).

## 3. Numerical / calculation mistakes

- **Units:** ns vs ps (1 ns = 1000 ps); MHz → Hz; ms vs s (80 ms = 0.08 s); bits vs bytes (÷ 8 at the end only).
- **Off-by-one in steps:** forgetting that the `WMFC` wait is a step of its own when it cannot share with a bus transfer; counting T1…T6 as 5 steps.
- **Fetch forgotten:** reporting 3 for ADD when the question asks for total steps (6), or reporting 6 when it asks for execute steps (3).
- **ceil/floor:** L = ⌈25 / 8⌉ = 4, not 3; ⌈log₂ 8⌉ = 3 (exactly 8 states needs 3 bits, not 4).
- **Rounding too early** in weighted CPI before multiplying by the clock period.
- **Speed-up direction:** speed-up of A over B = time(B)/time(A); reporting its reciprocal.

## 4. PYQ-derived traps (kinds, newest → oldest)

| Year | Mapping entry | Trap kind |
|---|---|---|
| 2020 | Q.4 (cross-filed under ALU) | Shuffled datapath steps: operand order for the ALU latch, fetch steps first, write-back last; the mapped text is garbled so use the PDF |
| 2018 | Q.5 (this folder) | RISC-feature combination question: evaluate each feature on its own (register–register arithmetic / load-store, fixed-length instructions, hardwired control) and only then pick the combination; the official answer is unverified in the mapping |
| 2013 | Q.28 / Q.45 / Q.34 / Q.39 (cross-filed under Interrupt; one question in four booklets) | Micro-operation sequence interpretation: judge by what each transfer does, not by register names |

## 5. Examination-time mistakes

- Not reading which design the question describes (step counter vs state register vs one-hot) before computing bits.
- Skipping the assumption lines (single bus? Y/Z registers? memory latency in cycles? overhead per cycle in all designs?).
- Starting arithmetic before drawing the micro-operation table.
- Not rechecking that no step has two `…out` signals.
- Spending time on a long RISC/CISC statement list without marking each statement T/F first.

## 6. How to check yourself

1. Does every step of my table have ≤ 1 `out`?
2. Are fetch steps included/excluded as the question requires?
3. Did I use the right N for the log (longest instruction vs all states)?
4. Parallel paths → max; serial → sum?
5. Weighted CPI × clock period for the final time?
6. Units: ns/ps, bytes/bits, ms/s?
7. Does my equation for each signal include the fetch term unconditionally?
8. For RISC/hardwired statements: did I judge each separately?

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
