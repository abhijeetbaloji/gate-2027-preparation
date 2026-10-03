# Microprogrammed Control — Practice

Original questions (not from any GATE paper, and different from the questions in the repository's separate practice file). Answers directly under each question. Theory: [NOTES.md](NOTES.md). Conventions: 1 K = 2¹⁰; widths in bits; "Mini-1" is the reference machine of NOTES Section 4.

---

## Level 1 — Conceptual

### Q1 — MCQ — Level 1

Which register holds the control-store address of the microinstruction that is currently being read?

A. Instruction register (IR)  
B. Memory address register (MAR)  
C. Control address register / micro-PC  
D. Program counter (PC)

**Answer:** C

**Solution:** The micro-PC (CAR) addresses the *control store*. PC addresses the next machine instruction in main memory; MAR addresses main memory; IR holds the current machine instruction (its opcode is used to *find* the starting microaddress, but it is not the control-store address register).

**Concept tested:** CAR vs PC/MAR/IR.

**Difficulty:** Easy

**Common trap:** Choosing PC because "program counter" sounds right.

---

### Q2 — MSQ — Level 1

One or more options are correct. Select all that apply (no partial marking).

A. A single microinstruction may specify several micro-operations that happen in the same step.  
B. A micro-operation and a machine instruction are the same thing.  
C. The control data register (microinstruction register) holds the microinstruction currently being executed.  
D. Vertical microinstructions never need a decoder.

**Answer:** A, C

**Solution:** A is true (a microinstruction asserts a set of compatible control signals). B is false: a machine instruction is implemented by a *sequence* of microinstructions, each doing one or more micro-operations. C is true: CAR → control store → CDR. D is false: vertical (encoded) fields must be decoded into individual control signals.

**Concept tested:** Terminology.

**Difficulty:** Easy

**Common trap:** Mixing micro-operation, microinstruction and machine instruction.

---

### Q3 — NAT — Level 1

A control store contains 1000 microinstructions. What is the minimum number of bits in the control address register? (Integer.)

**Answer:** 10

**Solution:** ⌈log₂ 1000⌉: 2⁹ = 512 < 1000 ≤ 1024 = 2¹⁰, so 10 bits.

**Concept tested:** CAR width = ⌈log₂ N⌉.

**Difficulty:** Easy

**Common trap:** Using 9 (⌊log₂⌋) or 1000/8.

---

## Level 2 — Standard GATE style

### Q4 — MCQ — Level 2

In a microprogrammed CPU every instruction starts with the same fetch microroutine. How does control normally enter the microroutine of the specific instruction that was fetched?

A. The control address register is loaded with a start address derived from the opcode in IR (mapping ROM or opcode bits).  
B. The control address register is reset to zero and the user program supplies the next address.  
C. The ALU computes the next microinstruction address from the operands.  
D. The fetch routine is replicated at the start of every execute routine, so no mapping is needed.

**Answer:** A

**Solution:** After IR holds the opcode, the sequencer's MAP mode forms the start address (via a mapping ROM, or by concatenating/shifting opcode bits). B and C do not describe any control mechanism. D is wrong: fetch is stored once and shared (that is the point of sharing), and replication would not select the routine anyway.

**Concept tested:** Shared fetch; opcode-to-start-address mapping.

**Difficulty:** Easy

**Common trap:** Thinking the fetch routine is repeated per instruction.

---

### Q5 — NAT — Level 2

A horizontal control word has one bit per control signal for 36 control signals, a 3-bit condition-select field, and a 10-bit absolute next-address field. There are no other fields. What is the word width in bits?

**Answer:** 49

**Solution:** 36 + 3 + 10 = 49 bits.

**Concept tested:** Horizontal word width includes sequencing fields.

**Difficulty:** Easy

**Common trap:** Answering 36 (signals only).

---

### Q6 — MCQ — Level 2

A group of 16 control signals is such that at most one is asserted per microinstruction, and a microinstruction may assert none of them. The minimum number of bits to encode this group in one field is

A. 4  
B. 5  
C. 16  
D. 17

**Answer:** B

**Solution:** Codes needed = 16 signals + 1 "none" = 17. 2⁴ = 16 < 17 ≤ 32 = 2⁵, so 5 bits. A (4 bits) fails because 16 codes cannot also represent "none". C is the horizontal cost. D is the number of codes, not bits.

**Concept tested:** ⌈log₂ (n+1)⌉ with the power-of-two trap.

**Difficulty:** Easy–Medium

**Common trap:** Answering 4 because log₂ 16 = 4.

---

### Q7 — NAT — Level 2

The shared fetch routine has 4 microinstructions. Six instructions have execute routines of 3, 5, 4, 6, 2 and 7 microinstructions. Every microinstruction is 22 bits wide. How many bits does the control store contain? (Count only the microinstructions.)

**Answer:** 682

**Solution:** N = 4 + (3 + 5 + 4 + 6 + 2 + 7) = 4 + 27 = 31 words. Bits = 31 × 22 = 682.

**Concept tested:** Shared fetch counted once; N × W.

**Difficulty:** Easy–Medium

**Common trap:** Adding the fetch routine to every instruction (6 × 4 + 27 = 51 words).

---

### Q8 — MCQ — Level 2

A machine has a 5-bit opcode. The starting microaddress of an instruction's routine is formed as `opcode ‖ step`, where `step` is a 3-bit field that the micro-PC increments from 000. What is the largest number of microinstructions an instruction's routine can contain without jumping to a continuation elsewhere?

A. 3  
B. 5  
C. 8  
D. 32

**Answer:** C

**Solution:** The step field has 3 bits, so each opcode owns 2³ = 8 consecutive words (steps 000–111). Total routine address space = 2⁸ = 256 words, with 32 blocks of 8 (D is the number of blocks, not the routine length).

**Concept tested:** Concatenated-opcode layout; fixed block size.

**Difficulty:** Medium

**Common trap:** Confusing block count (32) with block size (8).

---

### Q9 — MCQ — Level 2

A single-bus Mini-1-style datapath has these candidate microinstructions for `ADDM R1, addr` (R1 ← R1 + M[addr]; A, T, MDR, MAR as in NOTES Section 4; memory data is valid in MDR in the step after `Read`). Which one is **not** a legal single-bus microinstruction?

A. `IRout, MARin, Read`  
B. `R1out, Ain`  
C. `MDRout, R1out, ADD, Tin`  
D. `Tout, R1in`

**Answer:** C

**Solution:** C asks two different registers (MDR and R1) to drive the single internal bus in the same step. A, B and D each use one bus source. The correct pair of steps for the add would be `MDRout, ADD, Tin` (A already holds R1 from step B), then `Tout, R1in`.

**Concept tested:** Bus-conflict legality when reading a micro-operation listing.

**Difficulty:** Medium

**Common trap:** Checking only the data dependency and not the one-source-per-step rule.

---

## Level 3 — Multi-step

### Q10 — NAT — Level 3

A control word is designed with these fields. In a horizontal version the same information is kept as one bit per signal, with the condition-select and next-address fields unchanged.

| Field | Alternatives | Rule |
|---|---|---|
| Bus source | 12 signals | at most one asserted, none allowed |
| Bus destination | 12 signals | at most one asserted, none allowed |
| ALU function | 7 functions | at most one asserted, none allowed |
| Memory | read, write | at most one, none allowed |
| Flag controls | 6 signals | may be asserted together |
| Condition select | 5 conditions plus unconditional | encoded |
| Next address | absolute | 400 control-store words |

The control store has 400 words. How many bits does the encoded design save compared with the horizontal design? (Integer.)

**Answer:** 8000

**Solution:**
- Encoded groups: ⌈log₂ 13⌉ = 4 (bus source), 4 (destination), ⌈log₂ 8⌉ = 3 (ALU), ⌈log₂ 3⌉ = 2 (memory); flags stay 6 bits.
- Condition select: ⌈log₂ (5 + 1)⌉ = 3. Next address: ⌈log₂ 400⌉ = 9.
- W_encoded = 4 + 4 + 3 + 2 + 6 + 3 + 9 = 31 bits.
- W_horizontal = 12 + 12 + 7 + 2 + 6 + 3 + 9 = 51 bits.
- Saving = 400 × (51 − 31) = 400 × 20 = 8000 bits (12 400 vs 20 400).

**Concept tested:** Field-encoded width, savings.

**Difficulty:** Medium

**Common trap:** Forgetting the "none" code. It does not change the 12-signal groups (⌈log₂ 12⌉ is also 4) or the 7-function ALU group (⌈log₂ 7⌉ is also 3), but it does change the memory field: ⌈log₂ 2⌉ = 1 would be wrong, it needs 2 bits. Another trap is re-encoding the six flag controls, which may be asserted together.

---

### Q11 — NAT — Level 3

Each microcycle of a microprogrammed CPU consists of a 12 ns control-store read, a 3 ns decode and a 15 ns datapath operation, in sequence (no overlap). An instruction executes 7 microinstructions (fetch included). How long does the instruction take, in ns?

**Answer:** 210

**Solution:** t_µ = 12 + 3 + 15 = 30 ns. 7 × 30 = 210 ns.

**Concept tested:** Non-overlapped microcycle.

**Difficulty:** Easy–Medium

**Common trap:** Using only the 12 ns access time.

---

### Q12 — NAT — Level 3

The same CPU as Q11 (12 ns read, 3 ns decode, 15 ns datapath) now latches each microinstruction in the CDR so that the next control-store read overlaps the current decode + datapath work. The instruction executes 7 microinstructions, two of which are taken jumps; each taken jump wastes exactly one extra microcycle (the prefetched word is discarded). How long does the instruction take, in ns?

**Answer:** 162

**Solution:** Overlapped microcycle t_µ = max(12, 3 + 15) = max(12, 18) = 18 ns. Cycles = 7 + 2 wasted = 9. Time = 9 × 18 = 162 ns.

**Concept tested:** Overlapped microcycle and branch penalty.

**Difficulty:** Medium

**Common trap:** Using 30 ns, or forgetting the wasted cycles (7 × 18 = 126 ns).

---

### Q13 — NAT — Level 3

On a microprogrammed CPU each microinstruction takes one 20 ns clock. Instruction mix and microinstructions per instruction (fetch included): ALU 40 % → 5, load 30 % → 7, store 20 % → 6, branch 10 % → 4. What is the average time per instruction in ns? (One decimal place.)

**Answer:** 114.0

**Solution:** CPI = 0.4×5 + 0.3×7 + 0.2×6 + 0.1×4 = 2.0 + 2.1 + 1.2 + 0.4 = 5.7 microcycles. Time = 5.7 × 20 = 114.0 ns.

**Concept tested:** CPI from microinstruction counts.

**Difficulty:** Medium

**Common trap:** Forgetting to multiply by the clock period (answer 5.7).

---

### Q14 — NAT — Level 3

A flat horizontal control store has 1024 microinstructions of 72 bits each. Only 120 distinct 72-bit control patterns occur. A two-level design stores each distinct pattern once in a nanostore and keeps only the minimum-width pointer in each microinstruction (ignore sequencing bits). How many bits are needed in total for the two-level design? (Integer.)

**Answer:** 15808

**Solution:** p = ⌈log₂ 120⌉ = 7 (2⁶ = 64 < 120 ≤ 128). Micro level = 1024 × 7 = 7168 bits. Nanostore = 120 × 72 = 8640 bits. Total = 7168 + 8640 = 15 808 bits (flat design 73 728 bits, saving 57 920).

**Concept tested:** Nanoprogramming storage.

**Difficulty:** Medium

**Common trap:** Forgetting the nanostore term, or using 120 bits as the pointer.

---

### Q15 — NAT — Level 3

Eight machine instructions each need the same 4-step operand-address computation. Option 1 repeats it inline in each routine. Option 2 stores it once as a microsubroutine whose last word returns, and each instruction uses one extra microinstruction to call it. How many control-store words does Option 2 save compared with Option 1?

**Answer:** 20

**Solution:** Inline = 8 × 4 = 32 words. Shared = 4 + 8 call words = 12 words. Saving = 20 words. (Cost: one extra microcycle per execution for the call word, assuming it does no datapath work.)

**Concept tested:** Microsubroutine sharing.

**Difficulty:** Medium

**Common trap:** Forgetting the call words (32 − 4 = 28).

---

## Level 4 — Tricky / trap-based

### Q16 — NAT — Level 4

Six control signals P, Q, R, S, T, U must be encoded into mutually exclusive fields (each field may also assert none). In the microprogram, the following pairs of signals are asserted together in some microinstruction: P&S, Q&S, R&T, P&U, Q&T, R&U. No other pair is ever asserted together. What is the minimum total number of encoded bits, counting each field as ⌈log₂ (size + 1)⌉? (Partition the signals into fields of mutually compatible signals.)

**Answer:** 4

**Solution:** Conflict graph edges: P–S, Q–S, R–T, P–U, Q–T, R–U. It is a 6-cycle (P–S–Q–T–R–U–P), so it is 2-colourable: {P, Q, R} and {S, T, U} are independent sets. Each group of 3 + none = 4 codes → 2 bits; total 2 + 2 = 4 bits. Other partitions: 3+2+1 → 2 + 2 + 1 = 5; 2+2+2 → 6 (no better). Horizontal would use 6.

**Concept tested:** Choosing field groups from simultaneity constraints.

**Difficulty:** Hard

**Common trap:** Using ⌈log₂ 7⌉ = 3 by treating all six signals as one field (illegal, because pairs must be asserted together).

---

### Q17 — MSQ — Level 4

One or more options are correct. Select all that apply (no partial marking).

A. Nanoprogramming reduces total storage when many microinstructions use the same wide control pattern.  
B. Each microinstruction in a two-level scheme needs a second memory access (to the nanostore), so the microcycle tends to lengthen.  
C. For D distinct patterns the microstore pointer needs ⌈log₂ D⌉ bits.  
D. Nanoprogramming always reduces total storage, even if every microinstruction has a distinct pattern.

**Answer:** A, B, C

**Solution:** A, B, C hold. D is false: if D ≈ M the pointer bits are pure overhead: two-level = M·p + D·W exceeds M·W (e.g. M = 512, W = 60, D = 500 gives 34 608 > 30 720).

**Concept tested:** When nanoprogramming helps; its time cost.

**Difficulty:** Medium

**Common trap:** Believing a second level always saves space.

---

### Q18 — MCQ — Level 4

A branch microinstruction can test any one of 8 status conditions, or branch unconditionally, using a single encoded condition-select field. Minimum width of that field?

A. 3  
B. 4  
C. 8  
D. 9

**Answer:** B

**Solution:** Alternatives = 8 conditions + 1 "unconditional" = 9 codes. 2³ = 8 < 9 ≤ 16, so 4 bits. A fails to represent "unconditional". C and D are code counts or unencoded widths.

**Concept tested:** Condition-select field width with an "always" code.

**Difficulty:** Medium

**Common trap:** Answering ⌈log₂ 8⌉ = 3.

---

### Q19 — NAT — Level 4

A microprogram uses 20 signal bits, a 3-bit condition select, and an 8-bit next-address field. Design X gives every control-store word all three fields (31 bits). Design Y uses a variable format: a 1-bit type flag, and the remaining bits hold either the 20 signal bits (operate word, next = CAR + 1) or the condition select + address (branch word); all ROM words have the same width. Assume both designs need 200 words (idealised, stated for this question). How many bits does Y save over X?

**Answer:** 2000

**Solution:** Y width = 1 + max(20, 3 + 8) = 21 bits. X width = 20 + 3 + 8 = 31. Saving per word = 10. Total = 200 × 10 = 2000 bits. (In real designs Y needs more words for branch-only microinstructions, which erodes the saving.)

**Concept tested:** Variable-format sequencing.

**Difficulty:** Medium–Hard

**Common trap:** Using 20 + 11 + 1 = 32 for Y, or forgetting the max().

---

## Level 5 — Challenge

### Q20 — NAT — Level 5

A CPU has a 6-bit opcode field (64 possible opcode values). Each instruction's execute routine has at most 6 microinstructions; the shared fetch routine fits in an otherwise unused opcode block. The signal part of a microinstruction is 20 bits; the next-address field has as many bits as the control-store address.

Design 1: start address = `opcode ‖ step(3 bits)`; the whole address space is built as control store.  
Design 2: a dense control store of 150 words (fetch included) plus a mapping ROM that has one entry per possible opcode value (64 entries), each entry as wide as the control-store address.

How many more ROM bits does Design 1 use than Design 2? (Count the control store and the mapping ROM.)

**Answer:** 10136

**Solution:**
- Design 1: address = 6 + 3 = 9 bits → 2⁹ = 512 words. Word = 20 + 9 = 29 bits. Bits = 512 × 29 = 14 848.
- Design 2: CAR = ⌈log₂ 150⌉ = 8 (128 < 150 ≤ 256). Word = 20 + 8 = 28 bits. Control store = 150 × 28 = 4200. Mapping ROM = 64 × 8 = 512. Total = 4712.
- Difference = 14 848 − 4712 = 10 136 bits.

**Concept tested:** Mapping ROM vs concatenation layout cost; the next-address width follows N.

**Difficulty:** Hard

**Common trap:** Using the same word width (29) for both designs, or omitting the mapping ROM.

---

### Q21 — NAT — Level 5

Two implementations of the same instruction set: Horizontal needs 300 microinstructions of 56 bits and an average of 6 microinstructions per machine instruction, with a 20 ns microcycle. Vertical needs 410 microinstructions of 31 bits and an average of 9 microinstructions per machine instruction (more, since each word does less), with a 24 ns microcycle (it includes decode). What is the ratio (average control time per machine instruction of Vertical) / (that of Horizontal)? (One decimal place.)

**Answer:** 1.8

**Solution:** Horizontal: 6 × 20 = 120 ns. Vertical: 9 × 24 = 216 ns. Ratio = 216 / 120 = 1.8. (Storage: 300 × 56 = 16 800 vs 410 × 31 = 12 710 bits, so vertical is smaller in bits but slower. The store sizes are not needed for the ratio.)

**Concept tested:** Speed/size trade-off, not "just a narrower word".

**Difficulty:** Medium–Hard

**Common trap:** Comparing only 24/20 = 1.2 and forgetting the longer microprograms.

---

### Q22 — NAT — Level 5

A machine-instruction `MULN` uses this microroutine (after the shared 3-word fetch). Addresses 40–45 hold:

```
 40 : CNT ← IR.count                       next = +1
 41 : A ← 0                                next = +1
 42 : T ← A + R2                           next = +1
 43 : A ← T                                next = +1
 44 : CNT ← CNT − 1                        if CNT ≠ 0 JUMP 42 else +1      (test uses the decremented value)
 45 : R1 ← A                               JUMP 0 (fetch)
```

`IR.count` = 7. Each microinstruction takes 15 ns. How long, in ns, does one execution of MULN (fetch included) take? (Integer.)

**Answer:** 405

**Solution:** Fetch = 3; words 40 and 41 = 2; loop body 42, 43, 44 = 3 words per pass. With count 7 the decrement test exits after the 7th pass (CNT becomes 0), so 7 passes = 21. Word 45 = 1. Total = 3 + 2 + 21 + 1 = 27 microinstructions. Time = 27 × 15 = 405 ns.

**Concept tested:** Tracing a looping microroutine; test after decrement.

**Difficulty:** Hard

**Common trap:** Counting 6 or 8 passes, or leaving out the fetch.
