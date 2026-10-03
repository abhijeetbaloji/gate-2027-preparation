# Programming in C — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Unless a question says otherwise, assume `sizeof(int) = 4`, `sizeof(char) = 1`, every object pointer is 8 bytes, and integer division truncates toward zero. `int` can represent every value that appears.

## Level 1 — Conceptual

## Q1 — MCQ

What is printed?

```c
int a = 7;
int *p = &a;
*p = *p + 3;
printf("%d", a);
```

A. 7

B. 10

C. 3

D. the address of `a`

---

## Q2 — MCQ

What is printed?

```c
char s[] = "gate";
printf("%d", (int)strlen(s));
```

A. 5

B. 4

C. 8

D. 1

---

## Q3 — NAT

What is printed?

```c
int x = 17, y = 5;
printf("%d", x / y);
```

---

## Q4 — MCQ

Which declaration has static storage duration and internal linkage?

A. `int count = 0;` at file scope

B. `static int count = 0;` at file scope

C. `static int count = 0;` inside a function

D. `int count = 0;` inside a function

---

## Q5 — MCQ

What is printed?

```c
void add(int x) { x = x + 5; }
int main(void) {
    int n = 4;
    add(n);
    printf("%d", n);
}
```

A. 9

B. 4

C. 5

D. The behavior is undefined.

---

## Level 2 — Standard GATE Style

## Q6 — MCQ

What is printed?

```c
int f(void) {
    static int x = 2;
    x = x + 3;
    return x;
}
int main(void) {
    printf("%d", f() + f());
}
```

A. 10

B. 13

C. 8

D. 5

---

## Q7 — NAT

What is printed?

```c
int a[] = {3, 1, 4, 1, 5};
int *p = a;
printf("%d", *(p + 3) + p[0]);
```

---

## Q8 — MCQ

What is printed?

```c
int x = 1, y = 2, z;
z = x++ + ++y;
printf("%d %d %d", x, y, z);
```

A. 2 3 4

B. 1 3 4

C. 2 2 3

D. 2 3 5

---

## Q9 — NAT

What is printed?

```c
int a[6];
printf("%d", (int)sizeof(a));
```

---

## Q10 — MSQ

Select all that apply. Which of the following have defined behavior if executed as written?

A. ```c
char buf[] = "ok";
buf[0] = 'O';
```

B. ```c
char *p = "ok";
p[0] = 'O';
```

C. ```c
int x;
printf("%d", x + 1);
```

D. ```c
int a = 5;
int *p = &a;
*p = 9;
```

---

## Q11 — MCQ

What is printed?

```c
int x = 0, y = 4;
if (x && y++) { }
printf("%d", y);
```

A. 5

B. 4

C. 0

D. The behavior is undefined.

---

## Q12 — NAT

`struct Pair { int a; int b; }` is laid out so that `int` is aligned on a 4-byte boundary and no extra padding is inserted when every member is already aligned. What is printed?

```c
printf("%d", (int)sizeof(struct Pair));
```

---

## Level 3 — Multi-Step

## Q13 — MCQ

What is printed?

```c
void show(int *p) {
    printf("%d", (int)sizeof(p));
}
int main(void) {
    int a[5] = {1, 2, 3, 4, 5};
    printf("%d ", (int)sizeof(a));
    show(a);
}
```

A. 20 20

B. 20 8

C. 5 8

D. 40 8

---

## Q14 — NAT

What is printed? The destination has room for the result, including the terminating null character.

```c
char s[8] = "ace";
strcat(s, "bd");
printf("%d", (int)strlen(s));
```

---

## Q15 — MCQ

Consider this function.

```c
int *make(void) {
    int t = 11;
    return &t;
}
```

Which statement is correct?

A. The returned pointer remains valid for the rest of the program.

B. The returned pointer is dangling. Dereferencing it is undefined behavior.

C. If the caller prints `*make()`, the program is guaranteed to print 11.

D. `t` has static storage duration.

---

## Q16 — NAT

What is printed?

```c
int a = 2;
int *p = &a;
int **q = &p;
**q += 5;
*p += 1;
printf("%d", a);
```

---

## Q17 — MCQ

`struct Box { int w; int h; }` contains two `int` members and has size 8 under the alignment assumption of Q12. What is printed?

```c
struct Box b = {3, 5};
struct Box *p = &b;
int area = p->w * (*p).h;
printf("%d", area + (int)(sizeof(b) / sizeof(int)));
```

A. 15

B. 17

C. 8

D. 16

---

## Level 4 — Tricky / Trap-Based

## Q18 — MCQ

What is printed?

