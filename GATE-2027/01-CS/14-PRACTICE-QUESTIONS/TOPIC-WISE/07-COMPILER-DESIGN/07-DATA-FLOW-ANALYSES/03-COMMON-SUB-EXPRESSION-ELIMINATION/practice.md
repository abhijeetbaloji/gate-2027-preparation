# Common Subexpression Elimination — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

An expression `x op y` is available at a point when every path from the entry to that point evaluates `x op y`, and neither operand is redefined between the last evaluation on that path and the point. The data-flow is forward. The value on the entry edge is the empty set. At a join, the incoming sets are intersected: the expression must arrive on all paths, not merely on one path. A later occurrence of an available expression is redundant and may be replaced by a temporary that already holds the value. Assume integer operands and no side effects.

## Level 1 — Conceptual

## Q1 — MCQ

Common-subexpression elimination may delete an evaluation of `b + c` at a point only when

A. `b + c` is available there: every path from the entry evaluates it and does not later redefine `b` or `c`
B. `b + c` is evaluated on at least one path from the entry
C. `b` and `c` are live
D. `b` and `c` are compile-time constants

---

## Q2 — MSQ

Select all that apply.

A. Available-expressions analysis is a forward analysis.
B. The sets arriving at a join are combined by intersection.
C. The sets arriving at a join are combined by union.
D. A redundant evaluation can be replaced by a use of a temporary that already holds the value.

---

## Level 2 — Standard GATE Style

## Q3 — NAT

The block is

```
t1 = b + c
t2 = b + c
a = t2
```

Nothing defines `b` or `c` inside the block. After common-subexpression elimination, how many evaluations of `b + c` remain? Enter an integer.

---

## Q4 — MCQ

The block is

```
b = 1
t1 = b + c
b = 2
t2 = b + c
```

Which statement is true?

A. The evaluation that defines `t2` is redundant.
B. The evaluation that defines `t2` is not redundant.
C. Both evaluations of `b + c` can be deleted.
D. The evaluation that defines `t1` is redundant.

---

## Q5 — MSQ

The block is

```
a = b * c
d = b * c
b = b + 1
e = b * c
```

Select all that apply.

A. The evaluation in `d = b * c` is redundant.
B. The evaluation in `e = b * c` is redundant.
C. `b * c` is available immediately before `e = b * c`.
D. `b * c` is available immediately before `d = b * c`.

---

## Level 3 — Multi-Step

## Q6 — MCQ

The entry edge reaches both \(B_2\) and \(B_3\). Both of those blocks go to \(B_4\). The blocks are

```
B2: t = a + b
B3: u = c + d
B4: v = a + b
```

No block defines `a`, `b`, `c`, or `d`. At the entry of \(B_4\), the expression `a + b` is

A. available, because \(B_2\) evaluates it
B. not available
C. available, because intersection keeps every expression evaluated anywhere
D. a constant

---

## Q7 — MCQ

Using the graph and the blocks of Q6, how many of the expressions \(\{ a + b,\ c + d \}\) are available at the entry of \(B_4\)?

A. 0
B. 1
C. 2
D. 3

---

## Level 4 — Tricky / Trap-Based

## Q8 — MCQ

A solver uses union instead of intersection at the join of Q6 and reports that `a + b` is available at the entry of \(B_4\). What is wrong with that report?

A. Nothing; one path that evaluates `a + b` is enough.
B. Availability demands the expression on every path, so the join must intersect. The path through \(B_3\) does not evaluate `a + b`, and `a + b` is not available at \(B_4\).
C. Available-expressions analysis runs backward from the exit.
D. Computing `c + d` in \(B_3\) kills `a + b`.

---

## Q9 — MSQ

Change \(B_3\) in the graph of Q6 to `u = a + b`. Blocks \(B_2\) and \(B_3\) still do not define `a` or `b`, and \(B_4\) is still `v = a + b`. Select all that apply.

A. `a + b` is available at the entry of \(B_4\).
B. The evaluation `v = a + b` is redundant.
C. `c + d` is available at the entry of \(B_4\).
D. An evaluation of `a + b` on each path into \(B_4\), with no later definition of `a` or `b`, is enough to reuse the value in \(B_4\).

---

## Level 5 — Challenge

## Q10 — NAT

The block below is reached with no expression available. How many of the seven instructions contain a redundant evaluation? Enter an integer.

```
(1) t1 = a + b
(2) t2 = c * d
(3) t3 = a + b
(4) c = 1
(5) t4 = c * d
(6) t5 = a + b
(7) t6 = a + b
```

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | A |
| 2 | MSQ | A, B, D |
| 3 | NAT | 1 |
| 4 | MCQ | B |
| 5 | MSQ | A, D |
| 6 | MCQ | B |
| 7 | MCQ | A |
| 8 | MCQ | B |
| 9 | MSQ | A, B, D |
| 10 | NAT | 3 |

