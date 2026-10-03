# Intermediate Code Generation — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the three-address instruction \(x = y\ \mathrm{op}\ z\), how many operands does the operator have?

A. 1
B. 2
C. 3
D. 4

---

## Q2 — MSQ

Which of the following are already three-address statements? Select all that apply.

A. `t1 = a + b`
B. `if t1 < t2 goto L`
C. `a = b + c * d`
D. `goto L`

---

## Q3 — MCQ

A basic block is

A. a maximal straight-line sequence with entry only at the first instruction and no branch into or out of the middle
B. an entire procedure, including every call
C. one node of an expression DAG
D. any sequence of instructions that mentions a loop index

---

## Q4 — MCQ

The expression `a + b * c - d` uses the usual precedence of `*` over `+` and `-`. Each operator becomes its own three-address instruction. How many such instructions are required?

A. 2
B. 3
C. 4
D. 5

---

## Level 2 — Standard GATE Style

## Q5 — NAT

Translate `a = b + c * d - e` with the usual precedence. Every operator except the final store into `a` is given a fresh temporary. How many temporaries are used? Enter an integer.

---

## Q6 — MCQ

The statement `if (a < b) x = 1; else x = 2;` is translated with one conditional jump and one unconditional jump that skips the else part. How many jump instructions are there?

A. 1
B. 2
C. 3
D. 4

---

## Q7 — MSQ

The statement `while (i < n) { i = i + 1; }` is translated so that the condition is tested at the top of the loop. Select all that apply.

A. The condition is evaluated at least once whenever the loop is reached.
B. A jump at the end of the body returns to the condition.
C. The false exit of the condition skips the body.
D. The condition is placed only after the body, with no jump back to it.

---

## Q8 — MCQ

The array `a` stores 4-byte integers. The address of `a[i]`, apart from the base address, scales `i` by which factor?

A. 1
B. 2
C. 4
D. 8

---

## Level 3 — Multi-Step

## Q9 — NAT

Boolean `&&` is short-circuit: the right comparison is not emitted on the path where the left comparison is false. Use these costs.

- Each comparison `x rel y` is one instruction `t = x rel y`.
- Each `if t == 0 goto L` is one instruction.
- The assignment `x = y + 1` is one instruction.
- Each `goto` is one instruction.

How many instructions implement `if (a < b && c < d) x = y + 1;`? Enter an integer.

---

## Q10 — MCQ

How many basic blocks are in the following three-address code?

```
(1) i = 0
(2) s = 0
(3) if i >= 3 goto (7)
(4) s = s + i
(5) i = i + 1
(6) goto (3)
(7) return s
```

A. 3
B. 4
C. 5
D. 6

---

## Q11 — MSQ

For the code in Q10, which instructions are leaders? Select all that apply.

A. Instruction (1)
B. Instruction (3)
C. Instruction (4)
D. Instruction (5)

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

The loop `do { s = s + i; i = i + 1; } while (i < n);` is translated in the natural way. Which statement is true?

A. The condition is tested before the first execution of the body.
B. In the generated code the body appears before the test.
C. The translation needs no backward jump.
D. The test jumps only forward.

---

## Q13 — NAT

Use the instruction costs of Q9, and treat a use of a boolean name `a` or `b` as the test `if a == 0 goto L` or `if b == 0 goto L` with no extra comparison instruction. Each assignment `x = 1`, `x = 2`, or `x = 3` is one instruction, but count only jump instructions.

How many jump instructions implement

```
if (a) x = 1; else if (b) x = 2; else x = 3;
```

Enter an integer.

---

## Q14 — MSQ

Which sequences mean the same as `x = a + b * c`, with `*` binding tighter than `+`? Select all that apply.

A. `t1 = b * c` followed by `x = a + t1`
B. `t1 = a + b` followed by `x = t1 * c`
C. `t1 = b * c` followed by `t2 = a + t1` followed by `x = t2`
D. `t1 = a * b` followed by `x = t1 + c`

