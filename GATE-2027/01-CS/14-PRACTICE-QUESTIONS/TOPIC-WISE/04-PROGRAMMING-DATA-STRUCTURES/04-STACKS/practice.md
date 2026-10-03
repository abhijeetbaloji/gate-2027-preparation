# Stacks — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

The top of a stack is the end at which push and pop occur. In the infix conversions below, the operators are `+` and `-` at the lowest precedence, then `*` and `/`, then `^` at the highest precedence. `+`, `-`, `*`, and `/` associate left to right. `^` associates right to left. Operands are single letters or the integers written in the postfix expressions.

## Level 1 — Conceptual

## Q1 — MCQ

An empty stack receives `push A`, `push B`, `push C`, `pop`, `pop`, `push D`, `pop`. The sequence of popped values is

A. C, B, D

B. A, B, C

C. C, D, B

D. B, C, D

---

## Q2 — MCQ

Which string is correctly balanced?

A. `{[()]}`

B. `{[(])}`

C. `((])`

D. `([)]`

---

## Q3 — MCQ

The postfix form of `A + B * C` is

A. `AB+C*`

B. `ABC*+`

C. `ABC+*`

D. `A+BC*`

---

## Q4 — NAT

The value of the postfix expression `5 1 2 + 4 * + 3 -` is ____. Every operand is a single-digit integer, and the operator follows its two operands.

---

## Level 2 — Standard GATE Style

## Q5 — MSQ

Input arrives in the order 1, 2, 3, 4. A stack may hold values temporarily: the next input may be pushed, or the current top may be popped to the output. Select all that apply. Which outputs can be produced?

A. 2, 4, 3, 1

B. 4, 3, 1, 2

C. 3, 1, 2, 4

D. 2, 3, 4, 1

---

## Q6 — MCQ

The postfix form of `(A + B) * (C - D)` is

A. `AB+CD-*`

B. `AB+CD*-`

C. `ABCD+-*`

D. `AB+C*D-`

---

## Q7 — NAT

A stack is used to check the parentheses in `((())())`. Only the two characters `(` and `)` occur. The maximum number of characters stored on the stack at one time is ____.

---

## Q8 — NAT

The value of the postfix expression `8 2 3 * + 4 -` is ____.

---

## Level 3 — Multi-Step

## Q9 — NAT

For the array `{4, 5, 2, 25}`, the next greater element of a value is the nearest strictly greater value on its right, if one exists. How many elements have a next greater element?

---

## Q10 — MCQ

The infix form of the postfix expression `AB+C*`, with the usual precedence restored using the fewest parentheses, is

A. `(A + B) * C`

B. `A + (B * C)`

C. `A + B * C`

D. `(A + B * C)`

---

## Q11 — NAT

While the postfix expression `9 3 2 * 4 5 * + + 8 2 / -` is evaluated, the operand stack holds a varying number of values. The maximum number of values on that stack at one time is ____.

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

The postfix form of `A - B - C` is

A. `AB-C-`

B. `ABC--`

C. `A-BC-`

D. `AB--C`

---

## Q13 — MCQ

A stack is stored in `S[0..n-1]`, and `top` starts at `-1`. A correct push refuses to insert when `top == n - 1`. A student instead uses this push:

```c
if (top == n) { /* report overflow */ }
else {
    top = top + 1;
    S[top] = x;
}
```

Which statement describes this push?

A. It reports overflow at the right time and never writes outside `S`.

B. It can set `top` to `n` and write `S[n]`, which is outside the array, before the overflow test would succeed.

C. It treats the stack as full when `top` is `-1`.

D. After `n` successful pushes, `top` is still `-1`.

---

## Q14 — MCQ

The prefix form of `A + B * C` is

A. `+A*BC`

B. `+*ABC`

C. `ABC*+`

D. `*+ABC`

---

## Level 5 — Challenge

## Q15 — NAT

An empty stack receives `push 1`, `push 2`, `push 3`, `pop`, `push 4`, `pop`, `pop`, `push 5`. The sum of the integers still on the stack after these operations is ____.

---

## Q16 — MCQ

Using the precedence and associativity stated at the top of this set, the postfix form of `A ^ B ^ C * D + E` is

A. `ABC^^D*E+`

B. `AB^C^D*E+`

C. `ABC^D^*E+`

D. `ABC^^DE+*`

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (A) |
| 2 | MCQ | (A) |
| 3 | MCQ | (B) |
| 4 | NAT | 14 |
| 5 | MSQ | (A), (D) |
| 6 | MCQ | (A) |
| 7 | NAT | 3 |
| 8 | NAT | 10 |
| 9 | NAT | 3 |
| 10 | MCQ | (A) |
| 11 | NAT | 4 |
| 12 | MCQ | (A) |
| 13 | MCQ | (B) |
| 14 | MCQ | (A) |
| 15 | NAT | 6 |
| 16 | MCQ | (A) |

## Detailed Solutions

### Q1

Answer: (A)

After `A`, `B`, and `C` are pushed, the stack from bottom to top is `A B C`. The first pop returns `C`, and the second returns `B`. Then `D` is pushed onto `A`, and the last pop returns `D`. The popped sequence is `C, B, D`. The value `A` is still on the stack.

### Q2

Answer: (A)

Scan from left to right. An opening bracket is pushed. A closing bracket is allowed only when it matches the current top, which is then popped.

For `{[()]}`, the stack grows through `{`, `{ [`, and `{ [ (`. The three closing brackets match `(`, `[`, and `{` in that order, and the stack ends empty.

