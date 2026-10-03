# Arithmetic and Logic Unit — Last-minute Revision

Full theory: [NOTES.md](NOTES.md) · formulas: [FORMULAS.md](FORMULAS.md) · traps: [MISTAKES.md](MISTAKES.md)

## Must-remember definitions

* Full adder: S = A⊕B⊕Cin, Cout = AB + Cin(A⊕B). Generate G = AB, propagate P = A⊕B, C(i+1) = Gi + Pi·Ci, Si = Pi⊕Ci.
* Subtract: A − B = A + ~B + 1 (XOR on B with M, carry-in M).
* Flags: Z = result all 0; N = result MSB; C = carry-out; **V = C(n−1) ⊕ C(n)**.
* Unsigned add overflow = C. Signed add overflow = V (= same-sign operands, different-sign result).
* After A − B, raw carry-out 1 ⟺ A ≥ B unsigned (no borrow). If the ISA's C is a borrow flag, C = NOT raw carry.

## Compare after A − B

```
            signed             unsigned (raw C)    unsigned (C = borrow)
A <  B      N⊕V = 1            C = 0               C = 1
A ≥ B       N⊕V = 0            C = 1               C = 0
A ≤ B       Z + (N⊕V)          C = 0 or Z          C = 1 or Z
A =  B      Z = 1
```

## Adder delay classes

```
ripple Θ(n)   | carry-skip, carry-select (equal blocks) Θ(√n) | CLA with fan-in ≤ 2: Θ(log n) | CLA with unbounded fan-in: Θ(1)
ripple (gate-delay model) = 2n       fan-in-2 prefix adder = 2 + 2⌈log₂ n⌉       4-bit-unit CLA with L levels = 4L
lower bound for fan-in 2: depth ≥ ⌈log₂(2n+1)⌉
```

## Shifts and multiplication

```
LSL ×2ᵏ (check overflow) | LSR for unsigned only | ASR = ⌊x/2ᵏ⌋ (toward −∞): −7>>1 = −4
barrel shifter: log₂n stages, n·log₂n 2:1 muxes, delay log₂n mux delays
shift-add: n iterations (add if Q0 = 1, then shift); time n(t_add + t_shift); product 2n bits
Booth: (Q0,Q−1) 10 → A−M, 01 → A+M, 11/00 none, then ASR; #ops = bit changes in (Q followed by 0); n shifts always
radix-4 Booth: n/2 steps, digits −2…+2, #ops = non-zero digits
```

## Division and floating point

```
restoring: shift, A−M, restore if <0 ; ≤ 2n add/sub ; restores = #zero quotient bits
non-restoring: shift, A∓M by sign of A ; n ops (+1 correction if A<0 at end)
FP add: align (smaller right by Δe) → add → normalise → round     FP mult: e = eX + eY − bias, 24×24 mantissa product
FP add is NOT associative: (2²⁴ + 1) + 1 = 2²⁴ ≠ 2²⁴ + (1+1) in single precision
```

## Data path (single bus)

```
PC→MAR, Read → (wait) → MDR→IR → R_a→Y → R_b + ALU→Z → Z→R_dest
one bus source per step; Y holds operand 1 (SUB = Y − bus); Z then destination; 3-bus: execute in 1 step
```

## Fast-solve checklist

1. Write n, representation, carry/borrow convention, delay model.
2. Add/sub: compute the n-bit pattern, then C (carry-out) and V (sign rule).
3. Compare: signed N⊕V, unsigned C — pick the convention.
4. Timing: draw the critical path (P/G → lookahead → carries → sum); the first section is not critical.
5. Booth: append 0, count changes. Division: count zero quotient bits for restores.
6. Data path: dependencies PC→MAR→MDR→IR first; operand 1 in Y before ALU step; result via Z.

## Top traps

* Carry-out ≠ signed overflow (0x7F+1: C=0, V=1; 0xFF+1: C=1, V=0).
* Signed less-than is N⊕V, not N.
* Logical shift on negative numbers; ASR rounds toward −∞.
* "Θ(1) for CLA" needs unbounded fan-in; fan-in 2 gives Θ(log n).
* Booth ops = transitions, not number of 1s; shift steps = n.
* 4-bit select = 16 operations.

## What the mapped PYQs test (no answers listed anywhere)

* 2016 CS-1 Q33: fan-in-2 carry-lookahead asymptotic delay.
* 2020 Q4: order of micro-steps for R0 ← R1 + R2 on a single-bus data path (figure garbled in the mapping).
* 2008 Q33: auto-increment (addressing-mode concept; misfiled here).
* Related ALU skills mapped under Digital Logic: overflow detection, ripple-carry latency, Booth operation count, left shift as multiplication, floating point.