---

## Level 5 — Challenge

## Q15 — NAT

Use the same instruction costs as in Q9. An assignment `v = v + e`, where `e` is a name, is one instruction. How many instructions implement the following statement? Enter an integer.

```
while (i < 10) {
  if (a < i) a = a + i;
  i = i + 1;
}
```

---

## Q16 — MCQ

Backpatching builds the boolean expression \(E \to E_1\ \mathbf{or}\ E_2\), with short-circuit evaluation. Which statement is the correct data-flow of the lists?

A. The false exits of \(E_1\) are patched to the start of \(E_2\), the true list of \(E\) is the merge of the true lists of \(E_1\) and \(E_2\), and the false list of \(E\) is the false list of \(E_2\).
B. The true exits of \(E_1\) are patched to the start of \(E_2\).
C. The false list of \(E\) is the false list of \(E_1\), and \(E_2\) is never reached from a false exit.
D. Both the true exits and the false exits of \(E_1\) fall through into \(E_2\).

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | B |
| 2 | MSQ | A, B, D |
| 3 | MCQ | A |
| 4 | MCQ | B |
| 5 | NAT | 2 |
| 6 | MCQ | B |
| 7 | MSQ | A, B, C |
| 8 | MCQ | C |
| 9 | NAT | 6 |
| 10 | MCQ | B |
| 11 | MSQ | A, B, C |
| 12 | MCQ | B |
| 13 | NAT | 4 |
| 14 | MSQ | A, C |
| 15 | NAT | 7 |
| 16 | MCQ | A |

## Detailed Solutions

### Q1

Answer: B

The instruction names three addresses: the result `x` and the two operands `y` and `z`. The operator itself is binary, so it has two operands. A unary instruction such as `x = - y` has one operand. The phrase “three-address” counts the result as well as the operands; it does not mean the operator has three operands.

### Q2

Answer: A, B, D

`t1 = a + b` is one binary operator and is already three-address. A conditional goto and an unconditional goto are three-address statements; the conditional form has a relational operator and a target. `a = b + c * d` contains two operators, so it must be split, for example into `t1 = c * d` and `a = b + t1`, before it is three-address code.

### Q3

Answer: A

A basic block is a maximal sequence of consecutive instructions that is entered only at the first instruction and is left only after the last. No jump lands in the middle, and the middle contains no jump. A procedure usually contains several blocks. A DAG node is a single value, not a block. Mentioning a loop index is not the definition of a block.

### Q4

Answer: B

Precedence makes the expression \((a + (b * c)) - d\). The three operators are `*`, `+`, and `-`, and each becomes one instruction:

```
t1 = b * c
t2 = a + t1
t3 = t2 - d
```

Three instructions are necessary because none of the operators can be merged with another in three-address form.

### Q5

Answer: 2

One legal translation is

```
t1 = c * d
t2 = b + t1
a  = t2 - e
```

The final operator stores directly into `a`, so it does not allocate a temporary. The two earlier operators use `t1` and `t2`. Using a third temporary for the subtraction would violate the question’s rule that the final store into `a` is not given a fresh temporary.

### Q6

Answer: B

```
      t1 = a < b
      if t1 == 0 goto Lelse
      x = 1
      goto Lend
Lelse: x = 2
Lend:
```

The conditional jump leaves the then-part, and the unconditional jump skips the else-part. That is two jumps. One jump is not enough: without the goto at the end of the then-part, control would fall into the else-part after assigning `x = 1`.

### Q7

Answer: A, B, C

A top-tested loop has the shape

```
L1:   t1 = i < n
      if t1 == 0 goto L2
      i = i + 1
      goto L1
L2:
```

Reaching the loop always evaluates the condition, including the case `i >= n`, which then takes the false exit and never runs the body. The body ends with a jump back to `L1`. Placing the test only after the body is the translation of a do-while, not of this while. D is false.

