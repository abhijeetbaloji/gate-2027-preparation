# Lexical Analysis — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

Which compiler phase reads the source as a character stream and groups those characters into lexemes, each labelled with a token name?

A. Semantic analysis
B. Lexical analysis
C. Syntax analysis
D. Intermediate-code generation

---

## Q2 — MSQ

Which of the following languages are regular, and can therefore be the pattern of a token recognised by a finite automaton? Select all that apply.

A. \(\{ a^{n} b^{n} \mid n \geq 0 \}\)
B. Binary strings that contain an even number of \(0\)s
C. Identifiers described by \(letter\,(letter \mid digit)^{*}\)
D. Strings of balanced parentheses

---

## Q3 — NAT

A scanner discards whitespace and does not emit a token for it. Identifiers match \([A\text{-}Za\text{-}z][A\text{-}Za\text{-}z0\text{-}9]^{*}\), numbers match \([0\text{-}9]^{+}\), and each of `=` and `+` is a separate token.

How many tokens are produced for the input below? Enter an integer.

```
rate2 = 10 + x
```

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

A scanner uses maximal munch. If two patterns match prefixes of equal length, the pattern listed earlier wins.

1. relop \(\to\) `<=` | `>=` | `==` | `<` | `>` | `=`
2. id \(\to\) \([A\text{-}Za\text{-}z][A\text{-}Za\text{-}z0\text{-}9]^{*}\)
3. num \(\to\) \([0\text{-}9]^{+}\)

Which token sequence is produced for `a>=b`?

A. id, relop(`>`), relop(`=`), id
B. id, relop(`>=`), id
C. relop(`>=`) only
D. id, relop(`>=`), relop(`=`), id

---

## Q5 — MCQ

How many strings of length exactly 3 belong to the language of the regular expression \((a \mid b)^{*}\, a\, (a \mid b)\)?

A. 2
B. 3
C. 4
D. 8

---

## Q6 — MSQ

Select all that apply.

A. Keywords are often recognised by the same pattern as identifiers, then distinguished by a keyword table.
B. When several token patterns match a prefix of the remaining input, maximal munch keeps the longest match.
C. A scanner implemented only as a DFA can check that parentheses are balanced to arbitrary depth.
D. The token patterns of a typical programming language are regular, so a DFA can implement the scanner.

---

## Q7 — MCQ

In the language below, an identifier matches \([A\text{-}Za\text{-}z][A\text{-}Za\text{-}z0\text{-}9]^{*}\), a number matches \([0\text{-}9]^{+}\), and `@` is not the start of any token. Which input contains a lexical error?

A. Two statements `int x = 1` and `int y = 2` written with no semicolon between them
B. The statement `x = y + ;`
C. The declaration `int 2ab = 1;`, tokenised as the number `2` followed by the identifier `ab`
D. The statement `x = @1;`

---

## Level 3 — Multi-Step

## Q8 — MCQ

Whitespace is discarded. Identifiers match \([A\text{-}Za\text{-}z][A\text{-}Za\text{-}z0\text{-}9]^{*}\), numbers match \([0\text{-}9]^{+}\), and each of `+`, `-`, `*`, and `/` is one token. How many tokens are produced for the input below?

```
Sum2 + 30 - x9 / 4
```

A. 5
B. 6
C. 7
D. 8

---

## Q9 — MCQ

A comment token is `/*`, then any characters, up to the nearest following `*/`. The pattern does not treat comments as nested. For the input

```
/* a /* b */ c */
```

what is the comment lexeme that starts at the first character?

A. `/* a /* b */`
B. `/* a /* b */ c */`
C. `/* a /*`
D. `/* a /* b */ c`

---

## Q10 — NAT

Maximal munch is used. On a tie in length, the earlier pattern wins. Whitespace is discarded and is not a token.

1. keyword \(\to\) `if` | `else`
2. id \(\to\) \([a\text{-}z][a\text{-}z0\text{-}9]^{*}\)
3. num \(\to\) \([0\text{-}9]^{+}\)

How many tokens are produced for `else2 if`? Enter an integer.

---

## Level 4 — Tricky / Trap-Based

## Q11 — MCQ

Which string belongs to the language of \((a \mid b)^{*}\) and does not belong to the language of \(a^{*} b^{*}\)?

A. `aaabbb`
B. `abab`
C. `bbb`
D. The empty string

---

## Q12 — MSQ

