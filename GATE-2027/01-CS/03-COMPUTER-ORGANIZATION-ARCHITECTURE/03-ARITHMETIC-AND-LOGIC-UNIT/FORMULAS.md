# Arithmetic and Logic Unit — Formulas

Companion to [NOTES.md](NOTES.md). Gate-delay model (GD) unless a question gives its own numbers: every 2-input gate = 1 delay, wires 0; an unbounded-fan-in AND/OR counts as 1 delay only when the question says so. Bit 0 = LSB. All examples were recomputed by script.

---

## A. Number-representation bridge

### A1. Ranges of n-bit integers

```
unsigned          0 … 2ⁿ − 1
2's complement   −2ⁿ⁻¹ … 2ⁿ⁻¹ − 1
sign-magnitude   −(2ⁿ⁻¹ − 1) … +(2ⁿ⁻¹ − 1)      (two zeros; also 1's complement)
```

* **Symbols:** n = word length in bits.
* **When:** choose the row for the stated representation.
* **Why:** 2's complement gives weight −2ⁿ⁻¹ to the MSB, so there is one more negative number than positive; the other two lose one code to −0.
* **Example:** n = 8 → −128…127 (2's complement), −127…127 (sign-magnitude), 0…255 (unsigned).
* **Misuse:** quoting −127 as the smallest 8-bit 2's-complement value.

### A2. Value and negation (2's complement)

```
value = −b(n−1)·2ⁿ⁻¹ + Σ_{i<n−1} b(i)·2ⁱ          −x = ~x + 1 (mod 2ⁿ)
```

* **Why:** ~x = (2ⁿ − 1) − x, so ~x + 1 = 2ⁿ − x.
* **Misuse:** negating −2ⁿ⁻¹ (gives itself; the result overflows).

### A3. Sign extension

Replicate the MSB. Example: 1010 (−6, 4-bit) → 1111 1010 (0xFA = −6, 8-bit).

---

## B. Adders

### B1. Half-adder and full-adder equations

```
Half adder :  S = A ⊕ B                 C = A·B
Full adder :  S = A ⊕ B ⊕ Cin           Cout = A·B + Cin·(A ⊕ B) = A·B + B·Cin + A·Cin
```

* **Why:** carry leaves a bit if both inputs are 1 or exactly one is 1 and a carry arrives. Sum is 1 for an odd count of 1s.
* **Misuse:** the carry is the majority, not the XOR; the sum is not A + B + Cin as an OR.

### B2. Generate / propagate

```
Gi = Ai·Bi      Pi = Ai ⊕ Bi        C(i+1) = Gi + Pi·Ci        Si = Pi ⊕ Ci
```

* **Why:** B1 rewritten. (P can also be Ai + Bi for the carry equation, but then the sum needs the XOR separately.)

### B3. Ripple-carry delay

```
MSB sum ≈ (n − 1)·t_carry + t_sum        carry-out ≈ n·t_carry
GD model (P,G 1; carry stage 2; sum XOR 1):  T = 1 + 2(n − 1) + 1 = 2n
```

* **Example:** n = 16 → 32; n = 32 → 64; n = 24 → 48 gate delays.
* **Example (given timings):** carry 2 ns per stage, sum 3 ns, n = 16: 15·2 + 3 = 33 ns.
* **Misuse:** multiplying n·(t_carry + t_sum); only the carry path is repeated.
* **Longest chain:** for fixed A with lowest set bit k, the longest carry chain has length n − k and occurs for B = −A.

### B4. Four-bit lookahead carries

```
C1 = G0 + P0·C0
C2 = G1 + P1·G0 + P1·P0·C0
C3 = G2 + P2·G1 + P2·P1·G0 + P2·P1·P0·C0
C4 = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0 + P3·P2·P1·P0·C0
```

* **Why:** repeated substitution of C(i+1) = Gi + Pi·Ci.
* **Misuse:** forgetting the C0 term or the growing fan-in (fan-in 5 for C4).

### B5. Block generate/propagate

```
G* = G3 + P3·G2 + P3·P2·G1 + P3·P2·P1·G0         P* = P3·P2·P1·P0         C4 = G* + P*·C0
```

* **When:** building multi-level lookahead (blocks act like single bits with (G*, P*)).

### B6. Delay of unbounded-fan-in CLA hierarchies (model GD)

```
single 4-bit CLA      : 1 + 2 + 1 = 4
L levels (n = 4ᴸ)     : T = 1 + 2(L − 1) + 2 + 2(L − 1) + 1 = 4L = 2·log₂n
16-bit, 2 levels      : 8       64-bit, 3 levels : 12
16-bit with 4-bit CLA blocks whose block carries ripple (2 per block): 12
ripple 16-bit : 32     ripple 64-bit : 128
```

* **Why:** 1 for P,G; 2 per level for block G*/P* going up; 2 for the top-level carries; 2 per level for internal carries going down; 1 for the XOR.
* **Misuse:** ignoring the sum XOR or using the same 2-delay twice at the top level.

### B7. Prefix-operator and the Θ(log n) bound (fan-in ≤ 2)

```
(G_hi, P_hi) ∘ (G_lo, P_lo) = ( G_hi + P_hi·G_lo , P_hi·P_lo )          associative
T(n) = 1 + 2·⌈log₂ n⌉ + 1 = 2 + 2⌈log₂ n⌉          (MSB sum, C0 as an extra operand)
lower bound on depth of S(n−1) :  d ≥ ⌈log₂(2n + 1)⌉          (it depends on 2n + 1 inputs)
```

* **Example:** n = 100: ⌈log₂100⌉ = 7 → T = 16; ripple 200. n = 128: 16 vs lower bound 9.
* **Why:** associativity ⇒ balanced tree of depth ⌈log₂ m⌉; each ∘ is AND then OR = 2 delays. A fan-in-2 gate tree of depth d sees at most 2ᵈ inputs.
* **Misuse:** claiming Θ(1) (needs unbounded fan-in) or Θ(n) (that is ripple).

### B8. Asymptotic summary

| Adder | Order |
|---|---|
| Ripple | Θ(n) |
| Carry-skip / carry-select, equal blocks | Θ(√n) |
| Lookahead, fan-in ≤ 2 | Θ(log n) |
| Lookahead, unbounded fan-in (idealised) | Θ(1) |

### B9. Carry-select delay, equal blocks

```
T ≈ b·t_c + (n/b − 1)·t_m          b* = √(n·t_m / t_c)          T_min ≈ 2√(n·t_c·t_m) − t_m
```

* **Example:** n = 16, t_c = 2, t_m = 2, b = 4: 8 + 3·2 = 14. Check b* = 4, T_min = 14.
* **Unequal blocks:** `C(next) = max(block ready time, previous carry) + t_m`. Blocks 4,4,6,10 (n = 24): 8, 10, 14, 22; six blocks of 4: 18.
* **Misuse:** applying the formula when blocks differ in size or when the first block has a different structure.

---

## C. Subtraction, overflow, flags

### C1. Adder/subtractor

`B' = B ⊕ M` (bitwise), `C0 = M`; M = 1 gives A + ~B + 1 = A − B.

### C2. Overflow and carry

```
Signed overflow (addition or subtraction) :  V = C(n−1) ⊕ C(n)
   addition      : V = 1 iff operands have equal sign and the result's sign differs
   subtraction A−B: V = 1 iff operands have different sign and the result's sign differs from A's
Unsigned overflow of an addition : C(n) = 1
Unsigned borrow after A − B (computed as A + ~B + 1) : borrow = NOT C(n) ; equivalently A < B ⟺ raw C(n) = 0
```

* **Example (8-bit):** 0x7F + 0x01: result 0x80, C = 0, V = 1. 0xFF + 0x01: 0x00, C = 1, V = 0. 0xC8 + 0x90: 0x58, C = 1, V = 1. 0x80 − 0x01: 0x7F, raw C = 1, V = 1.
* **Misuse:** using carry-out for signed overflow; using sign of the result when operands have opposite signs.

### C3. Flags

```
Z = NOR(result bits)       N = result MSB       C = carry-out (convention for subtraction must be stated)       V = C(n−1) ⊕ C(n)
```

### C4. Comparison after A − B

```
signed   A <  B : N ⊕ V = 1                 A ≤ B : Z + (N ⊕ V) = 1       A > B : ¬Z · ¬(N ⊕ V)
unsigned A <  B : raw C = 0   (or C = 1 if C is a borrow flag)               A = B : Z = 1
```

* **Why:** without overflow N is the true sign; with overflow it is inverted. Raw carry-out is 1 iff A + (2ⁿ − B) ≥ 2ⁿ iff A ≥ B.
* **Example:** 0x80 − 0x01 → N = 0, V = 1 ⇒ signed A < B; raw C = 1 ⇒ unsigned A ≥ B.
* **Misuse:** reading N alone for signed compare; reading C alone for signed compare.

---

## D. ALU organisation

### D1. Operation count

A k-bit function-select field encodes at most 2ᵏ operations (4 bits → 16).

### D2. Arithmetic unit via B-conditioning

```
Y = 0, B, ~B or all-ones (2-bit select);  result = A + Y + Cin
(Y=0, Cin=0) A   (Y=0, Cin=1) A+1   (Y=B,0) A+B   (Y=B,1) A+B+1
(Y=~B,0) A−B−1   (Y=~B,1) A−B       (Y=1…1,0) A−1  (Y=1…1,1) A
```

* **Example:** A = 0x35, B = 0x12: A−B = 0x23, A−B−1 = 0x22, A−1 = 0x34.

---

## E. Shifts

```
logical left by k    : x·2ᵏ mod 2ⁿ (unsigned)          signed left shift valid iff top k+1 bits are all equal
arithmetic right by k: ⌊x / 2ᵏ⌋ (rounds toward −∞)       logical right: ⌊x / 2ᵏ⌋ for unsigned only
barrel shifter       : stages = ⌈log₂ n⌉ ; muxes = n·⌈log₂ n⌉ ; delay = ⌈log₂ n⌉·t_mux  (independent of shift amount)
```

* **Example:** 8-bit −44 (0xD4) ASR 2 = −11 (0xF5); LSR gives 53 (wrong). −7 ASR 1 = −4 (C division gives −3). 16-bit 0xFA3C (−1476) << 2 = 0xE8F0 = −5904 (valid). 8-bit 0x50 << 1 = 0xA0 = −96 (overflow).
* **Example:** 32-bit barrel: 160 muxes; 64-bit at 0.35 ns/stage: 6·0.35 = 2.1 ns. Shift by 11 uses the 8-, 2- and 1-place stages.
* **Multiply by 10:** (x << 3) + (x << 1).

---

## F. Multiplication

### F1. Sequential shift-and-add (n×n unsigned)

```
n iterations ; add when Q0 = 1 ; shift A:Q right ; product = A:Q (2n bits)
time = n·(t_add + t_shift)  if both always executed in series
cycles = n shifts + (#1s in Q) adds   if an add costs its own cycle and only happens when Q0 = 1
```

* **Example:** 13 × 11, n = 4: 3 additions, product 143. 16 iterations × (5 + 2) ns = 112 ns; combinational 40 ns → sequential 72 ns slower. 24-bit, 9 ones, 1 cycle per add and per shift: 24 + 9 = 33 cycles.
* **Misuse:** forgetting the product needs 2n bits.

### F2. Booth radix-2

```
pair (Q0, Q−1):  10 → A−M ;  01 → A+M ;  00 or 11 → none ; then arithmetic shift right of A:Q:Q−1  (n steps)
#add/sub = number of bit changes in the string  q(n−1) … q0 0
weight of M at step i = q(i−1) − q(i)
```

* **Example:** Q = 0111 0010 → 4 operations; 0101 0101 → 8 (worst, = n); 1111 1111 → 1; 0 → 0; 0111 0 → 2.
* **Edge:** M = −2ⁿ⁻¹ needs an (n+1)-bit accumulator.

### F3. Booth radix-4 digits

`d(i) = −2·q(2i+1) + q(2i) + q(2i−1)`, Q = Σ d(i)·4ⁱ, n/2 partial products, #ops = #non-zero digits.

* **Example:** Q = 0111 0010 → digits (low first) −2, +1, −1, +2.

---

## G. Division

```
restoring     : n steps ; each: shift, subtract, if negative restore.  ≤ 2n add/sub ;  restores = #zero quotient bits (when quotient fits n bits)
non-restoring : n steps, one add/sub each ; final remainder correction (+M) if A < 0 :  n or n + 1 add/sub
dividend = quotient × divisor + remainder
```

* **Example:** 45 ÷ 7, n = 6: quotient 6 (000110), remainder 3; restoring uses 6 + 4 = 10 add/sub. 13 ÷ 3, n = 4: non-restoring A = −2, 0, −3, −2 then correction → remainder 1; 5 add/sub.

---

## H. Floating point (ALU level)

```
single : 1|8|23, bias 127, value (−1)^s·1.f·2^(e−127), 24-bit significand
double : 1|11|52, bias 1023, 53-bit significand
add/sub: align (shift smaller right by Δe) → add/sub significands → normalise → round → check overflow/underflow
multiply: s = sX ⊕ sY ; e = eX + eY − bias ; significand product (24×24 → 48) ; normalise (≤ 1 right shift) ; round
ulp(x) = 2^(exponent − 23) (single)
```

* **Example:** 52 + 4.5: Δe = 3 → 1.110001 × 2⁵ = 56.5 (single: 0x42620000). 12 × 0.3125: exponent 130 + 125 − 127 = 128 (true 1), significand 1.875 → 3.75.
* **Example:** (2²⁴ + 1) + 1 = 2²⁴ but 2²⁴ + (1 + 1) = 2²⁴ + 2 in single precision. x = 1.5·2¹⁰, y = 2⁻¹⁴: Δe = 24, y = ½ ulp(x), tie to even → x + y = x.
* **Misuse:** subtracting the bias twice (or not at all) in multiplication; treating float addition as associative.

---

## I. Data path

```
single-bus ADD Rd, Rs (1-cycle memory read, PC incremented in parallel) :
   PCout,MARin,Read | MDRout,IRin | Rdout,Yin | Rsout,ADD,Zin | Zout,Rdin    = 5 steps
2-cycle memory read: +1 (wait) = 6 steps       3-bus data path: execute phase = 1 step
```

* **Rules:** one bus source per step; Y (TEMP1) must hold operand 1 before the ALU step; result goes to Z (TEMP2) then to the destination in the next step; fetch chain PC → MAR → (memory) → MDR → IR precedes all execute steps.
* **Misuse:** swapping operands of SUB; combining two bus sources in one step.
