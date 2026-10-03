# Arithmetic and Logic Unit — Practice

Original questions (not from any GATE paper and not copied from the repo's existing practice file). Each answer sits directly under its question; try the question first. Theory: [NOTES.md](NOTES.md). All answers were recomputed by script.

Conventions for every question unless it says otherwise:
* Registers are 2's complement; hex numbers are n-bit patterns.
* Flags: Z, N (= result MSB), C, V = (carry into MSB) XOR (carry out of MSB). After a subtraction A − B computed as A + ~B + 1, **C is the raw carry-out** unless the question says "borrow flag".
* Gate-delay model: every 2-input gate costs 1 delay; wires 0.

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1

Which expression is the carry-out of a full adder with inputs A, B and Cin?

A. A ⊕ B ⊕ Cin  
B. A·B + Cin·(A ⊕ B)  
C. A + B + Cin (logical OR of the three inputs)  
D. (A ⊕ B)·Cin

**Answer:** B

**Solution:** The carry leaves the bit if both inputs are 1 (A·B, "generate") or if exactly one input is 1 and a carry arrives (Cin·(A ⊕ B), "propagate"). That is option B (it equals the majority function). A is the sum bit. C is 1 for (1,0,0) although the carry-out is 0. D misses the case A = B = 1 with Cin = 0 (carry-out 1, expression 0).

**Concept tested:** full-adder equations, generate/propagate (NOTES §3.2).  
**Difficulty:** Easy.  
**Common trap:** confusing the sum (odd parity) with the carry (majority).

---

### Q2 — NAT — Level 1

A 128-bit barrel shifter is built from stages of 2:1 multiplexers (one stage per bit of the shift amount, each stage 128 multiplexers). How many 2:1 multiplexers does it contain? (Integer.)

**Answer:** 896

**Solution:** Shift amounts 0…127 need log₂128 = 7 bits, so 7 stages. Each stage has 128 muxes: 7 × 128 = 896.

**Concept tested:** barrel shifter size n·log₂n (NOTES §9.3).  
**Difficulty:** Easy.  
**Common trap:** using 128 stages (one per shift position) or 128 muxes in total.

---

### Q3 — MCQ — Level 1

An 8-bit register holds 0xB8 (1011 1000, a 2's-complement number). It is shifted **arithmetically right by 3**. The new contents are

A. 0x17  
B. 0xF7  
C. 0xF6  
D. 0xE8

**Answer:** B

**Solution:** 0xB8 = −72. Arithmetic right shift by 3 replicates the sign bit: 1011 1000 → 1111 0111 = 0xF7 = −9 = −72/8. A (0x17) is the logical shift (and here also a rotate); C is −10 and D is −24, neither equal to −72/8.

**Concept tested:** arithmetic vs logical shift (NOTES §9.2).  
**Difficulty:** Easy.  
**Common trap:** filling with zeros.

---

### Q4 — MSQ — Level 1 (one or more options correct; no partial marking)

A combined adder/subtractor uses a control line M (M = 0 add, M = 1 subtract) and an n-bit adder. Which statements are correct?

A. Each bit of B is XOR-ed with M before entering the adder.  
B. The carry-in of the least significant bit is M.  
C. For M = 1 the circuit computes A + B + 1.  
D. A separate subtractor circuit must exist in addition to the adder.

**Answer:** A, B

**Solution:** B ⊕ M inverts B when M = 1 and the carry-in M adds the +1 of the 2's complement, so A + ~B + 1 = A − B. C is wrong (the circuit adds ~B + 1, not B + 1). D is wrong; the whole point is that one adder serves both.

**Concept tested:** adder/subtractor (NOTES §7.1).  
**Difficulty:** Easy.  
**Common trap:** forgetting the carry-in of 1.

---

## Level 2 — Standard GATE

### Q5 — NAT — Level 2

An n = 100-bit adder uses a carry-lookahead prefix tree built only from gates with at most two inputs. Assume: forming all Pi and Gi takes 1 gate delay; combining two (G, P) pairs takes 2 gate delays (an AND followed by an OR); the carry-in C0 is treated as one more operand of the prefix tree; the final sum bit Si = Pi ⊕ Ci takes 1 gate delay. What is the delay, in gate delays, until the most significant sum bit is ready?

**Answer:** 16

**Solution:** The carry into the MSB (C99) is a prefix over 100 operands (C0 plus the (G, P) of bits 0…98 — at most 100 operands), so the balanced tree has ⌈log₂100⌉ = 7 levels. Total = 1 + 2·7 + 1 = 16 gate delays. (A ripple adder in the same model needs 2n = 200.)

**Concept tested:** fan-in-2 lookahead delay 2 + 2⌈log₂n⌉ (NOTES §5.5).  
**Difficulty:** Medium.  
**Common trap:** using 2n, or counting 100 levels, or using log₂100 without the ceiling.

---

### Q6 — MCQ — Level 2

An 8-bit ALU adds 0xC8 and 0x90. Which pair (C, V) does it produce?

A. C = 0, V = 0  
B. C = 1, V = 0  
C. C = 0, V = 1  
D. C = 1, V = 1

**Answer:** D

**Solution:** 0xC8 + 0x90 = 0x158, so the stored result is 0x58 and the carry-out is C = 1. Carry into the MSB: low 7 bits 0x48 + 0x10 = 0x58 < 0x80 → carry into MSB = 0. V = 0 ⊕ 1 = 1. Sign check: both operands negative (−56 and −112), result 0x58 positive ⇒ signed overflow (−168 < −128). Unsigned 200 + 144 = 344 > 255 also overflows.

**Concept tested:** carry vs overflow (NOTES §7.2).  
**Difficulty:** Medium.  
**Common trap:** assuming C = 1 implies V = 0, or the reverse.

---

### Q7 — MSQ — Level 2 (one or more options correct; no partial marking)

An 8-bit ALU computes A − B for A = 0x90 and B = 0x30 as A + ~B + 1. Which statements are correct?

A. The raw carry-out C is 1.  
B. Treated as signed numbers, A < B.  
C. Treated as unsigned numbers, A < B.  
D. The overflow flag V is 0.

**Answer:** A, B

**Solution:** ~0x30 = 0xCF; 0x90 + 0xCF + 1 = 0x160 → result 0x60, raw C = 1, Z = 0, N = 0. Overflow: A is negative (−112), B positive (48), result positive: different-sign operands and result sign ≠ sign of A ⇒ V = 1. Signed A < B ⟺ N ⊕ V = 0 ⊕ 1 = 1 ✓ (−112 < 48). Unsigned A < B ⟺ raw C = 0, but C = 1 (144 ≥ 48), so C is false. D is false because V = 1.

**Concept tested:** signed vs unsigned comparison from flags (NOTES §7.4–§7.5).  
**Difficulty:** Medium.  
**Common trap:** using N alone (N = 0 would suggest A ≥ B signed).

---

### Q8 — NAT — Level 2

How many addition/subtraction operations does radix-2 Booth's algorithm perform for the 16-bit multiplier 0110 1110 0011 0101 (2's complement)? (Integer.)

**Answer:** 10

**Solution:** Append a 0 on the right of the multiplier and list adjacent pairs of the 17-bit string 0 1 1 0 1 1 1 0 0 0 1 1 0 1 0 1 0. Counting the places where neighbouring bits differ gives 10 changes. Each change is one A−M (start of a run of 1s) or one A+M (just after the end of a run). Cross-check by runs: the multiplier has five runs of 1s (11, 111, 11, 1, 1), each costing one subtraction and one addition: 5 + 5 = 10. The algorithm also performs 16 arithmetic shifts, which are not counted here.

**Concept tested:** Booth operation count (NOTES §10.3).  
**Difficulty:** Medium.  
**Common trap:** counting the 1 bits (which is 9 here) or forgetting the appended 0.

---

### Q9 — NAT — Level 2

A 64-bit barrel shifter has one stage per bit of the shift amount; each stage is a column of 2:1 multiplexers with delay 0.35 ns. Ignoring wire delay, how long (in ns, one decimal place) does a shift by any amount take?

**Answer:** 2.1

**Solution:** 6 stages (log₂64) in series regardless of the shift amount: 6 × 0.35 = 2.1 ns.

**Concept tested:** barrel shifter delay (NOTES §9.3).  
**Difficulty:** Easy–Medium.  
**Common trap:** multiplying by the shift amount.

---

### Q10 — MSQ — Level 2 (one or more options correct; no partial marking)

The arithmetic unit of an 8-bit ALU forms Y from B with a 2-bit select S1S0 (00 → 0, 01 → B, 10 → ~B, 11 → all ones), and outputs A + Y + Cin. Which (S1S0, Cin) combinations produce the stated function?

A. (10, 1) produces A − B.  
B. (11, 0) produces A − 1.  
C. (01, 1) produces A + B.  
D. (00, 0) produces A (transfer).

**Answer:** A, B, D

**Solution:** (10,1): A + ~B + 1 = A − B ✓. (11,0): A + 0xFF = A − 1 (mod 256) ✓. (01,1): A + B + 1, not A + B ✗. (00,0): A + 0 + 0 = A ✓.

**Concept tested:** arithmetic-unit B-conditioning (NOTES §8.3).  
**Difficulty:** Medium.  
**Common trap:** forgetting the extra +1 when Cin = 1.

---

## Level 3 — Multi-step

### Q11 — NAT — Level 3

A sequential 24-bit unsigned shift-and-add multiplier runs at 1.5 GHz. In each of the 24 iterations the shift takes one clock cycle; the addition takes one separate clock cycle and happens only when the current multiplier bit Q0 is 1. The multiplier has nine 1 bits. How long does the multiplication take, in ns? (Integer.)

**Answer:** 22

**Solution:** Cycles = 24 shifts + 9 additions = 33. Clock period = 1/1.5 GHz = 0.667 ns. Time = 33 / 1.5 = 22 ns.

**Concept tested:** shift-add cost (NOTES §10.1).  
**Difficulty:** Medium.  
**Common trap:** charging an addition in every iteration (48 cycles = 32 ns).

---

### Q12 — NAT — Level 3

A 6-bit unsigned restoring divider divides 59 by 4. Every step performs one subtraction; whenever the subtraction result is negative, one more addition restores the previous partial remainder. Assuming the quotient fits in 6 bits, how many add/subtract operations (including restoring additions) are performed in total? (Integer.)

**Answer:** 9

**Solution:** 59 ÷ 4 gives quotient 14 = 001110₂ and remainder 3. The 6 steps each subtract once. A restore happens exactly in the steps whose quotient bit is 0: 001110 has three 0 bits → 3 restores. Total = 6 + 3 = 9. (Simulation: the first two steps and the last step fail and restore.)

**Concept tested:** restoring division operation count (NOTES §11.1).  
**Difficulty:** Medium.  
**Common trap:** counting 2n = 12 operations for every division.

---

### Q13 — NAT — Level 3

A 64-bit adder is built from 4-bit lookahead units arranged in three levels: 4-bit blocks, 16-bit groups of four blocks, and one top-level unit for the four groups. Timing: all Pi and Gi are ready 1 ns after the operands; each lookahead unit needs 2 ns after its inputs to produce either its block (G*, P*) outputs or its carry outputs; a sum bit needs 1 ns after its carry. The adder's carry-in is available at time 0. What is the worst-case time, in ns, until all sum bits are ready? (Integer.)

**Answer:** 12

**Solution:** Timeline of the critical path:

```
t = 1   Pi, Gi
t = 3   block (4-bit) G*, P*
t = 5   group (16-bit) G**, P**
t = 7   top-level unit: carries into each group
t = 9   group-level unit: carries into each 4-bit block
t = 11  block lookahead: carries into each bit
t = 12  sums
```

**Concept tested:** multi-level lookahead timing (NOTES §5.4, 4L formula with L = 3).  
**Difficulty:** Medium.  
**Common trap:** counting only the way up (forgetting the way down) or adding the sum delay twice.

---

### Q14 — MCQ — Level 3

A single-bus data path has PC, MAR, MDR, IR, general registers, an ALU with temporary registers Y (first ALU input from Y, second from the bus) and Z (ALU output). `Xout` places X on the bus; `Xin` latches the bus into X. The instruction `SUB R1, R6, R2` means R1 ← R6 − R2. Memory read takes one step; the PC increment is done by a separate incrementer and is ignored. The five steps are:

(p) `R2out, SUB, Zin`  
(q) `PCout, MARin, Read`  
(r) `R6out, Yin`  
(s) `MDRout, IRin`  
(t) `Zout, R1in`

Which order is correct?

A. q, s, r, p, t  
B. q, s, p, r, t  
C. r, q, s, p, t  
D. q, s, r, t, p

**Answer:** A

**Solution:** Dependencies: q → s (address and read before MDR → IR); s → r, p, t (nothing instruction-specific before IR is loaded); r → p (R6 must already be in Y so the ALU computes Y − bus = R6 − R2); p → t (result is in Z only after the ALU step). The only permutation respecting all edges is q, s, r, p, t (script-enumerated: 1 of 120). B swaps r and p (ALU would use a stale Y). C starts the operand transfer before the instruction is fetched. D writes the destination before the ALU produced the result.

**Concept tested:** register-transfer ordering on a single bus (NOTES §13.2).  
**Difficulty:** Medium.  
**Common trap:** reversing the operands of a non-commutative operation.

---

### Q15 — NAT — Level 3

On the data path of Q14, memory is slower: if `Read` is issued in clock step 1 (with the address in MAR), the data is in MDR at the end of step 3 (so steps 2 and 3 are waiting). Then `MDRout, IRin` takes one step, and the instruction `SUB R3, R4, R5` (R3 ← R4 − R5) takes the three execute steps `R4out, Yin` / `R5out, SUB, Zin` / `Zout, R3in`. How many clock steps does the whole instruction (fetch + execute) take?

**Answer:** 7

**Solution:** Steps 1–3: address and memory read (the read occupies steps 1, 2, 3). Step 4: MDR → IR. Steps 5–7: execute. Total = 3 + 1 + 3 = 7.

**Concept tested:** counting clock steps on a single-bus data path (NOTES §13.2).  
**Difficulty:** Medium.  
**Common trap:** counting the wait steps as zero or adding a separate "decode" step.

---

### Q16 — NAT — Level 3

Radix-2 Booth multiplication with n = 4: multiplicand M = 0101 (+5), multiplier Q = 1101 (−3). Registers A (4 bits, initially 0000), Q, and the extra bit Q−1 (initially 0). Each iteration does the Booth add/subtract according to (Q0, Q−1) and then an arithmetic right shift of A:Q:Q−1. After the **second** iteration (including its shift), what is the 8-bit contents of A:Q interpreted as an **unsigned** integer? (Integer.)

**Answer:** 23

**Solution:**

```
init               A = 0000  Q = 1101  Q−1 = 0
iter 1: (Q0,Q−1) = (1,0) → A ← A − M = 0000 − 0101 = 1011 ; ASR → A = 1101, Q = 1110, Q−1 = 1
iter 2: (Q0,Q−1) = (0,1) → A ← A + M = 1101 + 0101 = 0010 (carry dropped) ; ASR → A = 0001, Q = 0111, Q−1 = 0
A:Q = 0001 0111 = 16 + 4 + 2 + 1 = 23
```

(For completeness the full product after 4 iterations is 1111 0001 = −15 = 5 × −3.)

**Concept tested:** Booth trace (NOTES §10.3, E10.2/E10.3).  
**Difficulty:** Medium.  
**Common trap:** shifting logically instead of arithmetically, or forgetting to update Q−1.

---

## Level 4 — Tricky / trap-based

### Q17 — MSQ — Level 4 (one or more options correct; no partial marking)

An 8-bit ALU performs the following operations on 2's-complement patterns (subtraction as A + ~B + 1; C is the raw carry-out). Which statements are correct?

A. 0x7F − 0xFF sets V = 1.  
B. 0x00 − 0x80 sets V = 1.  
C. 0xFE + 0x02 gives C = 1 and V = 0.  
D. 0x40 + 0x40 gives C = 1.

**Answer:** A, B, C

**Solution:**
* A: 127 − (−1) = 128 > 127. Operands have different signs (0, 1), result 0x80 has sign 1 ≠ sign of A (0) ⇒ V = 1 ✓.
* B: 0 − (−128) = +128 > 127; result 0x80, different-sign operands and result sign 1 ≠ 0 ⇒ V = 1 ✓. (Negating −128 overflows.)
* C: 0xFE + 0x02 = 0x100 → result 0x00, carry-out 1. Signed: −2 + 2 = 0 fits ⇒ V = 0 ✓.
* D: 0x40 + 0x40 = 0x80, no carry-out (C = 0), but V = 1 (64 + 64 = 128 overflows signed). ✗.

**Concept tested:** overflow detection for add and subtract (NOTES §7.2).  
**Difficulty:** Hard.  
**Common trap:** applying the addition rule (same-sign operands) to subtraction.

---

### Q18 — MCQ — Level 4

A compiler replaces `x / 4` by an arithmetic right shift by 2 for an 8-bit signed variable x = −25 (0xE7). What signed value does the shift produce?

A. −6  
B. −7  
C. 57  
D. −25

**Answer:** B

**Solution:** 0xE7 = 1110 0111. ASR 2 → 1111 1001 = 0xF9 = −7 = ⌊−25/4⌋ = ⌊−6.25⌋. Truncating division would give −6 (A), so the shift differs from C-style division for negative non-multiples of 4. C (57 = 0x39) is the logical shift. D is unchanged x.

**Concept tested:** arithmetic shift rounds toward −∞ (NOTES §9.2).  
**Difficulty:** Medium–Hard.  
**Common trap:** assuming shift = truncating division.

---

### Q19 — MCQ — Level 4

On a processor the carry flag after a compare (subtraction A − B) is defined as a **borrow**: C = 1 exactly when the unsigned subtraction needed a borrow (C = NOT of the raw adder carry-out). Z is the zero flag. Which condition means "unsigned A ≤ B"?

A. C = 1 and Z = 0  
B. C = 1 or Z = 1  
C. C = 0 or Z = 1  
D. (N ⊕ V) = 1 or Z = 1

**Answer:** B

**Solution:** With a borrow flag, A < B ⟺ C = 1, and A = B ⟺ Z = 1, so A ≤ B ⟺ C = 1 or Z = 1 (B). A describes strictly A < B (it fails for A = B). C is the raw-carry-style condition "no borrow, or equal": for A = 200, B = 10 it holds (C = 0) although A > B. D is the signed ≤ condition: for A = 0x90, B = 0x30 it holds (signed −112 ≤ 48) but unsigned 144 ≤ 48 is false.

**Concept tested:** borrow vs raw-carry convention and branch conditions (NOTES §7.4–§7.5).  
**Difficulty:** Medium–Hard.  
**Common trap:** using the raw-carry condition (C = 0) while the question defines a borrow flag.

---

### Q20 — NAT — Level 4

In IEEE 754 single precision let a = 2²⁵ and b = 2. Evaluate s₁ = (a + b) + b and s₂ = a + (b + b), each addition rounded to nearest-even in single precision. Compute s₂ − s₁. (Integer.)

**Answer:** 4

**Solution:** Near 2²⁵ the spacing between single-precision numbers is 2^(25−23) = 4. a + b = 2²⁵ + 2 is exactly halfway between 2²⁵ and 2²⁵ + 4; ties go to the even significand, which is 2²⁵ (fraction all zeros). So a + b = 2²⁵, and adding b again gives 2²⁵ again: s₁ = 2²⁵. Meanwhile b + b = 4 and 2²⁵ + 4 is representable: s₂ = 2²⁵ + 4. Difference = 4.

**Concept tested:** non-associativity of floating-point addition (NOTES §12.3).  
**Difficulty:** Hard.  
**Common trap:** treating float addition like exact arithmetic (difference 0).

---

### Q21 — MCQ — Level 4

In single precision, x = 1.5 × 2¹² and y = 1.5 × 2⁻¹². The sum x + y is computed by an IEEE-754 adder (align, add, round to nearest-even). The result is

A. x  
B. x + 2⁻¹¹  
C. x + 1.5 × 2⁻¹² (exact sum)  
D. x + 2⁻¹²

**Answer:** B

**Solution:** ulp(x) = 2^(12 − 23) = 2⁻¹¹. y = 1.5·2⁻¹² = 0.75·ulp, which is more than half an ulp, so the aligned operand rounds up to one full ulp: x + 2⁻¹¹. A would be correct for y ≤ half an ulp (a tie at exactly half goes to even). C is not representable, and D is half an ulp (not representable either).

**Concept tested:** alignment and rounding in FP add (NOTES §12.1).  
**Difficulty:** Hard.  
**Common trap:** assuming "small addend vanishes" without comparing it with half an ulp.

---

## Level 5 — Challenge

### Q22 — NAT — Level 5

Counting argument: any adder circuit made only of gates with at most two inputs must have depth at least ⌈log₂(number of inputs the top sum bit depends on)⌉. For a 1000-bit adder (inputs A, B and the carry-in C0), what is this lower bound on the depth for the most significant sum bit? (Integer.)

**Answer:** 11

**Solution:** The top sum bit depends on 2·1000 + 1 = 2001 inputs. A depth-d tree of 2-input gates can depend on at most 2ᵈ inputs, so 2ᵈ ≥ 2001. 2¹⁰ = 1024 < 2001 ≤ 2048 = 2¹¹ ⇒ d ≥ 11. (The prefix adder of NOTES §5.5 uses 2 + 2·⌈log₂1000⌉ = 22, within a factor 2 of this bound; both are Θ(log n).)

**Concept tested:** Ω(log n) lower bound (NOTES §5.5).  
**Difficulty:** Hard.  
**Common trap:** using n instead of 2n + 1 inputs.

---

### Q23 — NAT — Level 5

For the 16-bit 2's-complement multiplier 0101 1101 0010 1100, how many **fewer** add/subtract operations does radix-4 (bit-pair, modified) Booth recoding need than radix-2 Booth? (Integer; count a digit 0 as no operation.)

**Answer:** 3

**Solution:** Radix-2: append 0 and count bit changes → 10 operations. Radix-4: groups (q(2i+1) q(2i) q(2i−1)) from the LSB give digits (low group first) 0, −1, −1, +1, +1, −1, +2, +1. Check: 0·4⁰ − 1·4¹ − 1·4² + 1·4³ + 1·4⁴ − 1·4⁵ + 2·4⁶ + 1·4⁷ = −4 − 16 + 64 + 256 − 1024 + 8192 + 16384 = 23852 = 0x5D2C ✓. The first digit (group i = 0) is 0, so there are 7 non-zero digits. Difference = 10 − 7 = 3.

**Concept tested:** radix-4 Booth recoding (NOTES §10.4).  
**Difficulty:** Hard.  
**Common trap:** thinking radix-4 always has exactly n/2 operations (zero digits need none).

---

### Q24 — NAT — Level 5

A 28-bit carry-select adder uses ripple-carry blocks of sizes 4, 5, 7 and 12 bits (least significant block first). A ripple block of s bits needs s ns to produce its carry-out and its sums; the multiplexer that selects between the two precomputed results needs 1.5 ns after the select (carry) arrives. The first block uses the real carry-in (available at time 0); every other block computes both cases in parallel from time 0. When is the last sum bit ready, in ns (one decimal place)?

**Answer:** 13.5

**Solution:** Block ready times (both versions): 4, 5, 7, 12. Carries: C4 = 4 (first block, real carry-in). C9 = max(5, 4) + 1.5 = 6.5. C16 = max(7, 6.5) + 1.5 = 8.5. The last block's results are ready at 12 but its select arrives at 8.5, so its output is available at max(12, 8.5) + 1.5 = 13.5 ns. Compare: pure ripple 28 ns; seven equal blocks of 4 give 4 + 6·1.5 = 13 ns — an unbalanced big last block loses to its own ripple delay.

**Concept tested:** carry-select timing with unequal blocks (NOTES §6.1).  
**Difficulty:** Hard.  
**Common trap:** using the equal-block formula b·t_c + (k − 1)·t_m instead of tracing max(ready, carry).
