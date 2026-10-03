# Arithmetic and Logic Unit — Shortcuts

Only shortcuts that are logically valid. Details and derivations: [NOTES.md](NOTES.md); formulas: [FORMULAS.md](FORMULAS.md). All examples verified by script.

---

## S1. Signed overflow from operand and result signs (no carries needed)

* **What it solves:** "does this add/subtract overflow in n-bit 2's complement?"
* **When:** you can read the three sign bits.
* **Why it works:** overflow requires the true result to leave the range; with operands of opposite sign (for addition) the sum lies between them and always fits (NOTES §7.2).
* **Rule:** addition — operands same sign, result opposite sign ⇒ overflow. Subtraction A − B — operands different sign and result sign ≠ sign(A) ⇒ overflow.
* **Example:** 4-bit 0111 + 0011 (7 + 3): same sign (0,0), result 1010 (sign 1) ⇒ overflow. 4-bit 1000 − 0001 (−8 − 1): different signs, result 0111 has sign 0 ≠ 1 ⇒ overflow.
* **Limitation:** valid only for 2's complement. Sign-magnitude uses the magnitude carry-out; unsigned uses the carry-out.

## S2. Unsigned vs signed overflow at a glance

* **What it solves:** which flag to inspect.
* **Rule:** unsigned add wraps ⟺ C = 1; signed add wraps ⟺ V = 1. The two are independent: 0x7F + 1 (V only), 0xFF + 1 (C only), 0x80 + 0x80 (both).
* **Limitation:** for subtraction the *unsigned* wrap (borrow) is C = 0 in the raw-carry convention (C = 1 in the borrow convention).

## S3. Reading a pattern sum quickly by modular arithmetic

* **What it solves:** the stored 8-bit result of an addition.
* **How:** add as ordinary numbers, subtract 256 if ≥ 256 (that is the carry), then read the pattern as signed by subtracting 256 again if ≥ 128.
* **Why:** the adder computes the sum mod 2ⁿ.
* **Example:** 100 + 50 = 150 → pattern 0x96 → signed 150 − 256 = −106 (V = 1 because 150 > 127).
* **Limitation:** this tells you the value, not the flags; derive V from the signs (S1).

## S4. Longest ripple carry chain for fixed A

* **What it solves:** which B causes the maximum latency in an n-bit ripple adder with A given.
* **How:** the chain starts at the lowest set bit of A (generate needs both bits 1) and, for B = −A, every higher bit propagates. Length = n − (index of lowest set bit of A).
* **Example:** 8-bit A = 3 → B = −3 = 1111 1101, chain 8. A = 12 (lowest set bit 2) → B = −12, chain 6.
* **Limitation:** the delay is data-dependent; "worst case" always means this maximum.

## S5. Counting Booth add/sub operations

* **What it solves:** "how many additions/subtractions in Booth's algorithm?"
* **How:** append a 0 on the right of the multiplier and count the places where adjacent bits differ.
* **Why:** an operation happens exactly at the start (1,0) and just after the end (0,1) of every run of 1s.
* **Example:** Q = 0111 0010 → 0111 0010 0 → 4 changes → 4 operations. Q = 1100 1011 → 1100 1011 0 → 5 changes → 5 operations.
* **Limitation:** counts add/sub only; the number of shift steps is always n. For radix-4 count non-zero digits instead.

## S6. Booth: runs of 1s

* **How:** a run of 1s from bit i to j contributes `2^(j+1) − 2ⁱ`, i.e. one subtraction and one addition, regardless of the run length.
* **Limitation:** a single isolated 1 (…010…) costs two operations in radix-2, more than shift-add (one). Booth wins only on long runs.

## S7. Arithmetic shift as division and multiplication by powers of two

* **Rule:** x << k = x·2ᵏ if the top k + 1 bits (signed) or top k bits (unsigned) are all equal to the sign / zero; x >> k (arithmetic) = ⌊x/2ᵏ⌋.
* **Example:** −44 ASR 2 = −11. −7 ASR 1 = −4 (not −3).
* **Limitation:** logical right shift is not division for negative signed numbers; ASR rounds toward −∞.

## S8. Barrel shifter size and delay

* **Rule:** muxes = n·log₂n, delay = log₂n mux delays (independent of the shift amount); to find which stages are used, write the shift amount in binary.
* **Example:** 32 bits → 160 muxes; 64 bits, 0.35 ns per stage → 2.1 ns.

## S9. Signed vs unsigned compare from flags

* **Rule (raw-carry convention):** unsigned A < B ⟺ C = 0; signed A < B ⟺ N ⊕ V = 1; equal ⟺ Z = 1.
* **If C is defined as borrow:** unsigned A < B ⟺ C = 1.
* **Limitation:** always check which convention the question defines.

## S10. Adder delay classes

* **How:** ripple Θ(n); carry-skip/select equal blocks Θ(√n); fan-in-2 lookahead Θ(log n); idealised unbounded fan-in lookahead Θ(1). A lower bound for fan-in-2 follows from "S(n−1) depends on 2n + 1 inputs ⇒ depth ≥ ⌈log₂(2n+1)⌉".
* **Limitation:** statements about constants (exact gate delays) need the stated model.

## S11. Multi-level CLA delay

* **Rule (model GD, 4-bit units):** delay = 4L gate delays for L levels (16-bit: 8, 64-bit: 12). With problem-specific stage times, add: P/G ready time + lookahead-unit delay + final sum time, along the critical path that goes through the top-level carry.
* **Example:** P,G at 7 ns, lookahead 9 ns, sum 11 ns after carry → 27 ns for every sum bit if all carries come from the lookahead.
* **Limitation:** the first section may start earlier because it uses the external carry-in; it is not the critical one.

## S12. Restoring division restore count

* **Rule:** number of restores = number of 0 bits in the n-bit quotient (when the quotient fits); total add/sub = n + restores.
* **Example:** 45 ÷ 7, n = 6: quotient 000110 → 4 restores → 10 operations.

## S13. Ordering data-path steps

* **How:** write the chain PC → MAR → MDR → IR first, then "first operand to Y", then "second operand + ALU → Z", then "Z → destination". Cross out options violating any edge.
* **Limitation:** only valid when the steps are single-bus and the dependencies are as listed; check non-commutative operations (SUB: first operand must be in Y).

---

## Do NOT use

1. **"Carry-out = 1 means overflow."** Counterexample: 0xFF + 0x01 has C = 1 but −1 + 1 = 0 is correct; 0x7F + 0x01 has C = 0 but overflows.
2. **"Sign of result negative ⟹ A < B (signed)."** Counterexample: 0x80 − 0x01 gives 0x7F (N = 0) although −128 < 1; 0x90 − 0x30 gives N = 0, V = 1, signed A < B.
3. **"x >> k = x / 2ᵏ in code for all signed x."** Counterexample: −7 >> 1 = −4 but −7 / 2 = −3 under truncation; logical shift breaks negatives.
4. **"Number of Booth operations = number of 1s in the multiplier."** Counterexample: 4-bit 0111 has three 1s but only two operations; 4-bit 0101 has two 1s but four operations (0101 followed by the appended 0 changes value four times).
5. **"Lookahead adders are constant time."** Only with unbounded fan-in gates; with fan-in ≤ 2, depth ≥ ⌈log₂(2n+1)⌉.
6. **"More hardware (more buses) always speeds the clock."** More buses reduce steps per instruction, not necessarily the cycle time.
7. **"Delay of FP add = delay of integer add."** Alignment, normalisation and rounding add shifters and extra adders to the path.
