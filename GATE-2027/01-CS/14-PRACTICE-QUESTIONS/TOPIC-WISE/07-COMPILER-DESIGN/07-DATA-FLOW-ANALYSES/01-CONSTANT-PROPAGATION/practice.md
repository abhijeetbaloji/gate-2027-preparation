# Constant Propagation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Each variable’s abstract value is UNDEF, a single integer, or NAC (not a constant). UNDEF means “no assignment has constrained this variable yet.” NAC means “at least two different constants reach this point.” The meet at a control-flow join is

- UNDEF \(\sqcap\) \(v = v\),
- \(c \sqcap c = c\),
- \(c \sqcap d =\) NAC when \(c \neq d\),
- NAC \(\sqcap\) \(v =\) NAC.

UNDEF is the top element used to initialise OUT of every block. A definition `x = c` sets `x` to the constant \(c\). A definition `x = y + z` is constant only when both operands are the same known constants; otherwise, if either operand is NAC, the result is NAC. The analysis is forward and is iterated to a fixed point. No loop is unrolled.

## Level 1 — Conceptual

## Q1 — MCQ

Constant propagation, as a data-flow problem on a control-flow graph, is

A. a forward analysis
B. a backward analysis, like liveness
C. a peephole that may inspect only one instruction and may not use the instruction before it
D. a synonym of available-expressions analysis

---

## Q2 — MSQ

Using the meet above, which equations are true? Select all that apply.

A. \(5 \sqcap 5 = 5\)
B. \(5 \sqcap 7 =\) NAC
C. UNDEF \(\sqcap\) \(4 = 4\)
D. NAC \(\sqcap\) \(4 = 4\)

---

## Q3 — NAT

Inside one basic block the statements are

```
a = 2
b = a + 3
c = b * a
```

After constant propagation and folding, what integer is `c`? Enter an integer.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Block B1 contains `x = 4` and goes to B3. Block B2 contains `x = 4` and goes to B3. Block B3 contains `y = x + 1`. No other assignment to `x` reaches B3. The value of `x` at the entry of B3 is

A. the constant 4
B. NAC
C. UNDEF
D. the constant 5

---

## Q5 — MCQ

Change B2 in Q4 so that it contains `x = 9` instead of `x = 4`. B1 still contains `x = 4`. At the entry of B3,

A. `y` folds to the constant 5
B. `x` is NAC, so `y = x + 1` is not a compile-time constant
C. `x` is the constant 4
D. `x` is the constant 9

---

## Q6 — NAT

One basic block, executed from top to bottom, is

```
x = 3
y = x + x
x = y - 1
z = x * 2
```

After propagation and folding, what integer is `z` at the end of the block? Enter an integer.

---

## Level 3 — Multi-Step

## Q7 — MSQ

At the exit of the block below, which constant facts hold? Select all that apply.

```
a = 1
b = 2
c = a + b
a = c
b = a + 1
```

A. `a` is the constant 3
B. `b` is the constant 4
C. `c` is the constant 3
D. `a` is the constant 1

---

## Q8 — MCQ

The control-flow graph has two blocks. B1 is `i = 0; s = 0` and goes only to B2. B2 is `s = s + i; i = i + 1` and has edges to itself and to the exit. OUT of every block starts as UNDEF for both variables, and the equations are iterated to a fixed point. How many of the variables \(\{ i, s \}\) are constants at the entry of B2?

A. 0
B. 1
C. 2
D. 3

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Entry goes to B2 and to B3, and both go to B4. Every variable starts as UNDEF at entry. B2 is the assignment `x = 5`. B3 is the assignment `y = 1` and does not mention `x`. B4 reads `x`. Using the meet defined above, `x` at the entry of B4 is

A. the constant 5
B. NAC
C. UNDEF
D. the constant 0

---

## Q10 — MSQ

One path into a join assigns `x = 2` and `y = 3`. The other path assigns `x = 2` and `y = 8`. Neither path leaves a variable at UNDEF. Which facts hold at the join? Select all that apply.

A. `x` is the constant 2
B. `y` is NAC
C. `x` is NAC
D. `y` is the constant 3

---

## Level 5 — Challenge

## Q11 — NAT

Propagation must respect the order of assignments inside the block.

```
a = 4
b = a - 1
a = b + b
c = a + b
```

What integer is `c`? Enter an integer.

---

## Q12 — MCQ

B1 is `x = 2` and branches to B2 and B3. B2 is `x = x + 1`. B3 is `x = 2`. B2 and B3 both go to B4, whose first use is `y = x`. At B4, the propagated value of `y` is

A. the constant 2
B. the constant 3
C. NAC
D. UNDEF

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 10 |
| 4 | MCQ | A |
| 5 | MCQ | B |
| 6 | NAT | 10 |
| 7 | MSQ | A, B, C |
| 8 | MCQ | A |
| 9 | MCQ | A |
| 10 | MSQ | A, B |
| 11 | NAT | 9 |
| 12 | MCQ | C |

## Detailed Solutions

### Q1

Answer: A

Constant information is produced by assignments and consumed by later uses, so values flow from earlier blocks to later blocks. The analysis is forward. Liveness is the backward analysis. A peephole on one instruction can fold `2 + 3`, but constant propagation also carries a constant from one instruction, and from one block, into later uses. Available expressions track which expressions have already been computed, not which variables hold a known integer.

