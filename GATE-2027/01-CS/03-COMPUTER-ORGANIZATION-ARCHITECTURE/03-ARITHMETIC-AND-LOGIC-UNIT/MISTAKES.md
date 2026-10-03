# Arithmetic and Logic Unit — Mistakes to Avoid

Theory: [NOTES.md](NOTES.md) · Quick sheet: [REVISION.md](REVISION.md). This file lists *typical* error patterns for the topic. The final section is blank, for your own log.

## 1. Conceptual confusions

1. **Carry-out vs signed overflow.** Carry-out is the unsigned-overflow indicator for addition; signed overflow is C(n−1) ⊕ C(n). They are independent: 0x7F + 1 (V only), 0xFF + 1 (C only).
2. **Reading N as the true sign after overflow.** N is the stored bit; with V = 1 the true sign is the opposite.
3. **Zero flag as a comparison.** Z gives equality only, not direction.
4. **Borrow vs carry.** After A − B (as A + ~B + 1) the raw carry is 1 when there was *no* borrow. Some ISAs invert it. Read the stated convention.
5. **Signed vs unsigned compare on the same bit patterns.** 0x90 vs 0x30: signed A < B, unsigned A > B; one subtraction, different flags used.
6. **Θ(1) vs Θ(log n).** The textbook "constant 4 gate delays" CLA uses unbounded fan-in gates. With fan-in ≤ 2 the depth is Θ(log n) and cannot be less than ⌈log₂(2n+1)⌉.
7. **CLA vs skip/select.** Carry-skip and carry-select (equal blocks) are Θ(√n); only multi-level lookahead is Θ(log n).
8. **Logical vs arithmetic right shift.** Only arithmetic preserves the sign. Arithmetic shift rounds toward −∞.
9. **Shift = multiply without checking overflow.** Left shift by k is ×2ᵏ only if the top k + 1 bits are equal (signed) or zero (unsigned, top k).
10. **Booth = fewer 1s.** Booth operations are bit *transitions*; an alternating multiplier is the worst case (n operations).
11. **Restoring vs non-restoring.** Non-restoring skips the restoring addition but may need a final remainder correction.
12. **Data path as a "parallel" machine.** With a single bus, only one register drives the bus per step; steps are strictly dependent.

## 2. Formula mistakes

1. Full adder: writing Cout = A ⊕ B ⊕ Cin (that is the sum).
2. Dropping the C0 term or a product term when expanding C3/C4.
3. Using `2n` for ripple delay when the question gives separate carry and sum times (use (n−1)·t_carry + t_sum).
4. Multi-level CLA: adding the "going down" levels only once, or the sum delay twice. In the 4-bit-unit model the delay is 4L, not 2L.
5. Fan-in-2 CLA depth: 2 + 2⌈log₂ n⌉ (ceiling!), not 2 log₂ n.
6. Barrel shifter: stages = ⌈log₂ n⌉, muxes = n·⌈log₂ n⌉ (not n stages, not n² muxes).
7. Sequential multiplier time: n·(t_add + t_shift) only when both are executed every iteration; otherwise adds only for 1 bits.
8. FP multiply exponent: eX + eY − bias (subtract the bias once).
9. Carry-select: applying b·t_c + (n/b − 1)·t_m to unequal blocks; use C = max(ready, previous carry) + t_m.

## 3. Numerical / calculation mistakes

1. Writing the 2's complement of a number by inverting but not adding 1 (A − B off by one).
2. Wrong width: results of n-bit operations are reduced mod 2ⁿ; the product needs 2n bits.
3. Reading a hex pattern as unsigned when asked for signed (0x96 is 150 unsigned, −106 signed).
4. Off-by-one in ripple chains: carries through the first n − 1 adders, then the MSB sum.
5. Ceiling errors: ⌈log₂100⌉ = 7, not 6.64 or 6.
6. Forgetting to append the 0 (Q−1 = 0) when counting Booth operations.
7. Dropping the carry from an n-bit register add during a trace (the carry belongs in C for shift-add, and is discarded in Booth).
8. Mixing ns and clock cycles (cycles ÷ frequency in GHz gives ns).
9. Counting restore operations in restoring division as one per step instead of one per zero quotient bit.
10. Float alignment: shifting the larger operand instead of the smaller, or shifting the wrong direction.

## 4. PYQ-derived traps (entries that exist in this topic's mapping, newest → oldest)

* **2020, Q.4 (data-path ordering):** operands of a non-commutative operation staged in the wrong temporary; executing the operand transfers before the instruction is fetched; forgetting that the ALU result sits in a temporary until the next step. (Figure is garbled in the mapping: always check the PDF.)
* **2016, Q.33 (CLA delay with fan-in ≤ 2):** choosing the constant-time class because lookahead is "parallel", or the √n class because blocks are involved. The deciding assumption is the stated gate fan-in.
* **2008, Q.33 (auto-increment; misfiled, addressing-mode concept):** the trap is mixing hardware details of effective-address calculation with the mode's semantics; study it in the addressing-modes folder.
* Related skills mapped under Digital Logic (see [PYQ.md](PYQ.md) §3): confusing carry with overflow in overflow-detection questions; counting 1s instead of transitions in Booth questions; ignoring the effect of a left shift on the sign bit.

## 5. Examination-time mistakes

* Not writing the width, representation and carry/borrow convention before starting.
* Mixing the signed and unsigned reading in one question.
* Skipping the ordering dependency graph and "pattern matching" the options in a data-path question.
* Trusting a half-seen figure; note which parts of the figure are not available and solve by method.
* Spending time on exact gate counts when the question only asks for an asymptotic class.

## 6. How to check yourself

* After every add/subtract: recompute the result as an ordinary integer, reduce mod 2ⁿ and compare with the bit pattern.
* Verify V with both rules (carries XOR and sign rule); they must agree.
* For delay questions: list the critical-path stages in order and sum them; check that the path goes through the slowest block.
* For Booth: verify the final product by ordinary multiplication; check the count of transitions with the appended 0.
* For division: check quotient × divisor + remainder = dividend.
* For data path: for each step name its inputs and outputs, and confirm every input is produced earlier.
* Sanity-check asymptotic answers: doubling n should add a constant (log), double the delay (linear), or multiply it by √2 (square root).

---

## My Mistakes

| Date | Source | Question | Mistake | Root cause | Fix / Rule |
|---|---|---|---|---|---|
| | | | | | |
