# Regular Expressions — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

In these questions, `+` denotes union, juxtaposition denotes concatenation, and `*` denotes Kleene star. The empty string is `ε`. Star binds tightest, then concatenation, then union.

## Level 1 — Conceptual

## Q1 — MCQ

Which language, over the alphabet `{a, b}`, is denoted by `(a+b)*abb`?

A. All strings that end with `abb`  
B. All strings that contain exactly one occurrence of the substring `abb`  
C. All strings that begin with `abb`  
D. All strings with equally many `a`'s and `b`'s

---

## Q2 — MCQ

The regular expression `ab+c` denotes the set

A. `{ab, c}`  
B. `{ab, ac}`  
C. `{abc}`  
D. `{a, b, c}`

---

## Q3 — NAT

The number of strings of length 3 denoted by `(0+1)*0(0+1)` is ____.

---

## Q4 — MCQ

Which one of the following regular expressions denotes `{0, 1}*`?

A. `0* + 1*`  
B. `(0*1*)*`  
C. `(01)*`  
D. `0*1*`

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

Which regular expression denotes all strings over `{a, b}` that contain at most one `a`?

A. `b* + b*ab*`  
B. `b*a*b*`  
C. `(a+b)*a(a+b)*`  
D. `a*b*`

---

## Q6 — MSQ

Which of the following regular expressions denote the set of all binary strings with an even number of `1`s? Select all that apply.

A. `(0*10*1)*0*`  
B. `0*(10*10*)*`  
C. `(0+10*1)*`  
D. `(1*01*)*`

---

## Q7 — NAT

The number of strings of length 4 denoted by `(a+ba)*` is ____.

---

## Q8 — MCQ

Arden's lemma, in the form used here: if `ε` is not in the language of `P`, then the equation `X = PX + Q` has the unique solution `X = P*Q`.

The solution of `X = aX + b` is

A. `a*b`  
B. `ba*`  
C. `(a+b)*`  
D. `a*b*`

---

## Level 3 — Multi-Step

## Q9 — MCQ

Which regular expression denotes all strings over `{a, b}` in which no two `a`'s are consecutive?

A. `(b+ab)*(ε+a)`  
B. `b*(ab*)*`  
C. `(a+b)*`  
D. `(aa+b)*`

---

## Q10 — NAT

The number of strings of length 5 denoted by `(0+10)*1` is ____.

---

## Q11 — MSQ

Which of the following strings belong to the language of `a(bc)*d`? Select all that apply.

A. `ad`  
B. `abcd`  
C. `abcbcd`  
D. `abd`

---

## Level 4 — Tricky / Trap-Based

## Q12 — MCQ

The regular expression `a+b*c` denotes

A. `{a} ∪ {b^n c | n ≥ 0}`  
B. `{a b^n c | n ≥ 0}`  
C. `{(a+b)^n c | n ≥ 0}`  
D. `{a, c} ∪ {b^n | n ≥ 0}`

---

## Q13 — NAT

How many binary strings of length 4 are denoted by `(0+1)*1(0+1)*0(0+1)*`?  
(These are exactly the length-4 strings in which some `1` occurs before a later `0`.)

---

## Q14 — MSQ

Which of the following denote exactly the binary strings that do not contain the substring `00`? Select all that apply.

A. `(1+01)*(ε+0)`  
B. `(10+1)*(ε+0)`  
C. `(1*01*)*`  
D. `(ε+0)(1+10)*`

---

## Level 5 — Challenge

## Q15 — MSQ

Which of the following denote exactly the strings over `{a, b}` with an odd number of `a`'s? Select all that apply.

A. `b*a(b*ab*a)*b*`  
B. `(b*ab*a)*b*ab*`  
C. `(ab*ab*)*ab*`  
D. `(b*ab*)*`

---

## Q16 — NAT

The number of strings of length 6 denoted by `(0+10)*(ε+1)` is ____.

## Answer Key
| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | NAT | 4 |
| 4 | MCQ | B |
| 5 | MCQ | A |
| 6 | MSQ | A, B, C |
| 7 | NAT | 5 |
| 8 | MCQ | A |
| 9 | MCQ | A |
| 10 | NAT | 5 |
| 11 | MSQ | A, B, C |
| 12 | MCQ | A |
| 13 | NAT | 11 |
| 14 | MSQ | A, D |
| 15 | MSQ | A, B |
| 16 | NAT | 21 |

## Detailed Solutions

### Q1

Answer: A