In `{[(])}`, the character `]` arrives while `(` is on top. Those brackets do not match. In `((])`, `]` does not match `(`. In `([)]`, `)` arrives while `[` is on top. Only (A) is balanced.

### Q3

Answer: (B)

`*` binds more tightly than `+`, so the expression is `A + (B * C)`. The postfix form of `B * C` is `BC*`, and the later addition places `+` after that result: `ABC*+`. The string `AB+C*` means `(A + B) * C`.

### Q4

Answer: 14

The operand stack proceeds as follows.

- Push 5, 1, and 2. The stack is `5 1 2`.
- `+` replaces 1 and 2 with 3. The stack is `5 3`.
- Push 4. The stack is `5 3 4`.
- `*` replaces 3 and 4 with 12. The stack is `5 12`.
- `+` replaces 5 and 12 with 17.
- Push 3, then `-` computes `17 - 3 = 14`.

The value is 14. The largest stack in this trace has three operands, but the question asks for the value.

### Q5

Answer: (A), (D)

(A) is possible: push 1, push 2, pop 2, push 3, push 4, pop 4, pop 3, pop 1. The output is `2 4 3 1`.

(D) is possible: push 1, push 2, pop 2, push 3, pop 3, push 4, pop 4, pop 1. The output is `2 3 4 1`.

(B) is impossible. To output 4 first, 1, 2, and 3 must already be on the stack, with 3 above 2 and 2 above 1. After popping 4 and then 3, the top is 2, so 1 cannot be output before 2.

(C) is impossible for the same reason at the start: after 3 is the first output, 2 is above 1, so the next output cannot be 1.

### Q6

Answer: (A)

`A + B` becomes `AB+`, and `C - D` becomes `CD-`. The multiplication is outside both parenthesized results, so `*` comes last: `AB+CD-*`. The parentheses force the addition and subtraction to happen before the multiplication.

### Q7

Answer: 3

Each `(` is pushed, and each `)` pops one `(`.

The depth is 1, 2, 3, 2, 1, 2, 1, 0. The maximum is 3. The string is balanced, so the stack is empty at the end; the question asks for the maximum, not the final size.

### Q8

Answer: 10

Push 8, 2, and 3. `*` replaces 2 and 3 with 6, leaving `8 6`. `+` replaces them with 14. Push 4, and `-` computes `14 - 4 = 10`.

### Q9

Answer: 3

The next greater element of 4 is 5. The next greater element of 5 is 25. The next greater element of 2 is 25. The value 25 has none. Three elements succeed.

A stack can find these in one left-to-right pass. Keep indices of values still waiting for a greater element. When 5 arrives, it resolves 4. When 25 arrives, it resolves 5 and 2. The count does not include 25.

### Q10

Answer: (A)

`AB+` is `A + B`. The following `C*` multiplies that whole result by `C`, so the expression is `(A + B) * C`. Option (C), written without parentheses, means `A + (B * C)` because `*` has higher precedence. That different expression has postfix `ABC*+`.

### Q11

Answer: 4

The stack sizes after each token are:

`9` (1), `9 3` (2), `9 3 2` (3), `*` leaves `9 6` (2), `9 6 4` (3), `9 6 4 5` (4), `*` leaves `9 6 20` (3), `+` leaves `9 26` (2), `+` leaves `35` (1), `35 8` (2), `35 8 2` (3), `/` leaves `35 4` (2), and `-` leaves `31` (1).

The maximum is 4, reached when the stack holds `9 6 4 5`. The value of the expression is 31, but the question asks for that maximum size. The final value is `9 + (3 * 2) + (4 * 5) - (8 / 2) = 31`, using integer division for the last operator.

### Q12

Answer: (A)

`-` associates to the left, so `A - B - C` means `(A - B) - C`. Its postfix form is `AB-C-`. The string `ABC--` means `A - (B - C)`, which is a different expression because subtraction is not associative. Reversing the operator order does not preserve the left association.

### Q13

Answer: (B)

The legal indices are 0 through `n - 1`. Starting from `top = -1`, the first `n` pushes see `top` equal to `-1, 0, ..., n - 2` at the moment of the test. None of those values equals `n`, so the `else` branch runs all `n` times and the last one sets `top` to `n`. The write `S[n]` is outside the array. The test `top == n` can become true only on a later call, after that illegal write. The correct full test, before incrementing, is `top == n - 1`.

### Q14

Answer: (A)

`A + B * C` means `A + (B * C)`. In prefix form the operator comes before its two operands, so `B * C` is `*BC`, and the addition is `+A*BC`. The postfix form `ABC*+` is not prefix. Reversing that postfix string produces `+*CBA`, which is not the prefix form either.

### Q15

Answer: 6

The stack from bottom to top changes as follows: `1`, `1 2`, `1 2 3`, pop 3 leaving `1 2`, `1 2 4`, pop 4 leaving `1 2`, pop 2 leaving `1`, then `1 5`. The popped values are 3, 4, and 2. The remaining values are 1 and 5, and their sum is 6.

### Q16

Answer: (A)

`^` is right-associative and tighter than `*`, and `*` is tighter than `+`. The expression means `((A ^ (B ^ C)) * D) + E`.

`B ^ C` becomes `BC^`. Then `A ^ (B ^ C)` becomes `ABC^^`. Multiplying by `D` adds a final `*`, giving `ABC^^D*`. Adding `E` puts `+` last: `ABC^^D*E+`.

Option (B) treats `^` as left-associative, which would mean `(A ^ B) ^ C` before the multiplication. That is not the associativity used here.
