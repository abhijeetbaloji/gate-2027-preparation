# Recursion — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Each recursive call has its own activation record: return address, parameters, and local variables. A call is tail recursive when its recursive call is the last action of that invocation, with the callee’s result returned directly.

## Level 1 — Conceptual

## Q1 — MCQ

What is printed by `f(4)`?

```c
void f(int n) {
    if (n == 0) return;
    printf("%d", n);
    f(n - 1);
}
```

A. 1234

B. 4321

C. 4444

D. 01234

---

## Q2 — NAT

What does `sum(6)` return?

```c
int sum(int n) {
    if (n == 0) return 0;
    return n + sum(n - 1);
}
```

---

## Q3 — MCQ

`fact(4)` is evaluated with the function below. The maximum number of `fact` activation records on the call stack at one time, counting the first call, is

```c
int fact(int n) {
    if (n <= 1) return 1;
    return n * fact(n - 1);
}
```

A. 1

B. 3

C. 4

D. 5

---

## Q4 — MSQ

Select all that apply. Which functions are tail recursive?

A. ```c
int f(int n) {
    if (n == 0) return 0;
    return n + f(n - 1);
}
```

B. ```c
int g(int n, int acc) {
    if (n == 0) return acc;
    return g(n - 1, acc + n);
}
```

C. ```c
int h(int n) {
    if (n <= 1) return n;
    return h(n - 1) + h(n - 2);
}
```

D. ```c
int s(int n, int acc) {
    if (n == 0) return acc;
    return s(n - 1, acc * n);
}
```

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

What is printed by `f(4)`?

```c
void f(int n) {
    if (n == 0) return;
    f(n - 1);
    printf("%d", n);
}
```

A. 4321

B. 1234

C. 01234

D. 4444

---

## Q6 — NAT

What does `fib(6)` return?

```c
int fib(int n) {
    if (n <= 1) return n;
    return fib(n - 1) + fib(n - 2);
}
```

---

## Q7 — NAT

How many calls of `fib` are made while evaluating `fib(6)`, including the original call? Use the function in Q6.

---

## Q8 — MCQ

What is printed by `bits(13)`?

```c
void bits(int n) {
    if (n == 0) return;
    bits(n / 2);
    printf("%d", n % 2);
}
```

A. 1011

B. 1101

C. 13

D. 01101

---

## Q9 — NAT

What does `gcd(84, 30)` return?

```c
int gcd(int a, int b) {
    if (b == 0) return a;
    return gcd(b, a % b);
}
```

---

## Level 3 — Multi-Step

## Q10 — MCQ

What is printed by `p(4)`?

```c
void p(int n) {
    if (n <= 0) return;
    p(n - 1);
    printf("%d", n);
    p(n - 2);
}
```

A. 1234

B. 1213124

C. 1231412

D. 4321

---

## Q11 — NAT

What does `f(20)` return?

```c
int f(int n) {
    if (n < 2) return n;
    return 1 + f(n / 2);
}
```

---

## Q12 — NAT

The recursion tree of `t(4)` has one node for each call. How many leaves does that tree have?

```c
int t(int n) {
    if (n <= 1) return 1;
    return t(n - 1) + t(n - 1);
}
```

---

## Q13 — NAT

While `t(4)` from Q12 runs, the two recursive calls in a single activation happen one after the other. The maximum number of `t` activation records on the stack at one time, counting the first call, is ____.

---

## Level 4 — Tricky / Trap-Based

## Q14 — MCQ

What is printed by `f(3)`?

```c
void f(int n) {
    if (n == 0) return;
    printf("%d", n);
    f(n - 1);
    printf("%d", n);
}
```

A. 321123

B. 123321

C. 321

D. 333222111

---

## Q15 — NAT

What does the first call `f(3)` return?

```c
int f(int n) {
    static int k = 0;
    k++;
    if (n <= 0) return k;
    return f(n - 1);
}
```

---

## Q16 — NAT

What does `mystery(a, 6)` return when `a` is `{2, 7, 4, 9, 1, 6}`?

```c
int mystery(int a[], int n) {
    if (n == 0) return 0;
    if (a[n - 1] % 2) return 1 + mystery(a, n - 1);
    return mystery(a, n - 1);
}
```

