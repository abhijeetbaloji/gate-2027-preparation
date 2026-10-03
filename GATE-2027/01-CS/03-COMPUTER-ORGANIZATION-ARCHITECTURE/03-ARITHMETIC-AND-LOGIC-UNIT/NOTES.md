# Arithmetic and Logic Unit (ALU) — Complete Notes

Syllabus line: "Design of arithmetic and logic unit (ALU)" (Computer Organization and Architecture).

All numeric examples in this file were recomputed by a script (`/tmp/coa-verify-alu.py`, outside the repo). The PYQ mapping lists no verified answers; this file therefore teaches methods and never states an official answer for a real past question.

---

## 0. Where this fits

| | |
|---|---|
| **Prerequisites** | Binary, hex, Boolean algebra, XOR/AND/OR gates, multiplexers; number representation (sign-magnitude, 1's and 2's complement, IEEE 754) in [../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC) |
| **This topic gives you** | How the processor actually adds, subtracts, compares, shifts, multiplies, divides; what the status flags mean; why a fast adder is Θ(log n) and a ripple adder Θ(n); how a single-bus data path sequences register transfers |
| **Needed by** | [../01-INSTRUCTION-SET](../01-INSTRUCTION-SET) (condition codes, branches), [../02-ADDRESSING-MODES](../02-ADDRESSING-MODES) (effective-address arithmetic), [../04-DESIGN-OF-CONTROL-UNIT](../04-DESIGN-OF-CONTROL-UNIT) (each data-path step becomes a control word), [../07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING) (the EX stage is this ALU; its delay sets the clock) |

### Conventions used in this file

* 1 K = 2¹⁰ etc. (binary prefixes); not needed much here, but stated for consistency.
* **Gate-delay model (GD)** unless a question gives its own numbers: every 2-input AND/OR/XOR gate costs 1 gate delay; wires cost 0. A multi-input AND/OR gate ("unbounded fan-in") also costs 1 delay *only when the question says so* (the classical textbook CLA assumption). **Fan-in 2** means every gate has at most two inputs, so a k-input AND needs ⌈log₂k⌉ levels.
* Bit positions are numbered from 0 (LSB). `Ci` is the carry **into** bit i; `C(i+1)` is the carry **out of** bit i.
* "ALU flags": Z (zero), N (negative/sign, = result MSB), C (carry), V (signed overflow). Different processors define C after a *subtraction* differently; both conventions are explained in §7.4.

---

## 1. Evidence snapshot (why each section has the depth it has)

Counts are of entries in the mapping file `13-PYQ-TOPIC-MAPPING/.../03-ARITHMETIC-AND-LOGIC-UNIT/questions.md`: **3 mapped entries**, of which 2 are genuinely about the ALU/data path (2016 carry-lookahead delay; 2020 single-bus register-transfer ordering) and 1 is an addressing-mode question (2008, auto-increment) that is misfiled here. ALU-skill questions that GATE actually asks live mostly in the *Digital Logic* mapping (overflow detection, Booth, ripple-carry latency, shifts as multiplication, floating point); see `PYQ.md`. The existing practice file (14 questions) drives the arithmetic/flags/CLA-timing/compare-by-flags depth.

| Section | Priority | Reason (evidence) |
|---|---|---|
| §2 Signed-number bridge | MEDIUM | Prerequisite for flags/overflow questions and for every practice problem that uses 2's complement |
| §3–§4 Adders, ripple delay | HIGH | Practice Q1, Q3, Q5; ripple-adder latency is a recurring GATE idea (mapped under Digital Logic) |
| §5 Carry lookahead and its Θ-analysis | **HIGH** | Mapped PYQ (2016 CS-1) tests exactly the fan-in-2 asymptotics; practice Q13 is two-level CLA timing |
| §6 Carry-select / carry-skip | MEDIUM | Needed to rule out wrong asymptotic options (Θ(√n)); not directly in PYQ list |
| §7 Adder/subtractor, overflow, carry vs borrow | **HIGH** | Practice Q4, Q6, Q8, Q10, Q12; several overflow PYQs in the Digital Logic mapping |
| §7.5 Flags and branches, signed vs unsigned compare | HIGH | Practice Q2, Q14 |
| §8 ALU organisation (function select) | MEDIUM | Practice Q7, Q9; syllabus line is literally "design of ALU" |
| §9 Shifter and barrel shifter | MEDIUM | Shifts as ×2ᵏ / ÷2ᵏ appears in the Digital Logic mapping (2010); syllabus scope guidance |
| §10 Multiplication (shift-add, Booth) | HIGH | Practice Q11; Booth add/sub counting is a mapped Digital Logic NAT |
| §11 Division | LOW–MEDIUM | Scope guidance; no mapped entry; stays as theory-plus-trace |
| §12 Floating-point at ALU level | MEDIUM | Floating point questions are common but live in the Digital Logic folder; only ALU steps here |
| §13 Single-bus data path | **HIGH** | Mapped PYQ (2020 Q4) is a data-path ordering question; feeds the control-unit topic |

---

## 2. Prerequisite / bridge: signed integers in one page

> Full treatment: [../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/01-FIXED-POINT). This is only what the ALU sections need.

n-bit ranges:

```
unsigned           0 .. 2ⁿ − 1
sign-magnitude     −(2ⁿ⁻¹ − 1) .. +(2ⁿ⁻¹ − 1)     two zeros (+0, −0)
1's complement     −(2ⁿ⁻¹ − 1) .. +(2ⁿ⁻¹ − 1)     two zeros
2's complement     −2ⁿ⁻¹ .. 2ⁿ⁻¹ − 1               one zero; one extra negative number
8-bit example:     unsigned 0..255   2's compl −128..127   sign-mag −127..127
```

Value of an n-bit 2's-complement pattern b(n−1)…b0 is `−b(n−1)·2ⁿ⁻¹ + Σ b(i)·2ⁱ`.

**Negation.** −x = invert all bits, add 1. Algebraically ~x = (2ⁿ − 1) − x, so ~x + 1 = 2ⁿ − x ≡ −x (mod 2ⁿ).

**Why one adder serves unsigned and signed.** An n-bit adder computes (a + b) mod 2ⁿ. The bit pattern of a signed value s is s mod 2ⁿ, so adding patterns gives the pattern of (s₁ + s₂) mod 2ⁿ. The sum is *correct* exactly when the true sum lies in the representable range; otherwise the stored pattern is the true sum wrapped by ±2ⁿ. Subtraction a − b = a + (2ⁿ − b) mod 2ⁿ = a + ~b + 1. Hardware never needs a separate subtractor; only the *interpretation* (and the flag used to detect wrap-around) differs between unsigned and signed.

**Sign extension.** To widen a 2's-complement number, replicate the MSB: −2ⁿ⁻¹ = −2ⁿ + 2ⁿ⁻¹, so adding a leading 1 bit adds −2ⁿ at position n and +2ⁿ⁻¹ at position n−1, which cancel for a number whose bit n−1 was 1. Example: 4-bit 1010 (−6) → 8-bit `1111 1010` (0xFA = −6). Zero extension (leading 0s) is for unsigned.

**Sign-magnitude addition** is not a plain binary add (it compares signs and magnitudes); its overflow is the carry out of the *magnitude* adder. That is why 2's complement is used for integer ALUs.

---

## 3. Building blocks: half adder and full adder

### 3.1 Half adder (HA)

Adds two bits, no carry-in.

```
sum   S = A ⊕ B
carry C = A · B
```

### 3.2 Full adder (FA)

Adds A, B and carry-in Cin.

```
 A B Cin | S Cout
 0 0 0   | 0 0
 0 0 1   | 1 0
 0 1 0   | 1 0
 0 1 1   | 0 1
 1 0 0   | 1 0
 1 0 1   | 0 1
 1 1 0   | 0 1
 1 1 1   | 1 1

S    = A ⊕ B ⊕ Cin          (1 when an odd number of inputs are 1)
Cout = A·B + B·Cin + A·Cin   (majority function)
     = A·B + Cin·(A ⊕ B)     ← the form used by lookahead
```

Define for every bit position