Every string matched by `(a+b)*abb` is an arbitrary string over `{a, b}` followed by the fixed suffix `abb`. Conversely, any string that ends with `abb` can be split that way. So the language is exactly the strings that end with `abb`.

It is not “exactly one occurrence”: `abbabb` ends with `abb` and contains the block twice, and it is generated. It is not the set of strings that merely begin with `abb`, and equality of the two letter counts is not enforced.

### Q2

Answer: A

Concatenation binds more tightly than union, so `ab+c` means `(ab)+c`, which is the two-string set `{ab, c}`.

Option (B) is the language of `a(b+c)`. Option (C) is the language of `abc`. Option (D) treats the expression as three separate symbols.

### Q3

Answer: 4

A match of `(0+1)*0(0+1)` ends with a `0` followed by exactly one symbol. In a string of length 3, that `0` occupies position 2, and positions 1 and 3 are free binary symbols.

The four strings are `000`, `001`, `100`, and `101`.

### Q4

Answer: B

`(0*1*)*` generates every binary string: scan the string from left to right and cut it into blocks that are a run of `0`s followed by a run of `1`s (either run may be empty only in a way that still covers the next symbol; empty blocks are not required). Equivalently, each bit is either a `0` inside some `0*` or a `1` inside some `1*`, and consecutive blocks can be chosen so that the cuts fall at every change from `1` back to `0`.

The other three miss strings:

- `0*+1*` does not contain `01`.
- `(01)*` does not contain `0` or `11`.
- `0*1*` does not contain `10`.

### Q5

Answer: A

`b* + b*ab*` is `b*(ε+a)b*`. Every `b` is unrestricted, and there is at most one `a`. Every string with at most one `a` has that shape: the `b`s before the `a` (if any) and the `b`s after it.

- `b*a*b*` allows `aa`.
- `(a+b)*a(a+b)*` requires at least one `a`.
- `a*b*` rejects `ba` and also allows many `a`s.

### Q6

Answer: A, B, C

(A), (B), and (C) each add `1`s in pairs.

- In (A), every pass through `(0*10*1)` contributes two `1`s, and the final `0*` contributes none. Any even placement works: put the `0`s before the first `1` of a pair into the leading `0*` of that pair, the `0`s between the two `1`s of the pair into the middle `0*`, and the `0`s after the last `1` into the final `0*`.
- In (B), the leading `0*` takes the opening `0`s and each `(10*10*)` takes two `1`s together with the `0`s that follow each of them.
- In (C), a summand is either a single `0` or a block `10*1` with two `1`s. The same left-to-right pairing used for (A) shows that every even string is obtained.

(D) is different. Each pass through `(1*01*)` consumes exactly one `0`, so the expression denotes `ε` together with every string that contains at least one `0`. It excludes `11`, which has an even number of `1`s, and it includes `01`, which has an odd number.

### Q7

Answer: 5

Every string in `(a+ba)*` is a concatenation of blocks `a` (length 1) and `ba` (length 2). For total length 4 the possibilities are:

- four `a` blocks: `aaaa`
- one `ba` and two `a` blocks, with the `ba` in any of the three block positions: `baaa`, `abaa`, `aaba`
- two `ba` blocks: `baba`

That is five strings. No block contains `bb`, so a string such as `abba` is not in the language.

### Q8

Answer: A

The equation is `X = aX + b`, so `P = a` and `Q = b`. The symbol `a` does not denote a language containing `ε`. Arden's lemma gives

`X = P*Q = a*b`.

Concretely, unfolding the equation produces `b`, `ab`, `aab`, `aaab`, and so on. Option (B) would be the solution of `X = Xa + b`. Options (C) and (D) contain strings such as `a` and `ba` that the equation does not generate.

### Q9

Answer: A

The blocks of `(b+ab)*` are `b` and `ab`. Every `a` inside the star is immediately followed by `b`, and the optional final `a` is attached only when the star has just ended on `b` or is empty. So two `a`s never touch. Every string with no `aa` is a sequence of `b`s and isolated `a`s, which is exactly this block decomposition (an `a` that is not at the end is grouped with the following `b` as `ab`).

(B) contains `aa`: take the outer `b*` empty and then two copies of `a` with the inner `b*` empty. (C) is every string. (D) contains `aa` and does not contain the legal string `a`.

### Q10

Answer: 5

`(0+10)*` denotes the binary strings with no substring `11` that are empty or end with `0`. Appending a final `1` therefore gives exactly the strings with no substring `11` that end with `1`: the symbol before that final `1` is not `1`, and every such string arises by taking its prefix before the last `1`.