---

## Level 5 — Challenge

## Q17 — NAT

What does `ack(2, 2)` return?

```c
int ack(int m, int n) {
    if (m == 0) return n + 1;
    if (n == 0) return ack(m - 1, 1);
    return ack(m - 1, ack(m, n - 1));
}
```

---

## Q18 — MCQ

What is printed by `walk(3)`?

```c
void walk(int n) {
    if (n <= 0) {
        printf("0");
        return;
    }
    printf("(");
    walk(n - 1);
    printf(")");
    walk(n - 2);
}
```

A. `(((0)0)0)(0)0`

B. `(((0)0)0)(0)`

C. `((0)(0))(0)`

D. `(0)(0)(0)(0)`

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (B) |
| 2 | NAT | 21 |
| 3 | MCQ | (C) |
| 4 | MSQ | (B), (D) |
| 5 | MCQ | (B) |
| 6 | NAT | 8 |
| 7 | NAT | 25 |
| 8 | MCQ | (B) |
| 9 | NAT | 6 |
| 10 | MCQ | (C) |
| 11 | NAT | 5 |
| 12 | NAT | 8 |
| 13 | NAT | 4 |
| 14 | MCQ | (A) |
| 15 | NAT | 4 |
| 16 | NAT | 3 |
| 17 | NAT | 7 |
| 18 | MCQ | (A) |

## Detailed Solutions

### Q1

Answer: (B)

`f(4)` prints 4 before calling `f(3)`. The same pattern prints 3, then 2, then 1. `f(0)` returns without printing. The output is 4321. The work is done on the way down, before each recursive call.

### Q2

Answer: 21

`sum(6) = 6 + sum(5) = 6 + 5 + sum(4) = 6 + 5 + 4 + 3 + 2 + 1 + sum(0)`. The base call returns 0, so the value is 21. This call is not tail recursive: the addition happens after `sum(n - 1)` returns.

### Q3

Answer: (C)

The pending calls are `fact(4)`, `fact(3)`, `fact(2)`, and `fact(1)`. That is four records. `fact(1)` is the base call and does not call `fact(0)`, so a fifth record is not created. Each record holds its own `n`. The deepest record can return only after it is created, so the maximum is reached when `fact(1)` is still active.

### Q4

Answer: (B), (D)

(B) and (D) return the recursive call directly. Nothing in the caller remains to do after that call, so each is tail recursive. (A) must add `n` after `f(n - 1)` returns. (C) makes two recursive calls and adds their results, so neither call is in tail position. Tail recursion is an idea about the last action of the activation. A compiler may reuse one record for the calls in (B) and (D); the meaning of the function does not depend on that optimization.

### Q5

Answer: (B)

`f(4)` calls `f(3)` before printing. The prints happen only after the deeper calls return, so the order is 1, then 2, then 3, then 4. Compare this with Q1: moving `printf` from before the call to after the call reverses the output.

### Q6

Answer: 8

The base values are `fib(0) = 0` and `fib(1) = 1`. Then `fib(2) = 1`, `fib(3) = 2`, `fib(4) = 3`, `fib(5) = 5`, and `fib(6) = 8`.

### Q7

Answer: 25

Let `C(n)` be the number of calls made by `fib(n)`, including itself. `C(0) = C(1) = 1`, and `C(n) = 1 + C(n - 1) + C(n - 2)` for `n > 1`.

`C(2) = 3`, `C(3) = 5`, `C(4) = 9`, `C(5) = 15`, and `C(6) = 25`. The recursion tree branches, so the call count is much larger than 6.

### Q8

Answer: (B)

Integer division by 2 and the remainder produce the binary digits of 13 from least significant to most significant: 1, then 0, then 1, then 1, because `13 = 8 + 4 + 1`. The recursive call happens before `printf`, so those digits are printed on the way back, most significant first: 1101. The base call `bits(0)` prints nothing, so there is no leading zero.

### Q9

Answer: 6

`gcd(84, 30)` calls `gcd(30, 84 % 30) = gcd(30, 24)`, then `gcd(24, 6)`, then `gcd(6, 0)`. The base call returns 6. This is the Euclidean algorithm written as a tail call.

### Q10