## Detailed Solutions

### Q1

Answer: A

Elimination is safe only when the earlier value is the same on every path. That is the definition of availability: the expression was evaluated, and neither operand changed afterward. A single path is not enough, because another path may reach the same point without that value. Liveness says a variable will be used; it does not say an expression was already computed. Constant propagation is a different analysis. An expression of two variables can be redundant without either variable being a constant.

### Q2

Answer: A, B, D

Computations generate availability that flows forward to later instructions, so the analysis is forward. At a join the expression is available only if it is available along every predecessor, which is an intersection. Union would keep an expression that is missing on some path and would make the later deletion unsafe. When the expression is available, the compiler can keep the first value in a temporary and replace the redundant operator by a copy or a use of that temporary.

### Q3

Answer: 1

The first instruction evaluates `b + c` and neither operand is redefined. The expression is available at the second instruction, so `t2 = b + c` is redundant. One legal result is `t1 = b + c` followed by `t2 = t1` and `a = t2`, which still evaluates `b + c` once. Deleting both evaluations would leave no value to store.

### Q4

Answer: B

The first `b + c` uses the `b` defined by `b = 1`. The assignment `b = 2` kills every available expression that mentions `b`. The second `b + c` therefore sees a different `b` and must be evaluated. It is not redundant. The first evaluation is the one that creates the value; nothing before it has computed `b + c`, so it is not redundant either. Deleting both would drop the only computations of the two different sums.

### Q5

Answer: A, D

After `a = b * c`, the expression `b * c` is available, and `d = b * c` uses the same operands. That evaluation is redundant, so A and D are true. The next instruction, `b = b + 1`, defines `b` and kills `b * c`. Immediately before `e = b * c` the expression is not available, so the evaluation of `e` is not redundant. B and C are false.

### Q6

Answer: B

The entry edge carries no available expression. Along the path through \(B_2\), `a + b` is generated and neither operand is killed, so OUT[\(B_2\)] contains `a + b`. Along the path through \(B_3\), the block generates `c + d` and does not generate `a + b`, so OUT[\(B_3\)] does not contain `a + b`. The entry of \(B_4\) is the intersection of those two sets, which does not contain `a + b`. The evaluation in \(B_2\) covers only one path. Intersection does not retain an expression that is missing from either input, so C describes union rather than intersection. Nothing shows that `a + b` is a constant.

### Q7

Answer: A

By the same intersection, `a + b` is missing from the \(B_3\) path and `c + d` is missing from the \(B_2\) path. Neither expression is in OUT[\(B_2\)] \(\cap\) OUT[\(B_3\)]. The count is 0. Each expression is available at the exit of the block that computes it, but the question asks for the join at the entry of \(B_4\).

### Q8

Answer: B

Union of OUT[\(B_2\)] and OUT[\(B_3\)] does contain `a + b`, because \(B_2\) computes it. That is the wrong confluence operator. A use in \(B_4\) is reached by the path entry \(\to B_3 \to B_4\), and that path never evaluates `a + b`. Replacing `v = a + b` by a temporary created only in \(B_2\) would read an undefined temporary on the \(B_3\) path. Computing `c + d` defines `u`, not `a` or `b`, so it does not kill `a + b`. The analysis is forward. The error is specifically the use of union where availability needs every path.

### Q9

Answer: A, B, D

Both predecessors now generate `a + b` and neither defines `a` or `b`. OUT[\(B_2\)] and OUT[\(B_3\)] both contain `a + b`, so their intersection does too. The evaluation `v = a + b` is redundant and can reuse a temporary assigned on both paths. The expression `c + d` is not computed in either block, so it is not available. D is the all-paths condition that this modified graph satisfies and that the original graph in Q6 does not.

### Q10

Answer: 3

Track the available set, starting from empty. An instruction is redundant when its expression is already in the set.

| Instruction | Expression available before it? | Effect |
| --- | --- | --- |
| (1) `t1 = a + b` | no | generate `a + b` |
| (2) `t2 = c * d` | no | generate `c * d`; `a + b` stays |
| (3) `t3 = a + b` | yes | redundant; set unchanged |
| (4) `c = 1` | | kill `c * d`; `a + b` stays, because `a` and `b` are not defined |
| (5) `t4 = c * d` | no | not redundant; generate `c * d` again |
| (6) `t5 = a + b` | yes | redundant |
| (7) `t6 = a + b` | yes | redundant |

The redundant instructions are (3), (6), and (7). That is 3. Instruction (5) looks like a copy of (2), but (4) has redefined `c`, so the product is a new value. Instruction (1) and instruction (2) are the first evaluations of their expressions.