```c
int a[] = {4, 7, 9};
int *p = a;
printf("%d ", *p++);
printf("%d ", (*p)++);
printf("%d", *p);
```

A. 4 7 8

B. 4 7 7

C. 7 8 8

D. 4 8 9

---

## Q19 — MCQ

What is printed?

```c
int a[8];
int *p = a;
printf("%d %d",
       (int)(sizeof(a) / sizeof(int)),
       (int)(sizeof(p) / sizeof(int)));
```

A. 8 8

B. 8 2

C. 2 2

D. 32 8

---

## Q20 — NAT

What is printed?

```c
int x = 3;
printf("%d", x << 1 + 2);
```

---

## Q21 — MSQ

Select all that apply. Which of the following have undefined behavior if executed as written?

A. ```c
int n;
printf("%d", n);
```

B. ```c
int a[3] = {0, 0, 0};
printf("%d", a[3]);
```

C. ```c
int x = 1;
int y = x + 2;
printf("%d", y);
```

D. ```c
int *p;
*p = 5;
```

---

## Level 5 — Challenge

## Q22 — NAT

What is printed?

```c
int a = 9, b = 4;
int *p = &a;
*p = *p % b;
b = *p + b;
p = &b;
*p = *p / 2;
printf("%d", a + b);
```

---

## Q23 — NAT

What is printed?

```c
int f(int *a, int n) {
    int i, s = 0;
    for (i = 0; i < n; i++)
        if (a[i] % 2 == 0)
            s += a[i];
    return s;
}
int main(void) {
    int a[] = {1, 4, 6, 3, 8};
    printf("%d", f(a, 5));
}
```

---

## Q24 — MCQ

What is printed?

```c
int a = 1;
int b = (a += 2, a * 3);
int *p = &a;
*p += b % 5;
printf("%d %d", a, b);
```

A. 7 9

B. 3 9

C. 7 4

D. 1 3

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | (B) |
| 2 | MCQ | (B) |
| 3 | NAT | 3 |
| 4 | MCQ | (B) |
| 5 | MCQ | (B) |
| 6 | MCQ | (B) |
| 7 | NAT | 4 |
| 8 | MCQ | (A) |
| 9 | NAT | 24 |
| 10 | MSQ | (A), (D) |
| 11 | MCQ | (B) |
| 12 | NAT | 8 |
| 13 | MCQ | (B) |
| 14 | NAT | 5 |
| 15 | MCQ | (B) |
| 16 | NAT | 8 |
| 17 | MCQ | (B) |
| 18 | MCQ | (A) |
| 19 | MCQ | (B) |
| 20 | NAT | 24 |
| 21 | MSQ | (A), (B), (D) |
| 22 | NAT | 3 |
| 23 | NAT | 18 |
| 24 | MCQ | (A) |

## Detailed Solutions

### Q1

Answer: (B)

`p` holds the address of `a`. `*p` is another name for `a`, so `*p = *p + 3` stores 10 in `a`. The call prints 10.

### Q2

Answer: (B)

The array is initialized from the literal `"gate"`, which is the four characters `g`, `a`, `t`, `e` followed by a null character. `strlen` counts characters before that null, so it returns 4. The value 5 is `sizeof(s)`, which includes the null character. `strlen` does not count it.

### Q3

Answer: 3

Both operands of `/` have type `int`, so the division is integer division. `17 / 5` is 3, and the remainder 2 is discarded. It is not rounded to 4.

### Q4

Answer: (B)

A file-scope `static int` has static storage duration and internal linkage: it lives for the whole program and is not visible to other translation units. A file-scope `int` without `static` also lives for the whole program, but its linkage is external. A `static` local has static storage duration and no linkage. An ordinary local has automatic storage duration and no linkage.

### Q5

Answer: (B)

C passes arguments by value. `add` receives a copy of 4 and changes only that copy. The variable `n` in `main` stays 4. Changing the caller’s object requires a pointer parameter and a dereference.

### Q6

Answer: (B)

A local `static` is initialized once. The first call starts from `x = 2`, adds 3, and returns 5, leaving `x` equal to 5. The second call adds 3 to that saved value and returns 8. The printed sum is `5 + 8 = 13`. Reinitializing `x` to 2 on every call would print 10, which is the trap.

### Q7

Answer: 4

`p` points at `a[0]`. `p + 3` points at `a[3]`, whose value is 1. `p[0]` is `a[0]`, whose value is 3. The sum is 4.

### Q8

Answer: (A)

The postfix expression `x++` contributes the old value 1, then `x` becomes 2. The prefix expression `++y` first changes `y` from 2 to 3 and contributes 3. Their sum is `z = 4`. The three printed values are 2, 3, and 4. The two modifications are of different objects, so this expression is defined.