```
Gi = Ai · Bi        generate  : this bit creates a carry by itself
Pi = Ai ⊕ Bi        propagate : this bit passes an incoming carry on
(Ti = Ai + Bi, "transmit", also works for the carry equation but not for the sum)

C(i+1) = Gi + Pi · Ci
Si     = Pi ⊕ Ci
```

Why `Cout = G + P·Cin`: a carry leaves bit i if both inputs are 1 (generate) or if exactly one input is 1 *and* a carry arrives (propagate). If neither input is 1 the carry is killed.

An FA is two HAs plus an OR gate. An n-bit adder uses n full adders (the LSB can use a half adder only if there is never a carry-in; adder/subtractor designs need a full adder at bit 0 because Cin = M).

---

## 4. Ripple-carry adder (RCA)

```
 A3 B3    A2 B2    A1 B1    A0 B0
  │  │     │  │     │  │     │  │
 ┌▼──▼┐   ┌▼──▼┐   ┌▼──▼┐   ┌▼──▼┐
 │FA3 │◄──│FA2 │◄──│FA1 │◄──│FA0 │◄── C0
 └─┬──┘C3 └─┬──┘C2 └─┬──┘C1 └─┬──┘
  S3  ▲     S2       S1       S0
      └── C4 out of bit 3 (carry out of the 4-bit adder)
```

Each carry is waiting for the one before it, so the delay is the length of the carry chain:

```
T_ripple ≈ (n − 1)·t_carry + t_sum          (MSB sum waits for C(n−1))
T_ripple ≈ n·t_carry                         (if you want the carry-out C(n))
```

Worked example E4.1 (number from model GD). With `P,G` formed in 1 delay, each carry stage `G + P·C` = AND then OR = 2 delays, and the sum XOR = 1 delay, the MSB sum of an n-bit adder is ready at

```
T = 1 + 2(n − 1) + 1 = 2n
n = 16 → 32 gate delays      n = 32 → 64 gate delays      n = 24 → 48 gate delays
```

If a question instead gives "carry in 2 ns per stage, sum 3 ns", use *its* numbers: delay = (n − 1)·2 + 3 for the MSB sum (practice Q5 style).

### 4.1 Worst-case input for a ripple adder

The delay of a ripple adder depends on the data. A carry is **generated** at bit i when Ai = Bi = 1, and then **propagates** through each higher bit j with Aj ⊕ Bj = 1. The longest chain starts at a generate and runs to the MSB.

