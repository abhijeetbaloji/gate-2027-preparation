# Local Optimisation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Arithmetic in these questions is ordinary integer arithmetic. A variable mentioned in a simplification has no side effect. Division by an expression that might be zero is not simplified.

## Level 1 — Conceptual

## Q1 — MCQ

Constant folding is the replacement of

A. `x = 2 * 8` by `x = 16` at compile time
B. a local variable by a machine register
C. a loop by an equivalent recursive procedure
D. every call by an inlined copy of the callee

---

## Q2 — MSQ

Which algebraic simplifications are valid for integer values with no side effects? Select all that apply.

A. `x + 0` simplifies to `x`
B. `x * 1` simplifies to `x`
C. `x * 0` simplifies to `0`
D. `x - x` simplifies to `1`

---

## Q3 — MCQ

Which transformation is strength reduction?

A. Replacing a multiplication by a loop-invariant constant, such as the address step `i * 4`, by a repeated addition of that constant
B. Replacing an addition by a multiplication
C. Replacing a constant operand by a variable
D. Splitting one basic block into two blocks at a label

---

## Level 2 — Standard GATE Style

## Q4 — NAT

Fold `x = (3 + 4) * 2 - 5` completely. What integer is stored in `x`? Enter an integer.

---

## Q5 — MCQ

After algebraic simplification, `a = b * 1 + 0` becomes

A. `a = b`
B. `a = 0`
C. `a = 1`
D. `a = b + 1`

---

## Q6 — MSQ

Which transformations can be decided from the instructions of a single basic block, without a data-flow solution on the whole control-flow graph? Select all that apply.

A. Folding the constants in `x = 4 + 5`
B. Replacing `y = z * 1` by `y = z`
C. Moving a computation out of a loop after proving, from every path into the loop, that its operands are invariant
D. Replacing `x = x + 0` by deleting the addition

---

## Level 3 — Multi-Step

## Q7 — NAT

The block is optimised by constant folding and algebraic simplification.

```
x = 2 * 5
y = x + 0
z = y * 1 + 3
```

What integer is `z` afterward? Enter an integer.

---

## Q8 — MCQ

Inside a loop the address step is `t = i * 4`, and the loop adds 1 to `i` on every iteration. Strength reduction introduces an induction variable for `t`. Which update replaces the multiplication?

A. `t = t * 4`
B. `t = t + 4`
C. `t = t + 1`
D. `t = i * 4`

---

## Level 4 — Tricky / Trap-Based

## Q9 — MCQ

Which transformation is not always safe for integers?

A. `x + 0` \(\to\) `x`
B. `x * 1` \(\to\) `x`
C. `x / x` \(\to\) `1`
D. `x - 0` \(\to\) `x`

---

## Q10 — MSQ

Local folding and algebraic simplification are applied to the block.

```
a = 8
b = a * 2
c = b + 0
d = c - c
e = d + 5
```

Select all that apply.

A. `b` can be replaced by the constant 16.
B. `c` can be replaced by the constant 16.
C. `d` can be replaced by the constant 0.
D. `e` can be replaced by the constant 0.

---

## Level 5 — Challenge

## Q11 — NAT

Fold and simplify the block as far as the integer identities allow.

```
t1 = 2 + 3
t2 = t1 * 4
t3 = t2 - t1
t4 = t3 * 0 + 7
```

What integer is `t4`? Enter an integer.

---

## Q12 — MCQ

The two instructions are folded, then the addition is folded.

```
k = 2 * 8
m = k + k
```

What is `m`?

A. 16
B. 18
C. 32
D. 64

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | MCQ | A |
| 4 | NAT | 9 |
| 5 | MCQ | A |
| 6 | MSQ | A, B, D |
| 7 | NAT | 13 |
| 8 | MCQ | B |
| 9 | MCQ | C |
| 10 | MSQ | A, B, C |
| 11 | NAT | 7 |
| 12 | MCQ | C |

## Detailed Solutions

### Q1

Answer: A