### Q2

Answer: A, B, C

The same constant meets itself and stays that constant, so \(5 \sqcap 5 = 5\). Two different constants are not a single constant, so \(5 \sqcap 7 =\) NAC. UNDEF is the identity of meet: a path that has not constrained `x` does not disagree with a path that has set `x` to 4. NAC is the bottom element. It meets everything, including 4, to NAC. D would say that a non-constant becomes a constant when it meets one constant, which is the opposite of a safe meet.

### Q3

Answer: 10

`a` is the constant 2. Then `b = 2 + 3 = 5`. Then `c = 5 * 2 = 10`. All three right-hand sides are constant, and nothing redefines `a` or `b` before they are used.

### Q4

Answer: A

OUT of B1 maps `x` to 4, and OUT of B2 maps `x` to 4. The meet at B3 is \(4 \sqcap 4 = 4\). Both branches agree, so the assignment is still a constant after the join. NAC would be the result only if the two constants differed. UNDEF would be the result only if neither branch assigned `x`. The `+ 1` is applied in B3; it is not the value of `x` on entry.

### Q5

Answer: B

The meet is now \(4 \sqcap 9 =\) NAC. A later use of `x` cannot be folded, so `y = x + 1` is not a compile-time constant. Choosing 4 or 9 keeps one branch and drops the other. Choosing 5 folds `4 + 1` and ignores the branch that carries 9.

### Q6

Answer: 10

The first assignment sets `x` to 3. Then `y = 3 + 3 = 6`. The third instruction defines `x` again: `x = 6 - 1 = 5`. The old constant 3 is dead after that definition. Then `z = 5 * 2 = 10`. Using the first value of `x` in the last instruction computes \(3 \times 2 = 6\) and misses the kill.

### Q7

Answer: A, B, C

Work down the block.

- `a = 1` and `b = 2`.
- `c = 1 + 2 = 3`.
- `a = c` sets `a` to 3. The earlier constant 1 no longer holds.
- `b = a + 1 = 3 + 1 = 4`.

At the exit, `a` is 3, `b` is 4, and `c` is 3. The fact `a = 1` was true only between the first and fourth instructions. D describes that killed value.

### Q8

Answer: A

Write pairs as \((i, s)\). OUT[B1] is \((0, 0)\) after the first evaluation, because B1 defines both variables. Initialise OUT[B2] to (UNDEF, UNDEF).

- Entry of B2 is OUT[B1] \(\sqcap\) OUT[B2] = \((0, 0) \sqcap\) (UNDEF, UNDEF) = \((0, 0)\). The body sets `s = 0 + 0 = 0` and `i = 0 + 1 = 1`, so OUT[B2] becomes \((1, 0)\).
- Entry of B2 is \((0, 0) \sqcap (1, 0) =\) (NAC, \(0\)). Then `s = NAC + 0 =` NAC and `i = NAC + 1 =` NAC, so OUT[B2] becomes (NAC, NAC).
- Entry of B2 is \((0, 0) \sqcap\) (NAC, NAC) = (NAC, NAC). The transfer leaves OUT[B2] at (NAC, NAC).

The fixed point at the entry of B2 has neither variable constant. The back edge destroys the constant 0 that the first iteration temporarily gave `s`. The count is 0. Unrolling the three iterations of a concrete bound is a different optimisation; this question does not unroll.

### Q9

Answer: A

At entry, `x` is UNDEF. B2 sets `x` to 5, so OUT[B2] has `x = 5`. B3 does not assign `x`, so it forwards the entry value and OUT[B3] has `x =` UNDEF. The meet at B4 is

\[
5 \sqcap \mathrm{UNDEF} = 5.
\]

UNDEF does not mean “some other runtime value.” It means this abstract path has not produced a conflicting constant. The trap is to treat the path through B3 as if it carried NAC, or as if “not assigned on every path” automatically meant “not a constant.” That would be correct if `x` had entered the procedure already at NAC, for example as an unknown parameter. The question initialises it to UNDEF, so the meet with 5 is 5.

### Q10

Answer: A, B

Both paths set `x` to 2, so \(2 \sqcap 2 = 2\). The paths set `y` to 3 and to 8, so \(3 \sqcap 8 =\) NAC. The join does not keep a variable constant just because one path’s constant is attractive, and it does not discard a variable that both paths set to the same constant. C and D each take one of those two mistakes.

### Q11

Answer: 9

- `a = 4`.
- `b = 4 - 1 = 3`.
- `a = 3 + 3 = 6`. This kills the constant 4.
- `c = 6 + 3 = 9`.

The use of `a` in `c = a + b` sees 6, while the use of `b` still sees 3. Adding the original `a` instead of the redefined `a` produces \(4 + 3 = 7\), which is the result of ignoring the third instruction.

### Q12

Answer: C

B1 sets `x` to 2 on the way into both branches. B2 replaces it by \(2 + 1 = 3\). B3 replaces it by 2. At B4 the meet is \(3 \sqcap 2 =\) NAC, so `y = x` does not fold. The constant 2 from B1 does not survive both branches, because B2 modifies it. The constant 3 describes only the B2 path. UNDEF would mean neither branch had defined `x`.