### Q8

Answer: C

Element `i` starts at byte offset \(i \times 4\) from the base, because each element occupies 4 bytes. The three-address form is `t1 = i * 4` followed by an indexed store through `t1`. The scale is 4, not the index width and not the index itself.

### Q9

Answer: 6

```
      t1 = a < b
      if t1 == 0 goto Lf
      t2 = c < d
      if t2 == 0 goto Lf
      x = y + 1
      goto Le
Lf:
Le:
```

The six instructions are the two comparisons, the two conditional jumps, the assignment, and the jump that skips the false label. Short-circuit code must not evaluate `c < d` when `a < b` is false; the first conditional jump is what enforces that. Labels are not instructions.

### Q10

Answer: B

The leaders are:

- (1), the first instruction;
- (3), the target of the jump at (6);
- (4), the instruction immediately after the conditional jump at (3);
- (7), the target of the conditional jump at (3).

The blocks are (1)–(2), (3), (4)–(6), and (7). There are 4 blocks. Instruction (5) is in the middle of the body block, and (6) is the last instruction of that block. Neither starts a new block.

### Q11

Answer: A, B, C

From the leader rules used in Q10, (1) starts the program, (3) is a jump target, and (4) follows a conditional jump. Instruction (5) follows the ordinary assignment (4). Control does not enter there by a branch, so (5) is not a leader.

### Q12

Answer: B

A do-while executes the body and then tests:

```
Lbody: s = s + i
       i = i + 1
       t1 = i < n
       if t1 != 0 goto Lbody
```

The body is textually before the test, so the first iteration does not depend on the condition. That is why A, which describes a while, is false. The true exit of the test jumps backward to `Lbody`, so C and D are false. The trap is to translate this loop with the while shape and skip the body when the condition is initially false.

### Q13

Answer: 4

```
      if a == 0 goto L1
      x = 1
      goto Lend
L1:   if b == 0 goto L2
      x = 2
      goto Lend
L2:   x = 3
Lend:
```

The jumps are `if a == 0`, `goto Lend`, `if b == 0`, and `goto Lend`. There are 4. The three assignments are not jumps, and the question does not count them. Each then-part needs its own skip to `Lend`; sharing one conditional jump would send both the false `a` and the false `b` to the same place.

### Q14

Answer: A, C

Usual precedence rewrites `a + b * c` as `a + (b * c)`. Sequence A computes the product first and adds `a`. Sequence C does the same and then copies the sum into `x`. Sequence B computes `(a + b) * c`. Sequence D computes `(a * b) + c`. Neither B nor D is the original expression.

### Q15

Answer: 7

```
L1:   t1 = i < 10
      if t1 == 0 goto L2
      t2 = a < i
      if t2 == 0 goto L3
      a = a + i
L3:   i = i + 1
      goto L1
L2:
```

The seven instructions are the two comparisons, the two conditional jumps, the two assignments, and the backward `goto L1`. The increment of `i` is outside the inner if, so the jump on `a < i` being false must land at the increment, not at the loop exit. Sending that false exit to `L2` would drop the increment and would be a different program. Labels contribute no instructions.

### Q16

Answer: A

For short-circuit `or`, a true result of \(E_1\) already makes \(E\) true, so those exits stay in the true list and must not fall into \(E_2\). A false result of \(E_1\) is not yet a result for \(E\); those exits are patched to the first instruction of \(E_2\). If \(E_2\) is true, \(E\) is true, so the true lists are merged. If \(E_2\) is false, \(E\) is false, so the false list of \(E\) is exactly the false list of \(E_2\). Patching the true exits of \(E_1\) to \(E_2\) would implement `and`, not `or`. Keeping the false list of \(E_1\) would ignore \(E_2\). Letting both outcomes of \(E_1\) fall through would evaluate \(E_2\) even when \(E_1\) is already true.