Constant folding evaluates an operator whose operands are compile-time constants and replaces the instruction by the result. Here \(2 \times 8 = 16\), so the store of `x` becomes a constant store. Allocating a register is register allocation. Turning a loop into recursion is a change of control structure, not folding. Inlining is a different interprocedural transformation, and it is not applied to every call.

### Q2

Answer: A, B, C

For integers, adding zero and multiplying by one do not change the value, and multiplying by zero yields zero. The difference `x - x` is 0, not 1. D uses the identity for division by a nonzero value, or simply the wrong constant, and it is not valid.

### Q3

Answer: A

Strength reduction replaces an expensive operator by a cheaper one that produces the same sequence of values. If `i` increases by 1, then `i * 4` increases by 4, so a running `t` can be updated with `t = t + 4` instead of a multiplication. Replacing addition by multiplication makes the operator more expensive. Replacing a constant by a variable is not a reduction. Splitting a block is a control-flow edit, not an operator-strength change.

### Q4

Answer: 9

\[
(3 + 4) \times 2 - 5 = 7 \times 2 - 5 = 14 - 5 = 9.
\]

The parentheses force the addition before the multiplication. Folding left to right without them would be a different expression.

### Q5

Answer: A

`b * 1` simplifies to `b`, and `b + 0` simplifies to `b`. The assignment is `a = b`. Replacing the whole right-hand side by 0 would require a multiplication by zero, which is not present. The constant 1 is an operand, not the result.

### Q6

Answer: A, B, D

Both operands of `4 + 5` are constants written in the same instruction, so folding is local. The identity `z * 1 = z` is visible in that one instruction. Adding zero is likewise local; if this `x = x + 0` is the whole use, the addition can be deleted inside the block. Hoisting a loop-invariant computation is not local: invariance means every path into the loop leaves the operands unchanged, which is a property of the control-flow graph, not of one block’s text.

### Q7

Answer: 13

Fold `2 * 5` to 10, so `x` is 10. Then `y = 10 + 0` simplifies to 10. Then `z = 10 * 1 + 3 = 10 + 3 = 13`. Stopping after `y = x + 0` and forgetting to fold `x` would leave `z` symbolic; the block defines `x` by a constant expression, so the constant propagates through the local simplification.

### Q8

Answer: B

If `t` holds \(i \times 4\) at the start of an iteration and `i` grows by 1, the next product is \((i + 1) \times 4 = t + 4\). The multiplication disappears and the update is `t = t + 4`, with `t` initialised to the product for the first index. Adding 1 would track `i`, not the byte address. Leaving `t = i * 4` does not reduce the strength. Multiplying `t` by 4 again would scale by 16.

### Q9

Answer: C

`x / x` equals 1 only when `x` is not 0. When `x` is 0 the division is undefined, so a compiler may not rewrite it to 1. Adding or subtracting 0, and multiplying by 1, are identities for every integer, including 0. The trap is to treat every “cancel the variable” pattern as an algebraic identity; cancellation of a divisor needs a nonzero operand.

### Q10

Answer: A, B, C

`a` is 8, so `b = 8 * 2 = 16`. Adding 0 leaves `c = 16`. Then `d = 16 - 16 = 0`. Then `e = 0 + 5 = 5`. The constant 0 is the value of `d`, not of `e`. Replacing `e` by 0 drops the final addition of 5. A, B, and C are true; D is false.

### Q11

Answer: 7

\[
\begin{align*}
t_1 &= 2 + 3 = 5, \\
t_2 &= 5 \times 4 = 20, \\
t_3 &= 20 - 5 = 15, \\
t_4 &= 15 \times 0 + 7 = 0 + 7 = 7.
\end{align*}
\]

The multiplication by zero folds the copied value of `t3` away, but the added constant 7 remains. An algebraic pass may rewrite `t3 * 0 + 7` directly to 7 once it knows the multiplication has no side effect. Either route stores 7.

### Q12

Answer: C

\(2 \times 8 = 16\), so `k` is 16. Then `m = 16 + 16 = 32`. Using `k` only once gives 16. Multiplying the folded `k` by 4, or doubling 32 again, gives 64. The instruction is an addition of the two copies of the folded constant, so the stored value is 32.