### Q9

Answer: 24

`a` is an array object of six `int`s here, not a pointer. `sizeof(a)` is `6 * 4 = 24`.

### Q10

Answer: (A), (D)

(A) is defined: `buf` is a writable array initialized with a copy of the characters. (D) is defined: `p` points at the local `a`, and `*p = 9` stores 9 there. (B) modifies a string literal. That object is not writable, so the assignment is undefined. (C) reads the uninitialized automatic variable `x`. An automatic variable is not implicitly set to 0; reading it is undefined.

### Q11

Answer: (B)

`&&` evaluates its right operand only when its left operand is nonzero. Here `x` is 0, so `y++` is not evaluated. `y` stays 4, and the condition is false.

### Q12

Answer: 8

The first `int` occupies bytes 0 through 3. The next `int` is already aligned at offset 4, so it occupies bytes 4 through 7. The struct size is 8. This question states the layout; a struct that mixed a `char` with an `int` could contain padding, and that size would have to be computed from the stated alignment rules rather than guessed.

### Q13

Answer: (B)

In `main`, `a` is an array of five `int`s, so `sizeof(a)` is 20. The expression `a` passed to `show` is converted to a pointer to its first element. Inside `show`, `sizeof(p)` is the size of that pointer, which is 8. The parameter does not remember that the caller had five elements.

### Q14

Answer: 5

`s` begins as the characters `a`, `c`, `e` and a null. `strcat` appends `b`, `d`, and a new null. The result is the string `acebd`, whose length is 5.

### Q15

Answer: (B)

`t` has automatic storage. Its lifetime ends when `make` returns, so the returned address does not refer to a live object. Using that pointer is undefined. It is not guaranteed to still contain 11, and `t` is not `static`. A safe version would give `t` static storage, or allocate an object that outlives the function, and the caller would then be responsible for that object’s lifetime.

### Q16

Answer: 8

`q` points at `p`, and `p` points at `a`. `**q += 5` adds 5 to `a`, changing it from 2 to 7. `*p += 1` adds 1 to the same object, so `a` becomes 8.

### Q17

Answer: (B)

`p->w` and `(*p).h` are the same two members: 3 and 5. Their product is 15. `sizeof(b) / sizeof(int)` is `8 / 4 = 2`. The printed sum is 17.

### Q18

Answer: (A)

The three statements are sequenced, so the pointer updates are defined. `*p++` is `*(p++)`: it yields `a[0]`, which is 4, and then moves `p` to `a[1]`. `(*p)++` yields the current `a[1]`, which is 7, and then stores 8 there. The last `*p` reads that updated value, 8. The parentheses decide whether `++` applies to the pointer or to the `int` it points at.

### Q19

Answer: (B)

`sizeof(a) / sizeof(int)` is `32 / 4 = 8`, the element count of the array. `p` is a pointer, so `sizeof(p)` is 8, and `8 / sizeof(int)` is 2. That 2 is not the length of the array. Once an array expression has decayed to a pointer, `sizeof` no longer counts its elements.

### Q20

Answer: 24

Addition has higher precedence than `<<`. The expression is `x << (1 + 2)`, which is `3 << 3`. Shifting the value 3 left by 3 multiplies it by 8, giving 24. Reading it as `(x << 1) + 2` would give 8, but that is not how the operators associate here.

### Q21

Answer: (A), (B), (D)

(A) reads an uninitialized automatic variable. (B) uses index 3 of an array whose valid indices are 0, 1, and 2; that access is outside the array. (D) dereferences an uninitialized pointer, which does not point at an object the program may write. (C) is defined: `x` is initialized to 1, `y` becomes 3, and printing `y` is valid.

### Q22

Answer: 3

`p` initially points at `a`. `*p = *p % b` stores `9 % 4 = 1` in `a`. Then `b = *p + b` uses that new value: `b = 1 + 4 = 5`. The assignment `p = &b` retargets `p`; it does not change `a` again. `*p = *p / 2` stores `5 / 2 = 2` in `b`. The sum `a + b` is `1 + 2 = 3`.

### Q23

Answer: 18

The loop inspects 1, 4, 6, 3, and 8. The even values are 4, 6, and 8. Their sum is 18. The parameter `a` is a pointer to the first element; `a[i]` is defined for `i` from 0 through 4.

### Q24

Answer: (A)

The comma operator evaluates `a += 2` first, so `a` becomes 3, and then yields `a * 3`, so `b` is 9. `b % 5` is 4. `p` points at `a`, and `*p += 4` changes `a` from 3 to 7. The call prints 7 and 9. The comma is inside parentheses, so it binds the two expressions that produce `b`; it does not include the later pointer update.