The remaining input is `aabbab`. Consider these patterns as candidates for a prefix of that input. Select all that apply.

A. \((a \mid b)^{*}\, ab\) matches the entire string `aabbab`.
B. \(a^{+} b^{+}\) matches a prefix of length 4.
C. \(b^{+}\) matches a nonempty prefix.
D. With maximal munch, and with \((a \mid b)^{*}\, ab\) as one of the token patterns, the first token can be the whole string.

---

## Level 5 — Challenge

## Q13 — NAT

How many strings of length exactly 5 does the regular expression \((aa \mid b)^{*}\) generate? Enter an integer.

---

## Q14 — MSQ

Maximal munch is used. If two patterns match the same length, the earlier pattern wins.

- T1: \(a b^{*} a\)
- T2: \(a b^{+}\)
- T3: \(b a^{+}\)

The input is `ababa`. Select all that apply.

A. The first token is T1, with lexeme `aba`.
B. The second token is T3, with lexeme `ba`.
C. A T2 token is emitted.
D. Exactly two tokens are emitted.

---

## Answer Key

| Q | Type | Answer |
| --- | --- | --- |
| 1 | MCQ | B |
| 2 | MSQ | B, C |
| 3 | NAT | 5 |
| 4 | MCQ | B |
| 5 | MCQ | C |
| 6 | MSQ | A, B, D |
| 7 | MCQ | D |
| 8 | MCQ | C |
| 9 | MCQ | A |
| 10 | NAT | 2 |
| 11 | MCQ | B |
| 12 | MSQ | A, B, D |
| 13 | NAT | 8 |
| 14 | MSQ | A, B, D |

## Detailed Solutions

### Q1

Answer: B

Lexical analysis is the phase that converts a character stream into a token stream. Syntax analysis consumes that token stream. Semantic analysis checks meaning, such as types and declarations. Intermediate-code generation runs after the front end has a syntax tree or an equivalent representation. Grouping characters into lexemes is the scanner’s job.

### Q2

Answer: B, C

A language can be a token pattern only if it is regular. Binary strings with an even number of \(0\)s are recognised by a two-state DFA, so B is regular. The identifier pattern \(letter\,(letter \mid digit)^{*}\) is a regular expression, so C is regular. \(\{ a^{n} b^{n} \mid n \geq 0 \}\) is a classic context-free language that is not regular: a DFA cannot remember an arbitrary count of \(a\)s. Balanced parentheses are not regular for the same reason; matching arbitrary nesting needs a stack and is the parser’s job. So A and D are not token patterns for a finite-automaton scanner.

### Q3

Answer: 5

The input splits, after discarding the spaces, as follows.

| Lexeme | Token |
| --- | --- |
| `rate2` | identifier |
| `=` | operator |
| `10` | number |
| `+` | operator |
| `x` | identifier |

That is five tokens. The letters and digits of `rate2` stay in one identifier because the identifier pattern allows digits after the first letter, and maximal munch takes the whole word.

### Q4

Answer: B

From the start of `a>=b`, the identifier pattern matches `a` (length 1). The next two characters are `>=`. The relop pattern matches `>=` (length 2), and it also matches the shorter prefix `>`. Maximal munch keeps `>=`. The last character `b` is an identifier. The sequence is id, relop(`>=`), id. Splitting `>=` into `>` and `=` violates longest match.

### Q5

Answer: C

The expression \((a \mid b)^{*}\, a\, (a \mid b)\) is every string of length at least 2 whose second-to-last symbol is \(a\). For length 3 the middle symbol is fixed as \(a\), and the first and last symbols are free: `aaa`, `aab`, `baa`, `bab`. There are \(2 \times 2 = 4\) such strings.

### Q6

Answer: A, B, D

Keywords are regular, but writing a separate pattern for every keyword is unnecessary. Scanners usually let the identifier regex accept the spelling, then look the lexeme up in a keyword table. Maximal munch is the usual disambiguation rule when several prefixes match. Token classes such as identifiers, numbers, and operators are regular, so the scanner can be a DFA. Balanced parentheses of unbounded depth are not regular, so a DFA scanner cannot check them. That check belongs to the parser. C is false.

### Q7

Answer: D

