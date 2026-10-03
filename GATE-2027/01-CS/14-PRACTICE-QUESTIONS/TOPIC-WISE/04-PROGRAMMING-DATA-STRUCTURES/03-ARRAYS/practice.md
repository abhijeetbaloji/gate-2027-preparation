# Arrays — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Array indices start at 0. For a two-dimensional array `a[R][C]` stored in row-major order, the address of `a[i][j]` is

`base + (i * C + j) * element_size`.

Stored in column-major order, it is

`base + (j * R + i) * element_size`.

Unless a question says otherwise, `sizeof(int) = 4`.

## Level 1 — Conceptual

## Q1 — NAT

`int a[5][4]` is stored in row-major order. The base address of `a` is 1000, and each element occupies 4 bytes. The address of `a[2][3]` is ____.

---

## Q2 — MSQ

Select all that apply.

A. After `int a[5] = {1, 2, 3};`, the value of `a[4]` is 0.

B. If `a` is declared as `int a[5];`, the later statement `a = {1, 2, 3, 4, 5};` is a valid assignment.

C. If `a` is declared in a block as `int a[5];`, then `sizeof(a)` equals `5 * sizeof(int)`.

D. If `int *p = a;` for that same array, then `sizeof(p)` equals `sizeof(a)`.

---

## Q3 — NAT

An array of 9 elements is reversed by swapping the element at index `i` with the element at index `8 - i`, for every `i` that satisfies `i < 8 - i`. How many swaps are performed?

---

## Q4 — MCQ

How many `int` elements does the declaration `int a[3][5];` contain?

A. 8

B. 15

C. 2

D. 35

---

## Level 2 — Standard GATE Style

## Q5 — NAT

How many distinct values are present in the array `{4, 1, 7, 1, 7, 4, 9}`?

---

## Q6 — NAT

The following fragment counts how many times the value seen so far is replaced by a strictly larger one. What is printed?

```c
int a[] = {2, 8, 3, 9, 5};
int m = a[0], i, c = 0;
for (i = 1; i < 5; i++)
    if (a[i] > m) {
        m = a[i];
        c++;
    }
printf("%d", c);
```

---

## Q7 — NAT

`int a[5][4]` is stored in column-major order. The base address is 2000, and each element occupies 4 bytes. The address of `a[2][3]` is ____.

---

## Q8 — MCQ

A one-dimensional array already contains 12 elements in indices 0 through 11. Inserting a new element at index 0, while preserving the order of the old elements, requires how many element moves?

A. 1

B. 11

C. 12

D. 13

---

## Level 3 — Multi-Step

## Q9 — NAT

What is printed?

```c
int a[4][3] = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9},
    {10, 11, 12}
};
printf("%d", a[2][1] + a[0][2]);
```

---

## Q10 — NAT

What is printed?

```c
int r0[] = {1, 2};
int r1[] = {3, 4, 5};
int *a[2];
a[0] = r0;
a[1] = r1;
printf("%d", a[1][2] + a[0][1]);
```

---

## Q11 — MCQ

In `{6, 2, 9, 4, 9, 1}`, the largest value that is strictly smaller than the maximum is

A. 9

B. 6

C. 4

D. 2

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

What does this fragment do?

```c
int a[] = {5, 5, 5, 5};
int i, s = 0;
for (i = 0; i <= 4; i++)
    s += a[i];
```

A. It sets `s` to 20 with defined behavior.

B. It sets `s` to 15 with defined behavior.

C. It sets `s` to 25 with defined behavior.

D. The behavior is undefined.

---

## Q13 — NAT

For `int a[4][6]`, element size 4, the row-major address of `a[1][2]` and the column-major address of `a[1][2]` are computed from the same base. The absolute difference of those two addresses, in bytes, is ____.

---

## Q14 — MCQ

What is printed?

```c
int a[] = {1, 2, 3, 4, 5};
int *p = a + 4;
printf("%d", p[-2]);
```

A. 5

B. 4

C. 3

D. 2

---

## Level 5 — Challenge

## Q15 — NAT

The array `{10, 20, 30, 40, 50}` is rotated left by two positions, so it becomes `{30, 40, 50, 10, 20}`. The element then stored at index 3 is ____.

---

## Q16 — NAT

`int a[2][3][4]` is stored in row-major order: `a[i][j][k]` has offset `i * (3 * 4) + j * 4 + k`. The base address is 1000, and each element occupies 4 bytes. The address of `a[1][2][3]` is ____.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | NAT | 1044 |
| 2 | MSQ | (A), (C) |
| 3 | NAT | 4 |
| 4 | MCQ | (B) |
| 5 | NAT | 4 |
| 6 | NAT | 2 |
| 7 | NAT | 2068 |
| 8 | MCQ | (C) |
| 9 | NAT | 11 |
| 10 | NAT | 7 |
| 11 | MCQ | (B) |
| 12 | MCQ | (D) |
| 13 | NAT | 4 |
| 14 | MCQ | (C) |
| 15 | NAT | 10 |
| 16 | NAT | 1092 |