For length 5 the strings are

`00001`, `00101`, `01001`, `10001`, `10101`.

There are 5 of them. The same count satisfies the recurrence for “no two consecutive `1`s”: if `a_n` is the number of such strings of length `n` and `e_n` is the number that end with `1`, then `e_n = a_{n-2}` for `n ≥ 2`, with `a_1 = 2`, `a_2 = 3`, `a_3 = 5`, so `e_5 = a_3 = 5`.

### Q11

Answer: A, B, C

`a(bc)*d` is an `a`, followed by zero or more copies of the block `bc`, followed by `d`.

- `ad` uses zero blocks.
- `abcd` uses one block.
- `abcbcd` uses two blocks.
- `abd` would require a `b` that is not part of a `bc` block, so it does not match.

### Q12

Answer: A

Star binds before concatenation, and concatenation binds before union. Thus `a+b*c` means `a + ((b*)c)`, which is `{a}` together with `{b^n c | n ≥ 0}`. The strings are `a`, `c`, `bc`, `bbc`, `bbbc`, and so on.

- (B) is the language of `ab*c`, which excludes the string `a` standing alone and excludes `c` with no leading `a`.
- (C) is the language of `(a+b)*c`. That reading pretends that union binds more tightly than the star, or it inserts parentheses that are not in the expression.
- (D) includes `b` and excludes `bc`.

### Q13

Answer: 11

The expression requires a `1` somewhere and a `0` strictly to its right. A binary string fails this test precisely when it belongs to `0*1*`: a block of `0`s followed by a block of `1`s (either block may be empty).

There are `2^4 = 16` binary strings of length 4, and the members of `0*1*` of that length are

`0000`, `0001`, `0011`, `0111`, `1111`.

Hence `16 − 5 = 11` strings match the expression.

### Q14

Answer: A, D

A binary string avoids `00` exactly when every `0` is either at the end or immediately followed by `1`.

(A) builds the string from blocks `1` and `01`, then allows one final `0`. Every internal `0` is the start of a `01` block, so it is followed by `1`. Every avoiding string is obtained by grouping each internal `0` with the following `1` and leaving a final `0` unmatched if there is one.

(D) allows one leading `0` and then blocks `1` and `10`. A leading `0` is safe only because the next block, if any, starts with `1`. Every later `0` ends a `10` block, so the next symbol is either absent or the start of a block that begins with `1`. This is the same language.

(B) does not denote that language. The blocks `10` and `1` cannot produce a string that starts with `0` and then continues, so `01` is missing even though `01` has no `00`. Also `(10)0 = 100` is generated and does contain `00`.

(C) generates `00`, by concatenating two copies of `0` with all of the `1*` parts empty, and it does not generate `11`.

### Q15

Answer: A, B

(A) places one distinguished `a` and then zero or more pairs `(b* a b* a)`. The total number of `a`s is `1 + 2k`. The `b`s can sit in any of the `b*` slots, so every string with an odd number of `a`s is obtained by letting the distinguished `a` be the first `a` and pairing the rest. Strings with an even number of `a`s do not match this count.

(B) is the same idea with the pairs first and the distinguished `a` last. Again the count of `a`s is odd, and every odd string is obtained by letting the distinguished `a` be the last `a`.

(C) also forces an odd count, but every block starts with `a`. The string `ba` has one `a` and is not generated.

(D) generates one `a` per iteration, so the count may be even. In particular `aa` matches two iterations with every `b*` empty. It also fails to generate `b`.

### Q16

Answer: 21

First, `(0+10)*(ε+1)` denotes every binary string with no substring `11`.

- `(0+10)*` denotes the strings with no `11` that are empty or end with `0`. Each `1` in such a string is followed by a `0` and can be grouped with that `0` as a `10` block; the remaining symbols are `0` blocks.
- The optional final `1` adds exactly the avoiding strings that end with `1`, without creating an `11` at the junction.
- Every avoiding string is in one of those two families.

Let `a_n` be the number of binary strings of length `n` with no `11`. A nonempty avoiding string ends in `0` or in `01` after an avoiding prefix, so

`a_n = a_{n-1} + a_{n-2}`

for `n ≥ 3`, with `a_1 = 2` (`0`, `1`) and `a_2 = 3` (`00`, `01`, `10`). Then

`a_3 = 5`, `a_4 = 8`, `a_5 = 13`, `a_6 = 21`.