A lexical error occurs when the remaining characters do not form any token. In D, `@` matches no pattern, so the error is lexical. In A, every character forms a legal token; the missing semicolon is a syntax error. In B, `x`, `=`, `y`, `+`, and `;` are all legal tokens; the arrangement is a syntax error. In C, maximal munch produces the number `2` and the identifier `ab`. Both are legal tokens. A declaration that places a number where an identifier is required is a syntax error, not a lexical error.

### Q8

Answer: C

The seven lexemes are `Sum2`, `+`, `30`, `-`, `x9`, `/`, and `4`. `Sum2` is one identifier, not an identifier followed by a number, because digits may continue an identifier. `x9` is likewise one identifier. Spaces are discarded.

### Q9

Answer: A

The comment pattern closes at the nearest `*/`. Scanning from the opening `/*`, the first closing delimiter is the one after `b`. The lexeme is `/* a /* b */`. The inner `/*` is ordinary comment text because this pattern does not nest. The trailing ` c */` is not part of this token. Choosing the last `*/` would be a longest match that the stated “nearest closer” rule does not use.

### Q10

Answer: 2

At `else2`, the keyword pattern matches `else` (length 4). The identifier pattern matches `else2` (length 5), because digits may continue an identifier. Maximal munch keeps the identifier `else2`. After the space, `if` matches the keyword pattern of length 2. It also matches the identifier pattern of length 2, and the keyword rule is listed first, so the token is the keyword `if`. The tokens are id(`else2`) and keyword(`if`): two tokens. Taking the keyword `else` and then the number `2` would throw away a longer identifier match.

### Q11

Answer: B

\(a^{*} b^{*}\) is the set of strings that are zero or more \(a\)s followed by zero or more \(b\)s. A \(b\) may not be followed by an \(a\). The string `abab` has a \(b\) followed by an \(a\), so it is not in \(a^{*} b^{*}\), but it is in \((a \mid b)^{*}\). The string `aaabbb` is in both. The string `bbb` is \(a^{0} b^{3}\), so it is in both. The empty string is in both, as zero \(a\)s and zero \(b\)s.

### Q12

Answer: A, B, D

For P1, \((a \mid b)^{*}\, ab\) matches any string that ends in `ab`. The string `aabbab` ends in `ab`, and the prefix `aabb` is in \((a \mid b)^{*}\), so the whole string matches. The shortest match would be the prefix `aab`, but the expression itself also matches the longer string. For P2, \(a^{+} b^{+}\) matches `aabb` and then stops, because the next character is `a`. That prefix has length 4. For P3, \(b^{+}\) requires the prefix to start with `b`, but `aabbab` starts with `a`, so there is no nonempty match. Under maximal munch, P1’s match has length 6, which is longer than P2’s match of length 4, so the first token is the entire string.

### Q13

Answer: 8

Every string is a concatenation of blocks `aa` (length 2) and `b` (length 1) whose lengths sum to 5. If \(k\) blocks are `aa`, then \(5 - 2k\) blocks are `b`, and \(k \in \{0, 1, 2\}\).

- \(k = 0\): `bbbbb`. One string.
- \(k = 1\): one `aa` and three `b`s, arranged in \(1 + 3 = 4\) block positions. \(\binom{4}{1} = 4\) strings. The block sequences `aa b b b`, `b aa b b`, `b b aa b`, and `b b b aa` spell `aabbb`, `baabb`, `bbaab`, and `bbbaa`.
- \(k = 2\): two `aa` blocks and one `b`, in \(3\) positions. \(\binom{3}{1} = 3\) strings: `b` then two `aa` gives `baaaa`; `aa`, `b`, `aa` gives `aabaa`; two `aa` then `b` gives `aaaab`.

Total: \(1 + 4 + 3 = 8\). The eight strings are `bbbbb`, `aabbb`, `baabb`, `bbaab`, `bbbaa`, `baaaa`, `aabaa`, and `aaaab`.

### Q14

Answer: A, B, D

At the start of `ababa`:

- T1 is \(a b^{*} a\). The \(b^{*}\) can take the single `b`, and the final `a` matches, giving `aba` (length 3). It cannot take the later `b`, because another `a` would have to sit inside \(b^{*}\).
- T2 is \(a b^{+}\), which matches `ab` (length 2).
- T3 requires an initial `b`, so it fails.

The longest match is T1 with lexeme `aba`. The remaining input is `ba`.

- T1 and T2 require an initial `a`, so they fail.
- T3 matches `ba`.

The scanner emits T1 then T3, and it never emits T2. That is exactly two tokens.