## Detailed Solutions

### Q1

Answer: 1044

`a[5][4]` has 4 columns. The index pair `[2][3]` is at linear offset `2 * 4 + 3 = 11`. Each element is 4 bytes, so the byte offset is 44. The address is `1000 + 44 = 1044`.

### Q2

Answer: (A), (C)

(A) is true. When an initializer lists fewer values than the array length, the remaining elements are initialized to 0, so `a[3]` and `a[4]` are 0. (C) is true while `a` is still an array object: `sizeof(a)` is `5 * sizeof(int)`. (B) is false because an array is not an assignable object; the brace list can initialize it only in the declaration. (D) is false because `sizeof(p)` is the size of a pointer, while `sizeof(a)` is the size of the five-element array.

### Q3

Answer: 4

The pairs are `(0, 8)`, `(1, 7)`, `(2, 6)`, and `(3, 5)`. The next candidate would be `(4, 4)`, but the condition `i < 8 - i` fails when `i` is 4. Four swaps reverse the array. In general, an array of `n` elements uses `floor(n / 2)` such swaps.

### Q4

Answer: (B)

`a[3][5]` has 3 rows and 5 columns, so it contains `3 * 5 = 15` elements. The declaration does not create `3 + 5` elements.

### Q5

Answer: 4

The values that occur are 4, 1, 7, and 9. Repeated copies do not add new values, so the count is 4.

### Q6

Answer: 2

`m` starts at 2. The value 8 is greater, so `m` becomes 8 and `c` becomes 1. The value 3 is not greater. The value 9 is greater, so `m` becomes 9 and `c` becomes 2. The value 5 is not greater. The printed count is 2. The first element is the starting maximum and is not itself counted as a replacement.

### Q7

Answer: 2068

Column-major order walks down a column before moving to the next column. For 5 rows, `a[2][3]` has linear offset `3 * 5 + 2 = 17`. The byte offset is `17 * 4 = 68`. The address is `2000 + 68 = 2068`. The same element in row-major order would use offset `2 * 4 + 3 = 11`, which is a different address.

### Q8

Answer: (C)

The elements currently at indices 11, 10, ..., 0 must each move one slot to the right. That is 12 moves. Moving only 11 elements would leave index 0 occupied by the old first element, or it would drop one of the old elements.

### Q9

Answer: 11

`a[2]` is `{7, 8, 9}`, so `a[2][1]` is 8. `a[0]` is `{1, 2, 3}`, so `a[0][2]` is 3. The sum is 11. In this initializer, the inner braces follow the rows of the row-major layout.

### Q10

Answer: 7

`a` is an array of two pointers, not a rectangular `int` block. `a[1]` points at `{3, 4, 5}`, so `a[1][2]` is 5. `a[0]` points at `{1, 2}`, so `a[0][1]` is 2. The sum is 7. The rows may have different lengths because each pointer addresses its own array.

### Q11

Answer: (B)

The maximum value is 9. Ignoring both copies of 9, the remaining values are 6, 2, 4, and 1. The largest of those is 6. Choosing 9 again would not be strictly smaller than the maximum.

### Q12

Answer: (D)

The array has four elements, with valid indices 0, 1, 2, and 3. The condition `i <= 4` also evaluates `a[4]`. That read is outside the array, so the behavior is undefined. The sum of the four real elements would be 20, but the program is not guaranteed to compute that sum once it reads past the end.

### Q13

Answer: 4

Row-major offset of `a[1][2]` in an array with 6 columns: `1 * 6 + 2 = 8`, which is `8 * 4 = 32` bytes.

Column-major offset in an array with 4 rows: `2 * 4 + 1 = 9`, which is `9 * 4 = 36` bytes.

The absolute difference is 4 bytes. Swapping the roles of the two dimensions changes the address even though the index pair looks the same.

### Q14

Answer: (C)

`a + 4` points at the element 5, which is `a[4]`. The expression `p[-2]` means `*(p - 2)`, two elements before that position, which is `a[2]`. Its value is 3. A negative index is defined when the resulting address is still inside the same array.

### Q15

Answer: 10

A left rotation by two positions moves 10 and 20 from the front to the back. The new array is `{30, 40, 50, 10, 20}`. Index 3 holds 10. Equivalently, the new element at index `i` is the old element at index `(i + 2) mod 5`. For `i = 3`, that old index is 0.

### Q16

Answer: 1092

The offset of `a[1][2][3]` is `1 * 12 + 2 * 4 + 3 = 23` elements. The byte offset is `23 * 4 = 92`. The address is `1000 + 92 = 1092`. The rightmost index changes fastest in this row-major layout.