For a fixed A, a generate can only start at a position where A has a 1, so the longest chain starts at the **lowest set bit** of A. To make every higher bit propagate, B must be the complement of A above that bit, which is exactly what B = −A (2's complement) gives.

Worked example E4.2 (8-bit, A = 3 = 0000 0011): choose B = −3 = 1111 1101.

```
bit : 7 6 5 4 3 2 1 0
A   : 0 0 0 0 0 0 1 1
B   : 1 1 1 1 1 1 0 1
bit0: 1+1 → generate (carry 1)
bit1: A⊕B = 1 → propagate
bit2..7: A⊕B = 1 → propagate      chain length 8; sum = 0000 0000, carry-out 1
```

For A = 12 (0000 1100) the lowest set bit is bit 2, so the longest chain has length 8 − 2 = 6 (B = −12 = 1111 0100). Generalisation (script-verified for several A): longest chain = n − (index of lowest set bit of A).

Average-case ripple delay is much shorter, but **worst-case** delay is what the clock must cover, so ripple adders are Θ(n).

---

## 5. Carry-lookahead adder (CLA)

### 5.1 Idea

Do not wait for the carry to ripple. Express every carry directly in terms of the inputs and C0, using Gi and Pi, and compute all carries in parallel.

### 5.2 Derivation (4 bits)

Start from `C(i+1) = Gi + Pi·Ci` and substitute repeatedly:

```
C1 = G0 + P0·C0
C2 = G1 + P1·C1
   = G1 + P1·G0 + P1·P0·C0
C3 = G2 + P2·G1 + P2·P1·G0 + P2·P1·P0·C0
C4 = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0 + P3·P2·P1·P0·C0
```

Reading C4: a carry leaves bit 3 if bit 3 generates; or bit 3 propagates a carry that bit 2 generated; or bits 3,2 propagate a carry that bit 1 generated; … or all four bits propagate the carry-in. Each term is an AND, the whole thing an OR: a **two-level AND-OR circuit** whose gates have fan-in up to 5. All of C1…C4 are computed at the same time, independent of each other.

### 5.3 Gate-delay count (model GD with unbounded fan-in gates, 1 delay each)

```
level                         delay    cumulative
Pi, Gi from inputs              1          1
all carries (AND-OR)            2          3
Si = Pi ⊕ Ci                    1          4
```

So a 4-bit CLA gives all sums after **4** gate delays; a 4-bit ripple adder in the same model needs 2·4 = 8.

### 5.4 Block (group) generate and propagate, multi-level CLA

A 4-bit CLA block can tell the outside world only two things:

```
G* = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0        "block generates a carry-out regardless of Cin"
P* = P3·P2·P1·P0                                  "block propagates its Cin to its Cout"
C4 = G* + P*·C0
```

These have the same form as a single bit's `G, P`, so blocks can be combined recursively.

```
16-bit adder, two-level lookahead (4 blocks of 4 bits):

   bits 3..0   bits 7..4   bits 11..8   bits 15..12
   [CLA blk0]  [CLA blk1]  [CLA blk2]   [CLA blk3]
        │G*0,P*0   │G*1,P*1   │G*2,P*2     │G*3,P*3
        └──────────┴──────┬───┴────────────┘
                 [ 2nd-level lookahead unit ]
                  gives C4, C8, C12 (and C16)
                          │
          each block's own lookahead then produces its internal carries
```

Timeline (model GD):

```
t = 1   Pi, Gi
t = 3   block G*, P*              (+2: AND-OR)
t = 5   C4, C8, C12               (+2: second-level lookahead)
t = 7   carries inside each block (+2: block lookahead with its new Cin)
t = 8   sums                      (+1: XOR)
```

Worked example E5.1 (16-bit). Two-level CLA: **8** gate delays. Ripple adder (§4): **32**. If instead you chain the four 4-bit CLA blocks like ripple stages (block carry `C(4k+4) = G*k + P*k·C(4k)`, 2 delays per block): C4 at 5, C8 at 7, C12 at 9, then inside block 3: +2 → 11, sum +1 → **12**. Two-level lookahead (8) beats rippled blocks (12), which beat pure ripple (32).

Worked example E5.2 (64-bit, three levels: 4-bit blocks, 16-bit groups, one top unit). Add one more G*/P* level on the way up (+2) and one more carry level on the way down (+2): `1 + 2 + 2 + 2 (top carries) + 2 + 2 + 1 = 12` gate delays.

General pattern for L levels of 4-bit lookahead units (n = 4ᴸ): **delay = 4L gate delays = 4·log₄n = 2·log₂n**, i.e. logarithmic in n. The price is hardware: lookahead units of fixed fan-in 5 per level.

### 5.5 Why CLA with gates of fan-in at most 2 is Θ(log n) — the careful argument

Three questions are different and often confused:

| Circuit assumption | Delay |
|---|---|
| Ripple carry | Θ(n) |
| Lookahead with **unbounded fan-in** gates (single level, all carries as flat AND-OR) | Θ(1) — constant depth, but gate fan-in and size grow with n, so it is not a fixed-technology circuit |
| Lookahead with gates of **fan-in ≤ 2** | **Θ(log n)** |

**(a) Upper bound O(log n) — naive expansion.** C(i) expanded as in §5.2 is an OR of at most i + 1 product terms, each an AND of at most i + 1 literals. A k-input AND (or OR) built from 2-input gates is a balanced tree of depth ⌈log₂k⌉. So every carry has depth at most `⌈log₂(i+1)⌉ (AND tree) + ⌈log₂(i+1)⌉ (OR tree)` ≈ 2·log₂n. Add one level for forming P, G and one for the final XOR: `O(log n)`. (This direct form uses many gates, ~O(n²), but depth is already logarithmic.)

**(b) Upper bound with few gates — the prefix (G, P) operator.** Treat each position as a pair (G, P) and define

```
(G_hi, P_hi) ∘ (G_lo, P_lo) = ( G_hi + P_hi·G_lo ,  P_hi·P_lo )
```

meaning "the combined block generates a carry if the upper part generates, or the upper part propagates what the lower part generates". This operator is **associative** (script-verified over all inputs), so the carries `C(i+1) = (G_i,P_i)∘…∘(G_0,P_0)∘(C0,0)` can be evaluated in any bracketing, in particular by a **balanced binary tree** of depth ⌈log₂ m⌉ for m operands (Kogge–Stone and Brent–Kung adders are concrete layouts of this; Kogge–Stone has minimal depth, Brent–Kung fewer gates). Each ∘ costs 2 gate delays in fan-in-2 gates (AND, then OR; the P-product is computed in parallel).

Counting for the MSB sum with C0 treated as the extra operand (C0, 0):

```
T(n) = 1 (Pi,Gi) + 2·⌈log₂ n⌉ (prefix tree for C(n−1)) + 1 (Si = Pi ⊕ Ci) = 2 + 2⌈log₂ n⌉
n =   8 →  8        n =  16 → 10      n = 32 → 12
n =  64 → 14        n = 100 → 16      n = 128 → 16     (gate delays, script-verified)
```

Compare ripple (model GD): 2n = 16, 32, 64, 128, 200, 256. Doubling n adds only 2 delays to the CLA but doubles the ripple delay.

**(c) Lower bound Ω(log n).** The top sum bit S(n−1) depends on all 2n + 1 inputs (A0…A(n−1), B0…B(n−1), C0): flipping any one of them can flip S(n−1) for suitable other inputs. A fan-in-2 gate has two inputs, so a circuit of depth d can depend on at most 2ᵈ inputs. Therefore `2ᵈ ≥ 2n + 1`, i.e. depth `d ≥ ⌈log₂(2n+1)⌉` (e.g. n = 128 → d ≥ 9; the prefix adder above uses 16, so it is within a small constant factor of optimal). With fan-in unbounded this argument gives nothing, which is why constant depth is "possible" only in the idealised unbounded model.

**Conclusion:** with fan-in ≤ 2, the time of a lookahead adder is **Θ(log n)**. The same lower-bound argument shows *no* fan-in-2 adder can be Θ(1), and a ripple chain shows Θ(n) is not tight for lookahead.

Common wrong choices and why they appear in MCQs:

* Θ(1): true only with unbounded fan-in gates (the "textbook" 4-gate-delay CLA) — the question's "gates of fan-in at most two" phrase kills it.
* Θ(√n): this is the order of carry-skip / carry-select adders with equal-sized blocks (§6), not of full lookahead.
* Θ(n): ripple carry, or fixed-size CLA blocks whose carries are rippled between blocks (n/b blocks, each a constant delay).

> Check the official key yourself; this file derives the result from first principles and does not quote the answer to any paper.

### 5.6 Fixed-size lookahead blocks with rippled block carries

If the block size b is fixed (say 4) and block carries ripple (`C(4k+4) = G*k + P*k·C(4k)`), delay is ≈ (n/b)·2 + const, which is Θ(n) although the constant is ~b times smaller than pure ripple. To get Θ(log n) the block-level carries must themselves be computed by lookahead (§5.4), recursively.

---

## 6. Other fast adders (concept level)

### 6.1 Carry-select adder

Split the n bits into blocks. For every block except the first, build **two** ripple adders in parallel: one assuming carry-in 0, one assuming 1. When the real carry arrives from the previous block, a multiplexer picks the right pair of sum bits and the right carry-out.

```
              ┌── adder (Cin=0) ──┐
 block k  ────┤                   ├─ MUX ──► sums, carry-out
              └── adder (Cin=1) ──┘    ▲
                                       └── real carry from block k−1
```

With equal blocks of b bits, ripple time per bit t_c, mux delay t_m:

```
T ≈ b·t_c + (n/b − 1)·t_m          minimised at b* = √(n·t_m / t_c)  →  T ≈ 2√(n·t_c·t_m) − t_m   = Θ(√n)
```

Worked example E6.1 (16 bits, t_c = 2, t_m = 2 gate delays, 4 blocks of 4). Block 0 uses the real Cin: C4 at 4·2 = 8. Blocks 1–3 finish both versions at 8 and wait for the carry. C8 = 8 + 2 = 10, C12 = 12, last sums at 14.
`T = 4·2 + (4 − 1)·2 = 14`; formula check: b* = √(16·2/2) = 4, T = 2√(16·2·2) − 2 = 14. Ripple adder (model: 2 per stage) needs 32.

Worked example E6.2 (24 bits, same t_c, t_m; blocks of sizes 4, 4, 6, 10). Block-ready times 8, 8, 12, 20; carry arrivals `C = max(ready, previous carry) + 2`: C4 = 8, C8 = 10, C14 = max(12, 10) + 2 = 14, C24 = max(20, 14) + 2 = 22. Last sum at **22**. With six equal blocks of 4: 8 + 5·2 = 18. Lesson: a big late block is slow because its own ripple (20) is on the critical path; block sizes should grow only as fast as the carry arrives.

### 6.2 Carry-skip (carry-bypass) adder

Each block is a ripple adder plus a "skip" gate: if every bit in the block has Pi = 1 (block propagate P* = P3·P2·P1·P0), the incoming carry bypasses the block's ripple chain directly to the block output. Worst case: carry is generated in the first block, rippled to its end, skipped across the middle blocks, then rippled into the last block. With equal blocks of size b the delay is roughly `2b·t_c + (n/b − 2)·t_skip`, minimised at b ∝ √n, so also **Θ(√n)**. (Only the shape matters for GATE.)

### 6.3 Summary

| Adder | Delay order | Extra hardware |
|---|---|---|
| Ripple carry | Θ(n) | none |
| Carry-skip, equal blocks | Θ(√n) | skip AND/mux per block |
| Carry-select, equal blocks | Θ(√n) | duplicate adders + muxes (~2× adders) |
| Lookahead, fan-in ≤ 2 (prefix) | Θ(log n) | more gates, wiring |
| Lookahead, idealised unbounded fan-in | Θ(1) | gates of size ∝ n |

---

## 7. Adder/subtractor, overflow, carry vs borrow, status flags

### 7.1 One circuit for add and subtract

```
 M = 0 : A + B            M = 1 : A − B = A + ~B + 1

        B(n−1)…B0
           │ │          M ──┬────────────── C0 (carry-in of bit 0)
          XOR  (each Bi ⊕ M)│
           │ │              │
           ▼ ▼              ▼
        n-bit adder (A, B⊕M, C0 = M) ──► result, Cout
```

n XOR gates plus the adder. XOR with 0 passes B; XOR with 1 inverts it, and the carry-in M = 1 supplies the "+1" of the 2's complement.

### 7.2 Carry-out is *not* signed overflow

Two different questions are asked of the same addition:

| Question | Operands treated as | Detect with |
|---|---|---|
| Unsigned result wrong (does not fit in n bits)? | unsigned | **carry-out of the MSB** = 1 (for addition) |
| Signed result wrong? | 2's complement | **V = C(n−1) ⊕ C(n)** (carry *into* MSB XOR carry *out of* MSB) |

Derivation of V (signed addition A + B). Overflow is possible only if A and B have the same sign:

* **Both non-negative** (MSBs 0 0): the MSB column adds 0 + 0 + Cin → carry-out C(n) = 0, and the MSB of the sum is C(n−1). If C(n−1) = 1, the sum's sign bit is 1 although both operands were positive: overflow. So V = C(n−1) = C(n−1) ⊕ 0 ✓.
* **Both negative** (MSBs 1 1): the MSB column always produces carry-out 1. The sign bit of the sum is 1 ⊕ 1 ⊕ C(n−1) = C(n−1). If C(n−1) = 0 the sum looks non-negative: overflow. So V = 1 when C(n−1) = 0 = C(n−1) ⊕ 1 ✓.
* **Opposite signs** (MSBs 0 1): the true sum lies between the operands, so it always fits. Column MSB: carry-out = C(n−1), so V = C(n−1) ⊕ C(n) = 0 ✓.

Equivalent sign rule: **overflow iff both operands have the same sign and the result has the opposite sign.** For subtraction A − B (computed as A + ~B + 1): overflow iff A and B have **different** signs and the result sign differs from A's sign. (All four forms are script-verified exhaustively for 4- and 8-bit.)

Therefore:

* signed overflow can occur with carry-out 0 (e.g. 0x7F + 0x01 = 0x80, C = 0, V = 1);
* carry-out can be 1 with no signed overflow (0xFF + 0x01 = 0x00, C = 1, V = 0, which is −1 + 1 = 0);
* both can be 1 (0x80 + 0x80 = 0x00: −128 + −128 = −256, and 128 + 128 = 256 unsigned);
* never conclude "overflow" from the carry alone, and never read the sign bit of an unsigned sum.

### 7.3 Status flags

```
Z = 1  iff all result bits are 0          Z = NOR(R(n−1), …, R0)
N = R(n−1)  (sign bit of the stored result)  — N is the stored bit, even when the result overflowed
C = carry out of the MSB (as produced by the adder)
V = C(n−1) ⊕ C(n)
```

Worked example E7.1 — flag table, 8-bit adds (script-verified):

| Operation | Stored result | N | Z | C | V | Reading |
|---|---|---|---|---|---|---|
| 0x64 + 0x28 (100 + 40) | 0x8C | 1 | 0 | 0 | 1 | signed overflow (140 > 127); unsigned fine (140 ≤ 255) |
| 0xC8 + 0x90 (−56 + −112 signed; 200 + 144 unsigned) | 0x58 | 0 | 0 | 1 | 1 | both overflow: unsigned 344 > 255; signed −168 < −128 |
| 0xFF + 0x01 | 0x00 | 0 | 1 | 1 | 0 | unsigned overflow only; signed −1 + 1 = 0 is correct |
| 0x80 + 0x80 | 0x00 | 0 | 1 | 1 | 1 | both overflow |

### 7.4 Carry vs borrow after subtraction (state the convention!)

After `A − B` computed as `A + ~B + 1`, the raw adder carry-out is **1 when A ≥ B (unsigned), 0 when A < B**. (Reason: A + (2ⁿ − B) ≥ 2ⁿ ⟺ A ≥ B.) Two conventions exist:

| Convention | Flag C after subtraction | C = 1 means |
|---|---|---|
| **Raw carry** (ARM-style, and what "the carry flag is the raw carry-out" means) | C = Cout | A ≥ B unsigned (no borrow) |
| **Borrow flag** (x86 CF-style; also "C = 1 means unsigned borrow") | C = NOT Cout | A < B unsigned (borrow occurred) |

On many ISAs the hardware inverts the carry on subtraction so that C means borrow. Exam questions state the convention; if they do not, say which one you assume. Addition always sets C = raw carry-out in both conventions.

Worked example E7.2 (8-bit, raw-carry convention): 0x30 − 0x50 (48 − 80) = 0x30 + 0xAF + 1 = 0xE0, raw Cout = 0, N = 1, Z = 0, V = 0. Unsigned 48 < 80 ✓ (Cout = 0 ⟹ A < B). Signed 48 < 80, N ⊕ V = 1 ✓. The stored pattern 0xE0 is the unsigned value 224 = 256 − 32, or signed −32 ✓.

Worked example E7.3 — the trap where signed and unsigned disagree and V matters: 0x80 − 0x01 (−128 − 1 signed; 128 − 1 unsigned). Result 0x7F, Cout = 1 (A ≥ B unsigned ✓), N = 0, V = 1 (operands of different sign, result sign differs from A). Signed less-than = N ⊕ V = 1 ✓ (−128 < 1) even though the result's sign bit is 0. Unsigned: no borrow, 128 ≥ 1.

### 7.5 Conditional branches from flags (after A − B, i.e. a compare)

| Relation | Signed condition | Unsigned condition, raw-carry C | Unsigned condition, borrow C |
|---|---|---|---|
| A = B | Z = 1 | Z = 1 | Z = 1 |
| A ≠ B | Z = 0 | Z = 0 | Z = 0 |
| A < B | N ⊕ V = 1 | C = 0 | C = 1 |
| A ≥ B | N ⊕ V = 0 | C = 1 | C = 0 |
| A ≤ B | Z + (N ⊕ V) = 1 | C = 0 or Z = 1 | C = 1 or Z = 1 |
| A > B | Z = 0 and N ⊕ V = 0 | C = 1 and Z = 0 | C = 0 and Z = 0 |

Why signed A < B is **N ⊕ V** (not just N): if no overflow occurred, the stored sign N is the sign of the true difference, so A < B ⟺ N = 1. If overflow occurred, the stored sign is the *opposite* of the true sign, so A < B ⟺ N = 0 ⟺ N ⊕ V = 1 (V = 1). Exhaustively verified over all 65 536 8-bit pairs. Why unsigned A < B is just "no carry-out (raw)" : see the inequality above. Z distinguishes equality; it cannot give direction.

Signed vs unsigned comparison of the *same bit patterns* can disagree: 0x90 vs 0x30 — signed 0x90 = −112 < 48 (true), unsigned 144 > 48. Subtracting: 0x90 − 0x30 = 0x60, Cout = 1 (unsigned: no borrow, so A ≥ B), N = 0, V = 1 (negative minus positive gave a positive result), N ⊕ V = 1 (signed A < B). One subtraction, two different answers depending on which flags the branch reads.

---

## 8. ALU organisation

### 8.1 Structure

```
            A (n bits)        B (n bits)
               │                 │
               ▼                 ▼
      ┌──────────────────────────────────────┐
      │ Logic unit      : AND, OR, XOR, NOT  │──┐
      │ Arithmetic unit : A ± B, A+1, A−1…   │──┤──► result mux ──► [shifter] ──► R
      │ (adder + B-input conditioning)       │  │          ▲
      └──────────────────────────────────────┘  │          │
                function-select lines ──────────┴──────────┘
                flags: Z, N, C, V  ◄── from result / adder carries
```

* The **function-select** (opcode/control) field of k bits distinguishes at most 2ᵏ operations: 4 bits → 16, 3 bits → 8. (Practice Q7.)
* In the classic 4-bit ALU slice (the 74181 pattern) one mode bit M chooses logic vs arithmetic and 4 select bits choose among 16 functions in each mode.
* The datapath is built from **bit slices**: n identical slices (each with a full adder, a few gates and a multiplexer) connected by the carry line. A 32-bit ALU is 32 slices (plus lookahead wiring if the carries are accelerated).

### 8.2 Logic unit

Per bit, the four basic logic ops are computed in parallel and a 4:1 multiplexer selects one:

```
Ri = AND(Ai,Bi) | OR(Ai,Bi) | XOR(Ai,Bi) | NOT(Ai)     (selected by the 2-bit function field)
```

Worked example E8.1: A = 1100, B = 1010 → AND 1000, OR 1110, XOR 0110, NOT A = 0011.

### 8.3 Arithmetic unit: condition the B input, feed the adder

Instead of building separate hardware for increment/decrement/subtract, feed the adder a *conditioned* second operand Y and an optional carry-in:

```
S1 S0 | Y      || Cin = 0      | Cin = 1
 0 0  | 0000   || A            | A + 1      (transfer, increment)
 0 1  | B      || A + B        | A + B + 1
 1 0  | ~B     || A − B − 1    | A − B      (subtract)
 1 1  | 1111   || A − 1        | A          (decrement, transfer)
```

(Y = all ones is the pattern −1, so A + Y = A − 1; with Cin = 1 it becomes A + 2ⁿ ≡ A.) Script check (8-bit, A = 0x35, B = 0x12): Cin=0 row gives 0x35, 0x47, 0x22, 0x34; Cin=1 row gives 0x36, 0x48, 0x23, 0x35 ✓. Eight arithmetic functions from a 2-bit select and one carry bit.

### 8.4 Where the flags come from

* Z: an n-input NOR of the result (in fan-in-2 gates a tree of depth ⌈log₂n⌉ — this can be the slowest flag).
* N: the MSB of the result.
* C: carry-out of the adder (with the borrow-inversion convention applied for subtractions if the ISA defines it that way).
* V: one XOR of the last two carries.
* Logic and shift instructions typically update Z and N; whether they touch C and V depends on the ISA.

---

## 9. Shifts, rotates and the barrel shifter

### 9.1 Shift types (8-bit examples)

```
logical left   (LSL):  0xD4 = 1101 0100  >>  fill LSB with 0, MSB drops out (goes to C)
logical right  (LSR):  fill MSB with 0
arithmetic right (ASR): fill MSB with a COPY OF THE SIGN BIT
rotate left/right:     bits leaving one end re-enter at the other end (ROL/ROR); with carry (RCL/RCR) the carry flag joins the ring
```

### 9.2 Shifts as multiplication and division by 2ᵏ

| Shift | Unsigned | 2's complement |
|---|---|---|
| left by k | × 2ᵏ (mod 2ⁿ) | × 2ᵏ (mod 2ⁿ) — correct only if no overflow |
| logical right by k | ⌊x / 2ᵏ⌋ | **wrong for negative numbers** (sign bit becomes 0) |
| arithmetic right by k | — | ⌊x / 2ᵏ⌋ — rounds toward **−∞** |

Failure cases (worked):

* **Left shift overflow.** Signed 8-bit 0x50 (80) << 1 = 0xA0 = −96: the bit that was shifted into the sign position changed the sign. A signed left shift by k is overflow-free iff the top k + 1 bits (including the sign) are all equal. Unsigned 200 << 1 = 400 mod 256 = 144: a 1 fell off the end. Example with a good case: 16-bit 0xFA3C (−1476) << 2 = 0xE8F0 (−5904 = −1476·4) since the top 3 bits `111` are equal.
* **Logical right shift of a negative number.** 0xD4 = −44; LSR 2 = 0x35 = 53 ✗; ASR 2 = 0xF5 = −11 = −44/4 ✓.
* **Rounding.** ASR rounds toward −∞: −7 >> 1 = −4 (−7/2 = −3.5, floor −4). C/Java integer division truncates toward 0 and gives −3. So `x >> k` and `x / 2ᵏ` agree for negative odd x only after a correction (add 2ᵏ − 1 before shifting).
* **Constant multiply with shifts.** x × 10 = (x << 3) + (x << 1): for x = 13 this is 104 + 26 = 130 ✓.
* Worked ASR: 0xB8 = 1011 1000 = −72; ASR 3 → 1111 0111 = 0xF7 = −9 = −72/8 ✓ (LSR would give 0x17 = 23 ✗).

### 9.3 Barrel shifter

A shift-register shifter moves one place per clock, so a shift by k takes k cycles. A **barrel shifter** shifts by any amount 0…n−1 in one combinational pass:

```
n = 8, shift amount s = s2 s1 s0 (binary)

 data ─► [stage 0: shift by 1 if s0] ─► [stage 1: shift by 2 if s1] ─► [stage 2: shift by 4 if s2] ─► out
          n 2:1 muxes                    n 2:1 muxes                    n 2:1 muxes
```

* Stages: ⌈log₂n⌉ (one per bit of the shift amount); each stage is a column of n 2:1 multiplexers choosing "pass" or "shift by 2ⁱ".
* Total muxes = n·log₂n (e.g. 32-bit: 32·5 = 160; 16-bit: 16·4 = 64).
* Delay = log₂n mux delays, **independent of the shift amount**. E.g. 64-bit, 0.35 ns per mux: 6·0.35 = 2.1 ns.
* A shift by 11 = 1011₂ = 8 + 2 + 1 activates stages 3, 1 and 0 (all stages still sit in the path).
* The same structure with wrap-around wiring does rotates; with sign-fill it does ASR.

---

## 10. Multiplication

### 10.1 Sequential shift-and-add (unsigned)

Registers: **M** (n-bit multiplicand), **Q** (n-bit multiplier, ends up holding the low half of the product), **A** (n-bit accumulator, initially 0, ends up with the high half), and a 1-bit carry **C**. Product = A:Q (2n bits).

```
repeat n times:
    if Q0 == 1 :  (C, A) ← A + M          (n-bit add, carry captured in C)
    shift  C:A:Q  right by 1              (C into A's MSB, A0 into Q's MSB)
```

Why it works: step i either adds M·2ⁱ (the shift positions the addition relative to the growing product) or nothing; the multiplier bit consumed at Q0 is replaced by a product bit.

Worked example E10.1: 13 × 11, n = 4 (M = 1101, Q = 1011). (State shown after the conditional add, then after the shift.)

```
step  Q0  action     C  A     Q          → after shift   A     Q
 1    1   A ← A+M    0  1101  1011                      0110  1101
 2    1   A ← A+M    1  0011  1101       (0110+1101 = 1 0011)   1001  1110
 3    0   none       0  1001  1110                      0100  1111
 4    1   A ← A+M    1  0001  1111       (0100+1101 = 1 0001)   1000  1111
product = A:Q = 1000 1111 = 143 = 13 × 11 ✓      additions = 3 = number of 1s in the multiplier
```

**Cost.** n iterations, each an add (only when Q0 = 1) and a shift. If the add and shift happen in series with times t_add and t_shift: `T = n·(t_add + t_shift)` worst case; if they share a clock cycle: n cycles. Counting only needed adds: n shift cycles + (number of 1s in Q) add cycles when add and shift occupy different cycles. 8-bit, add 4 ns, shift 1 ns per iteration: 8·5 = 40 ns. A combinational (array) multiplier trades hardware (n² AND gates and ~n² adders) for one long combinational path; a Wallace/carry-save tree reduces the partial-product addition depth to Θ(log n) before the final fast adder.

**Width rule.** n × n bits needs 2n result bits. Unsigned n-bit × n-bit can never overflow 2n bits; multiplying only into n bits does.

### 10.2 Why plain shift-and-add fails for signed numbers

If M is negative and sign-extended only to n bits, the partial products are not sign-extended to 2n bits, and a negative multiplier's MSB has weight −2ⁿ⁻¹, not +2ⁿ⁻¹. Booth's algorithm fixes both.

### 10.3 Booth's algorithm (2's complement, radix-2)

**Idea.** A run of 1s in the multiplier from bit i to bit j is worth `2^(j+1) − 2ⁱ`. So instead of j − i + 1 additions you do **one subtraction at the start of the run and one addition just after its end**. 0 → 1 → … → 1 → 0 scanning from LSB upward: start of a run (bit pair `Q0, Q−1 = 1,0`) → subtract M; end of a run (pair `0,1`) → add M; inside a run of 1s or zeros (pairs `11`, `00`) → nothing.

Hardware: registers A (init 0), Q (multiplier), M, and a flip-flop **Q−1** (init 0). Repeat n times:

```
examine (Q0, Q−1):
   1 0  →  A ← A − M
   0 1  →  A ← A + M
   0 0 or 1 1  →  no arithmetic
then ARITHMETIC shift right of A:Q:Q−1 (A's sign bit is replicated)
```

Product = A:Q (2n-bit 2's complement).

**Why it works.** Write the multiplier as `Q = −q(n−1)·2ⁿ⁻¹ + Σ_{i<n−1} q(i)·2ⁱ`. Using 2ⁱ = 2·2ⁱ − 2ⁱ one can regroup this as `Q = Σ_{i=0}^{n−1} (q(i−1) − q(i))·2ⁱ` with q(−1) = 0 (the sign bit is handled automatically). So in step i the multiplicand M is added with weight `q(i−1) − q(i)`, which is **+1 for the pair (q(i), q(i−1)) = (0, 1), −1 for (1, 0), and 0 for (0, 0) and (1, 1)**. That is exactly the table above; no special case for a negative multiplier is needed. The arithmetic shift (sign replication) keeps partial products correctly sign-extended.

**Number of additions/subtractions.** Count the places where adjacent bits differ in the string `q(n−1) … q1 q0 0` (with an appended 0 on the right). Examples (8-bit unless noted; each verified):

| Multiplier Q | Pattern with appended 0 | Add/sub operations |
|---|---|---|
| 0000 0000 | 0000 0000 0 | 0 |
| 1111 1111 (−1) | 1111 1111 0 | 1 (one subtraction) |
| 0111 (4-bit, 7) | 0111 0 | 2 (subtract, then add) |
| 0111 0010 (114) | 0111 0010 0 | 4 |
| 0101 0101 | 0101 0101 0 | 8 (= n; the worst case) |
| 1010 1010 | 1010 1010 0 | 7 |

Maximum is n (alternating bits ending in 1), minimum 0 (only for Q = 0). Booth is **faster than shift-add only when the multiplier has long runs**; the hardware time is still n shift steps.

Worked example E10.2: 4-bit, M = 0110 (6), Q = 1101 (−3). Product should be −18.

```
step (Q0,Q−1)  action   A after op   → after ASR: A     Q     Q−1
 init                                              0000  1101  0
 1    (1,0)    A ← A−M  1010                       1101  0110  1       (0000 − 0110 = 1010)
 2    (0,1)    A ← A+M  0011  (1101+0110 = 1 0011) 0001  1011  0
 3    (1,0)    A ← A−M  1011  (0001−0110)           1101  1101  1
 4    (1,1)    none     1101                        1110  1110  1
A:Q = 1110 1110 = −18 ✓      add/sub operations = 3
```

Worked example E10.3: 4-bit, M = 0101 (5), Q = 1101 (−3): after 2 iterations A:Q = 0001 0111; final A:Q = 1111 0001 = −15 ✓ (same multiplier, 3 operations).

**Edge case.** If M = −2ⁿ⁻¹ (the most negative n-bit value), `A − M` needs +2ⁿ⁻¹, which does not fit in an n-bit accumulator; textbook hardware therefore uses an (n+1)-bit adder or sign-extends A. Exhaustive simulation of 6-bit Booth with an n-bit A fails only for M = −32.

### 10.4 Modified (radix-4, "bit-pair") Booth

Look at **three** bits at a time, `(q(2i+1), q(2i), q(2i−1))`, stepping 2 bits per iteration: the multiplier digit d(i) ∈ {−2, −1, 0, +1, +2} and Q = Σ d(i)·4ⁱ.

```
q(2i+1) q(2i) q(2i−1) | digit | partial product added (× 4ⁱ)
 0 0 0 |  0 | 0
 0 0 1 | +1 | +M
 0 1 0 | +1 | +M
 0 1 1 | +2 | +2M (shift M left 1)
 1 0 0 | −2 | −2M
 1 0 1 | −1 | −M
 1 1 0 | −1 | −M
 1 1 1 |  0 | 0
```

n-bit multiplier (n even) → n/2 partial products (half the work). Number of add/sub operations = number of non-zero digits.

Worked example E10.4: Q = 0111 0010 (114). Append q(−1) = 0 and read groups of three bits starting at the LSB end (adjacent groups overlap by one bit):

```
group (q1 q0 q−1) = 1 0 0  → −2        group (q3 q2 q1) = 0 0 1  → +1
group (q5 q4 q3)  = 1 1 0  → −1        group (q7 q6 q5) = 0 1 1  → +2
Q = −2·4⁰ + 1·4¹ − 1·4² + 2·4³ = −2 + 4 − 16 + 128 = 114 ✓
```

Four non-zero digits → four partial products for an 8-bit multiplier (radix-2 Booth would take 8 iterations, 4 of which also happen to add/subtract for this particular Q; the saving of radix-4 is the guaranteed halving of iterations, not of the add/sub count for every Q). Another check: 4-bit Q = 1101 (−3) gives digits [+1, −1] → 1 − 4 = −3 ✓.

---

## 11. Division

### 11.1 Restoring division (unsigned)

Registers: **A** (n+1 bits, remainder, initially 0), **Q** (n-bit dividend → becomes quotient), **M** (n-bit divisor). Repeat n times:

```
1. shift A:Q left by 1 (A's LSB gets Q's old MSB)
2. A ← A − M
3. if A < 0 :  Q0 ← 0 ; A ← A + M   (RESTORE the old value)
   else      :  Q0 ← 1
```

After n steps Q = quotient, A = remainder. Each step is one long division step on binary digits.

Worked example E11.1: 13 ÷ 3, n = 4 (A 5 bits).

```
step | after shift A:Q | A−M    | action        | A (new) Q
 init|  00000 1101     |        |               | 00000   1101
  1  |  00001 101_     | −2     | restore, q=0  | 00001   1010
  2  |  00011 010_     |  0     | keep, q=1     | 00000   0101
  3  |  00000 101_     | −3     | restore, q=0  | 00000   1010
  4  |  00001 010_     | −2     | restore, q=0  | 00001   0100
quotient Q = 0100 = 4, remainder A = 00001 = 1      (13 = 4·3 + 1 ✓)
```

Cost: n subtractions plus one restoring addition for every quotient bit that is 0, so up to 2n add/sub operations. For 45 ÷ 7 with n = 6: quotient 6 = 000110 has four 0 bits → 6 + 4 = **10** add/sub operations, remainder 3 (script-verified). (The restore count equals the number of 0 quotient bits only if the dividend and quotient fit in n bits, which is the standard setup.)

### 11.2 Non-restoring division

Observation: in restoring division, when `A − M < 0` the step restores A (adds M back) and the *next* step computes `2A − M` (shift, then subtract). If we skip the restore, the register holds A' = A − M, and the next step can compute `2A' + M = 2A − 2M + M = 2A − M` — the same value — with a single operation (shift, then **add**). So:

```
repeat n times:
   if A ≥ 0 :  shift A:Q left ; A ← A − M
   else     :  shift A:Q left ; A ← A + M
   Q0 ← 1 if A ≥ 0 else 0
after the loop: if A < 0 then A ← A + M      (remainder correction)
```

Worked example E11.2: 13 ÷ 3, n = 4: A after each step = −2, 0, −3, −2 with quotient bits 0, 1, 0, 0 → Q = 0100 = 4; final A = −2 < 0 → A ← −2 + 3 = 1. Remainder 1 ✓ (n + 1 = 5 add/sub operations including the correction).

Each step has exactly one add/sub (no separate restore), so n operations (+1 for the final correction) instead of up to 2n; the control logic is a little more complex. Both algorithms were verified by exhaustive simulation for 5- and 6-bit operands.

Signed division is done by dividing magnitudes and fixing signs (quotient sign = XOR of signs; remainder takes the dividend's sign), or by signed variants of non-restoring division.

---

## 12. Floating-point arithmetic at the ALU level

> Representation (fields, bias, special values, ranges): [../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT](../../02-DIGITAL-LOGIC/03-NUMBER-REPRESENTATION-AND-ARITHMETIC/02-FLOATING-POINT). Bridge summary only:

```
IEEE 754 single : sign(1) | exponent(8, bias 127)  | fraction(23) → value (−1)^s × 1.f × 2^(e−127)   (24-bit significand incl. hidden 1)
IEEE 754 double : sign(1) | exponent(11, bias 1023)| fraction(52) → 53-bit significand
exponent field 0 → zero/denormal ; all ones (255 / 2047) → ∞ / NaN
```

### 12.1 Addition / subtraction

```
1. Unpack. Compare exponents. Swap so that X has the larger exponent.
2. Align: shift the significand of Y RIGHT by d = e_X − e_Y (keep guard, round, sticky bits).
3. Add (or subtract, if the signs differ) the significands as integers; result sign from magnitude comparison.
4. Normalise: carry-out → shift right 1, exponent + 1; leading zeros (cancellation) → shift left k, exponent − k.
5. Round (default round-to-nearest, ties to even). Rounding may carry → renormalise.
6. Check overflow (exponent too large → ∞) / underflow (too small → denormal/0).
```

Worked example E12.1 (exact toy numbers; 6 fraction bits kept). X = 1.101₂ × 2⁵ (= 52), Y = 1.001₂ × 2² (= 4.5).

```
d = 5 − 2 = 3 → Y' = 0.001001 × 2⁵
        1.101000
      + 0.001001
      = 1.110001 × 2⁵      already normalised → 1.765625 × 32 = 56.5 = 52 + 4.5 ✓
IEEE single of 56.5: exponent field 5 + 127 = 132 = 1000 0100, fraction 110001 0…0 → 0x42620000 (verified)
```

Cancellation: 1.0001₂ × 2³ − 1.0000₂ × 2³ = 0.0001₂ × 2³ → shift left 4 → 1.0 × 2⁻¹ (= 0.5): after catastrophic cancellation only the low-order (possibly already-rounded) bits remain, so the *relative* error can be large.

**Alignment can annihilate the small operand.** In single precision (24-bit significand), once d is larger than the significand width plus the guard and round bits, the aligned Y can influence only the sticky bit and (with round-to-nearest) the sum is simply X. Concretely: x = 1.5×2¹⁰, y = 2⁻¹⁴: d = 24; the spacing of numbers near x is ulp(x) = 2^(10−23) = 2⁻¹³, so y is **exactly half an ulp**: a tie, resolved to even: x + y = x (verified). With y = 1.5·2⁻¹⁴ (more than half an ulp) the sum rounds up to x + 2⁻¹³.

### 12.2 Multiplication

```
1. sign = sX ⊕ sY.
2. exponent = eX + eY − bias   (in biased form; the bias is counted twice, so subtract one copy).
3. significand = 24-bit × 24-bit integer multiply → 48-bit product (a fixed-point multiplier: §10).
4. Normalise: product of two values in [1,2) lies in [1,4) → at most a 1-bit right shift, exponent + 1.
5. Round, check overflow/underflow.
```

Worked example E12.2: (1.5 × 2³) × (1.25 × 2⁻²) = 12 × 0.3125. Sign 0. Biased exponents 130 and 125: 130 + 125 − 127 = 128 → true exponent +1. Significands: 1.5 × 1.25 = 1.875 (already in [1,2)). Result 1.875 × 2¹ = 3.75 ✓. Division: subtract exponents (+ bias), divide significands, normalise by at most 1 left shift.

### 12.3 Why floating-point arithmetic loses precision and is not associative

Every operation rounds its exact result to 24 significant bits. Rounding errors depend on the magnitudes involved, so grouping changes the answer.

Worked example E12.3 (single precision): a = 2²⁴ = 16 777 216, b = 1.
* (a + b) + b: a + b = 16 777 217 is not representable (spacing is 2 at 2²⁴), tie → even → 16 777 216; again for + b → **16 777 216**.
* a + (b + b) = 2²⁴ + 2 = **16 777 218**, exactly representable.
So (a + b) + b ≠ a + (b + b) (difference 2). Consequences: summation order matters; never test floats with ==; adding a tiny number to a huge one may do nothing; subtracting nearly equal numbers cancels most significant digits.

---

## 13. Data path and register transfers

### 13.1 Single-bus data path

```
  ══════════════════════════ internal processor bus (one value per step) ══════════════════════════
     ▲▼          ▲▼          ▲▼         ▲▼          ▲▼             │ (bus is ALU input B)    ▲
     PC          MAR         MDR        IR        R0 … R7          │                        │ Zout
                  │           │                                    ▼                        │
              address       data                 Y ──────────►  ┌──────┐ ───────────────► Z ┘
              to memory   to/from memory      (Yin from bus)     │ ALU  │      (ALU result is latched in Z)
                                                                  └──────┘
  Xout : register X drives the bus      Xin : register X latches the bus at the end of the step
```

* A register's **out** control signal (Xout) places its contents on the bus; **in** (Xin) latches the bus value at the end of the clock step. Notation varies: the PYQ-style `R1r`/`R1w` means "read R1 onto the bus" / "write R1 from the bus".
* **Only one register may drive the bus in any one step** (single-bus constraint), but several registers may latch the same bus value in that step.
* The ALU has two inputs: one is the bus, the other is the temporary register **Y** (or TEMP1) loaded earlier. The ALU output cannot be put straight on the same bus that feeds it, so it goes into a temporary register **Z** (TEMP2) and is placed on the bus in the next step.
* Memory accesses go through MAR (address) and MDR (data); a read takes at least one clock step (maybe several: the control unit waits for the memory-function-complete signal).
* The PC is incremented in the fetch phase, either by a dedicated incrementer or through the ALU (which costs extra steps because the bus and ALU are shared).

### 13.2 Fetch, then execute; the ordering rules

```
FETCH  : MAR ← PC ; Read ; (PC ← PC + increment, concurrently if there is a separate incrementer)
         MDR ← M[MAR]            (data arrives after the memory delay)
         IR  ← MDR
DECODE : the control unit reads IR; only now does it know what the instruction wants
EXECUTE: operand transfers, ALU operation, write-back
```

Ordering follows from **data dependencies** and the **single-bus constraint**:

1. `PC → MAR` before the memory read (the address must be in MAR).
2. memory read completes (MDR valid) before `MDR → IR`.
3. IR must be loaded before any instruction-specific step (nothing can start executing an unknown instruction).
4. First operand must reach Y (or TEMP1) *before* the step that puts the second operand on the bus and triggers the ALU.
5. The ALU step writes Z (TEMP2); `Z → destination register` is therefore strictly after it.
6. Two transfers that both need the bus as source cannot share a step.

Worked example E13.1 (original). Instruction `SUB R3, R4, R5` meaning R3 ← R4 − R5 on a single-bus data path with Y and Z. Memory read takes one step; PC increment is done by a separate incrementer in the first step. The five micro-steps, listed out of order:

```
(a) Zout, R3in
(b) R4out, Yin
(c) MDRout, IRin
(d) PCout, MARin, Read
(e) R5out, SUB (Y − bus), Zin
```

Dependencies: (d) before (c) (rules 1–2); (c) before (b) and (e) (rule 3); (b) before (e) (rule 4, and ALU "Y − bus" means the first operand R4 must be in Y, otherwise it computes R5 − R4); (e) before (a) (rule 5). Every step needs the bus as source (d: PC; c: MDR; b: R4; e: R5; a: Z) so no two can be merged (rule 6). The order is forced: **d, c, b, e, a** (script-enumerated: the only one of 120 permutations that respects all constraints). Clock steps: 5.

**General recipe for an ordering question (the 2020 pattern):**

1. Mark each step's *inputs* (what it reads) and *outputs* (what it writes).
2. Draw edges producer → consumer (RAW dependencies) including the fetch chain PC → MAR → MDR → IR.
3. Note single-bus conflicts (steps that need different register sources cannot be merged but can be freely ordered unless a dependency forbids it).
4. Eliminate options violating any edge; usually one remains.

**Warning about the mapped 2020 question:** the data-path diagram and some step notation are garbled or missing in the mapping (the figure is not reproduced; the printed text contains OCR damage such as stray symbols in place of subscripts). Do not rely on the mapping text for the exact register names; use the official PDF, and apply the recipe above.

Worked example E13.2 — counting clock steps. For `ADD Rd, Rs` (Rd ← Rd + Rs) on the same single-bus path with a **two-cycle** memory read: 1 (`PCout, MARin, Read`), 2 (wait for memory), 3 (`MDRout, IRin`), 4 (`Rdout, Yin`), 5 (`Rsout, ADD, Zin`), 6 (`Zout, Rdin`) = **6 steps**. With a one-cycle memory read: 5 steps. If the PC increment must go through the shared ALU it adds steps (`PCout, Yin`; `Select 4, ADD, Zin`; `Zout, PCin`), which is why many designs put a dedicated incrementer on the PC.

### 13.3 Multi-bus data paths

With a 3-bus data path (two source buses A, B, one destination bus C) the register file has two read ports and one write port: `R3 ← R4 − R5` executes in a **single** step (R4 → bus A, R5 → bus B, ALU, result on C → R3) and no Y/Z registers are needed. More buses = fewer clock steps per instruction but more wiring/area. The choice of data path decides the CPI of the ISA.

### 13.4 Operand-select multiplexers

A real ALU input usually has a multiplexer: operand B can be a register value or an immediate field from IR. If both A and B inputs have such multiplexers, "immediate op immediate" is possible; if only B does, one operand must be a register. (A mapped-by-text 2025 question shows a partial data path of this kind; its figure was not extractable — see `PYQ.md`.)

### 13.5 From data path to control unit

Each micro-step above is a set of control-signal values (Xout, Xin, Read, ALU function code...). The control unit's job is to generate those values in the right order:

* **Hardwired**: a step counter (T1, T2, ...) plus decoders/combinational logic of (IR opcode, step, flags) produce the control signals.
* **Microprogrammed**: each step is a microinstruction in a control store.

Follow-up: [../04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED](../04-DESIGN-OF-CONTROL-UNIT/01-HARDWIRED) and [../04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED](../04-DESIGN-OF-CONTROL-UNIT/02-MICROPROGRAMMED).

---

## 14. PYQ patterns (recognise → recipe → trap)

(No answers: the mapping marks every answer "VERIFICATION REQUIRED".)

### Pattern A — "Time/delay of an adder as a function of n" (conceptual asymptotics)

* **Recognise:** "carry lookahead adder … gates of fan-in at most two … time is Θ(?)", or "ripple-carry latency".
* **Recipe:** (1) identify the adder family; (2) identify the gate model (bounded vs unbounded fan-in); (3) use the table in §6.3 and the derivation in §5.5.
* **Traps:** answering Θ(1) because textbook CLA is "constant 4 gate delays" (that needs unbounded fan-in); confusing Θ(√n) (skip/select) with CLA; forgetting that ripple is the *worst-case* carry chain.

### Pattern B — Longest carry chain / worst-case input of a ripple adder

* **Recognise:** "which B gives the longest latency for the sum to stabilise, given A".
* **Recipe:** §4.1: find A's lowest set bit; choose B so that bit generates and all higher bits propagate (B = −A); check the length n − k.
* **Traps:** picking a B that merely produces a big sum; ignoring that generate needs both bits 1.

### Pattern C — Overflow, carry, flags

* **Recognise:** fixed-width register add/subtract with listed operand patterns; "which operation overflows".
* **Recipe:** convert patterns, apply sign rule (same-sign operands, different-sign result; for subtraction different-sign operands, result sign ≠ minuend sign) or carries-XOR rule; remember sign-magnitude has a different rule (magnitude carry-out); remember "unsigned overflow" = carry-out for addition.
* **Traps:** using carry-out for signed overflow; thinking 0x7F + 1 sets carry; mixing the interpretation of subtract overflow (§7.2).

### Pattern D — Booth operation counting / tracing

* **Recipe:** count bit changes in `Q … Q0 0` (§10.3). Radix-4: count non-zero digits (§10.4).
* **Traps:** forgetting the appended 0 on the right; counting 1s instead of transitions; confusing add/sub operations with shift steps (shifts are always n).

### Pattern E — Data-path register-transfer ordering (2020 Q4 type)

* **Recipe:** §13.2 dependency recipe.
* **Traps:** operand order for non-commutative ops, ALU needs both inputs ready, result must pass through Z/TEMP2 before the destination, fetch chain PC→MAR→MDR→IR first.

### Pattern F — Shift as multiply/divide, 2's-complement left shift

* **Recipe:** hex → signed value, multiply by 2ᵏ, check fit; or shift the bit pattern and re-read. Trap: overflow and logical vs arithmetic right shift.

### Pattern G — Floating-point ALU questions

* **Recipe:** unpack, align, operate, normalise, round (§12). Trap: mistaking the exponent bias, comparing floats as integers (works for positive normal numbers only), non-associativity.

---

## 15. Traps and misconceptions

1. Carry-out ≠ overflow. Signed overflow = C(n−1) ⊕ C(n); unsigned overflow of an add = C(n).
2. After subtraction the raw carry means "no borrow". Some ISAs invert it. Always read the stated convention.
3. A zero flag Z cannot tell A < B from A > B.
4. N is the stored sign bit; it is wrong in sign when V = 1. Signed `<` uses N ⊕ V.
5. A logical right shift of a negative 2's-complement number is not a division; use arithmetic shift. Arithmetic shift rounds toward −∞, not toward 0.
6. Left shift is ×2ᵏ only without overflow; check the top k + 1 bits.
7. A 4-bit function select = 16 operations, not 15 or 4.
8. CLA is Θ(log n) only with *fan-in-bounded* gates; with idealised unbounded fan-in it is constant; ripple is linear.
9. Booth: number of additions depends on transitions, not on the number of 1s; there is a fixed n shift steps; the multiplicand −2ⁿ⁻¹ needs an extra accumulator bit.
10. Restoring division can need 2n add/sub; non-restoring needs n (+1 correction); the non-restoring remainder may need correction.
11. FP: biased exponent subtraction in multiplication (subtract the bias once); float addition is not associative; alignment drops low bits.
12. Data path: R_in and R_out are different signals; two sources cannot drive a single bus in one step; ALU needs both operands stable; the result goes to a temporary before the destination.

---

## 16. Edge cases and assumptions to state

* Memory addressability is not involved here, but **bit width n**, **representation (unsigned / 2's complement / sign-magnitude)** and **carry/borrow convention** must always be stated.
* Delay models: unit gate delays; unbounded or bounded fan-in; whether XOR counts as 1 or 2 gate delays; whether the carry-in is available at time 0.
* Division by zero, overflow of quotient (dividend ≥ divisor·2ⁿ) must be trapped before dividing.
* −2ⁿ⁻¹: its negation overflows (−(−128) = −128 in 8 bits; V = 1 on 0 − (−128)).
* Rotates do not change the numeric value in a meaningful way; they are bit-pattern operations.

---

## 17. Connections to other COA topics

* **Instruction set:** conditional branches are decided by Z/N/C/V (§7.5); instruction formats reserve opcode bits for ALU function select.
* **Addressing modes:** effective-address calculation uses an adder; auto-increment adds the operand size to a register, which can reuse the ALU or a dedicated incrementer (the concept of the 2008 mapped entry belongs to [../02-ADDRESSING-MODES](../02-ADDRESSING-MODES)).
* **Control unit:** every micro-step of §13 is a control word.
* **Pipelining:** the clock period must cover the ALU delay; a faster adder (Θ(log n)) shortens the EX stage; the register-file write/read timing conventions of the pipeline are in [../07-INSTRUCTION-PIPELINING](../07-INSTRUCTION-PIPELINING).
* **Digital logic:** all arithmetic circuits here are composed of the gates/MUXes/flip-flops of the DL folder; number representation is in the DL number-representation folder.

---

## 18. Existing practice coverage map

(`14-PRACTICE-QUESTIONS/.../03-ARITHMETIC-AND-LOGIC-UNIT/practice.md`; question text not reproduced.)

| Q# | Skill | Section |
|---|---|---|
| 1 | Full-adder sum equation (XOR of three inputs; majority for carry) | §3.2 |
| 2 | Meaning of the zero flag | §7.3 |
| 3 | Number of full adders in an n-bit ripple adder | §3.2, §4 |
| 4 | Flags for 0x7F + 0x01 (S, Z, C, V) | §7.2–§7.3 (E7.1) |
| 5 | Ripple delay from per-stage carry/sum times | §4 (E4.1) |
| 6 | True/false statements about signed overflow, carry-out | §7.2 |
| 7 | Number of ALU operations from a k-bit select field | §8.1 |
| 8 | Subtract by adding 2's complement; stored unsigned value | §2 (negation), §7.1, E7.2 |
| 9 | Bitwise XOR | §8.2 |
| 10 | Signed overflow of 100 + 50 in 8 bits; reading wrapped value | §2, §7.2 |
| 11 | Sequential shift-add vs combinational multiplier time | §10.1 |
| 12 | Flags for 0xFF + 0x01; which statements hold | §7.2–§7.3 (E7.1) |
| 13 | Two-level CLA timing from stage delays | §5.4 (E5.1) |
| 14 | Which flags give signed vs unsigned less-than (with C = borrow convention) | §7.4–§7.5 |

---

## 19. Self-check

1. Write Gi, Pi, C(i+1), Si for a lookahead adder and expand C3.
2. What is the worst-case delay of an n-bit ripple adder in terms of per-stage delay?
3. Why can signed overflow happen with carry-out 0, and carry-out 1 happen without overflow?
4. State V in terms of carries and in terms of operand/result signs, for addition and for subtraction.
5. After A − B (raw-carry convention) which flags give signed A < B, unsigned A < B, A ≤ B?
6. Why is the delay of a fan-in-2 lookahead adder Ω(log n)? Give the counting argument.
7. How many 2:1 multiplexers and how many mux delays does an n-bit barrel shifter need?
8. Compute −7 >> 1 arithmetically and explain why C's −7/2 differs.
9. Count Booth's add/sub operations for a given multiplier; explain the appended 0.
10. Perform one restoring and one non-restoring division step sequence for a small example.
11. List the steps of floating-point addition and say where precision is lost.
12. Order the register-transfer steps of ADD R1, R2, R3 on a single-bus data path and justify the order by dependencies.