Answer: (C)

`p(4)` first runs `p(3)` completely, then prints 4, then runs `p(2)`.

`p(3)` runs `p(2)`, prints 3, and runs `p(1)`.

`p(2)` runs `p(1)`, prints 2, and runs `p(0)`, which returns immediately.

`p(1)` runs `p(0)`, prints 1, and runs `p(-1)`, which returns immediately.

So `p(2)` prints 12, `p(3)` prints 1231, and the final `p(2)` after the digit 4 prints 12. The whole output is 1231412.

### Q11

Answer: 5

`f(20) = 1 + f(10)`, `f(10) = 1 + f(5)`, `f(5) = 1 + f(2)`, and `f(2) = 1 + f(1)`. Since `1 < 2`, `f(1)` returns 1. The total is `1 + 1 + 1 + 1 + 1 = 5`. The chain is a single recursive call at each step, so the activation depth is also 5.

### Q12

Answer: 8

Every call with `n > 1` has two children, both labeled `t(n - 1)`. The leaves are the calls with `n <= 1`. A complete binary tree of calls with 3 edges on the path from `t(4)` down to `t(1)` has `2^3 = 8` leaves. The value returned by `t(4)` is also 8, because every leaf returns 1 and the internal nodes add those results. The leaf count asked here is the number of base calls.

### Q13

Answer: 4

The two calls `t(n - 1)` are sequential. The first must return before the second begins, so their records are not on the stack together. The deepest chain is `t(4)`, `t(3)`, `t(2)`, `t(1)`: four records. The recursion tree has 8 leaves, but the maximum stack depth is the height of that tree in calls, not the number of leaves.

### Q14

Answer: (A)

`f(3)` prints 3, runs `f(2)`, and prints 3 again. `f(2)` prints 2, runs `f(1)`, and prints 2 again. `f(1)` prints 1, calls `f(0)`, and prints 1 again. `f(0)` prints nothing. The output is 321123. Printing both before and after the call is different from printing only on the way down or only on the way back. Reversing the whole string is not what this function does.

### Q15

Answer: 4

`k` is initialized once, not on every call. The calls are `f(3)`, `f(2)`, `f(1)`, and `f(0)`, and each increments `k`. When `f(0)` is reached, `k` is 4, and that value is returned straight back through the tail calls. The base case does not return 0. It returns the number of calls made so far. A later top-level call of `f` would continue from the saved `k` rather than from 0.

### Q16

Answer: 3

`n` is the number of elements still under consideration, and the function inspects `a[n - 1]`. For `n = 6, 5, 4, 3, 2, 1` the inspected values are 6, 1, 9, 4, 7, and 2. The odd ones are 1, 9, and 7, so the result is 3. Using `a[n]` instead of `a[n - 1]` would read past the array; the parameter `n` is a length, and the last valid index is `n - 1`.

### Q17

Answer: 7

`ack(0, n) = n + 1`. From that, `ack(1, 0) = ack(0, 1) = 2`, and `ack(1, n) = ack(0, ack(1, n - 1)) = ack(1, n - 1) + 1`, so `ack(1, n) = n + 2`.

Then `ack(2, 0) = ack(1, 1) = 3`, and `ack(2, n) = ack(1, ack(2, n - 1))`. This gives `ack(2, 1) = ack(1, 3) = 5` and `ack(2, 2) = ack(1, 5) = 7`.

The inner call `ack(2, 1)` must finish before the outer call `ack(1, ...)` begins. These are not tail calls, and both results are required.

### Q18

Answer: (A)

`walk(3)` prints `(`, runs `walk(2)`, prints `)`, and runs `walk(1)`.

`walk(2)` prints `(`, runs `walk(1)`, prints `)`, and runs `walk(0)`, which prints 0.

`walk(1)` prints `(`, runs `walk(0)` printing 0, prints `)`, and runs `walk(-1)` printing 0.

The first `walk(1)`, inside `walk(2)`, therefore contributes `(0)0`. Wrapped by `walk(2)`, that is `((0)0)0`. Wrapped by the opening part of `walk(3)`, that is `(((0)0)0)`. The final `walk(1)` contributes `(0)0`. The full string is `(((0)0)0)(0)0`.
