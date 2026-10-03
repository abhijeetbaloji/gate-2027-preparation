# Tabular Method — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

## Level 1 — Conceptual

## Q1 — MCQ

In the Quine–McCluskey tabular method, two implicants are combined when

A. their labels differ in exactly one bit position

B. their labels differ in exactly two bit positions

C. they contain the same number of 1s

D. both implicants are don't cares

---

## Q2 — MSQ

Select all that apply. Which statements about the tabular method are true?

A. Don't-care minterms may be used when implicants are combined.

B. A don't-care minterm need not be covered by the final expression.

C. An implicant that has been combined into a larger implicant is not prime.

D. Every prime implicant appears in every minimal sum of products.

---

## Q3 — NAT

For \(f(A, B, C) = \sum m(0, 7)\), the number of prime implicants is ______.

---

## Level 2 — Standard GATE Style

## Q4 — MCQ

Minterms \(m_5 = 0101\) and \(m_{13} = 1101\) of a four-variable function combine to the implicant

A. \(BC'D\)

B. \(B'C'D\)

C. \(ACD\)

D. \(BD'\)

---

## Q5 — NAT

For

\[
f(A, B, C, D) = \sum m(4, 5, 6, 8, 9, 10, 12, 13, 14),
\]

the number of essential prime implicants is ______.

---

## Q6 — MSQ

Select all that apply. For the function in Q5,

A. \(BD'\) is an essential prime implicant

B. \(BC'\) is an essential prime implicant

C. \(AB\) is a prime implicant

D. every minimal sum of products has four product terms

---

## Level 3 — Multi-Step

## Q7 — MCQ

A minimal sum of products of

\[
f(A, B, C, D) = \sum m(0, 1, 2, 5, 6, 7, 8, 9, 10, 14)
\]

is

A. \(CD' + B'C' + A'BD\)

B. \(CD' + B'C'\)

C. \(B'D' + B'C' + A'BC\)

D. \(CD' + B'D' + A'BD\)

---

## Q8 — NAT

The number of prime implicants of the function in Q7 is ______.

---

## Level 4 — Tricky / Trap-Based

## Q9 — MSQ

Select all that apply. For

\[
f(A, B, C, D) = \sum m(0, 4, 5, 7, 8, 12) + d(1, 9, 13),
\]

A. don't-care minterms may be paired during the combination stages

B. a minimal sum of products is \(C' + A'BD\)

C. if every don't care is forced to 0, the resulting literal-minimum expression on that smaller onset is still \(C' + A'BD\)

D. minterm 7 must be covered, while minterm 1 need not be covered

---

## Q10 — MCQ

For the function in Q7, which statement is correct?

A. \(A'BD\) is essential because it belongs to the only minimal sum of products.

B. \(A'BD\) is not essential, although every minimal sum of products contains it.

C. \(CD'\) is not essential.

D. \(B'D'\) is essential.

---

## Level 5 — Challenge

## Q11 — NAT

The unique minimal sum of products of the function in Q7 has ______ literal occurrences.

---

## Q12 — MSQ

Select all that apply. The tabular method is applied to

\[
f(A, B, C) = \sum m(0, 1, 2, 5, 6, 7).
\]

A. It produces 6 prime implicants.

B. It produces 0 essential prime implicants.

C. One minimal sum of products is \(A'B' + BC' + AC\).

D. As soon as \(m_0\) has been combined with another minterm, \(m_0\) can be deleted from the covering chart.

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MSQ | A, B, C |
| 3 | NAT | 2 |
| 4 | MCQ | A |
| 5 | NAT | 4 |
| 6 | MSQ | A, B, D |
| 7 | MCQ | A |
| 8 | NAT | 6 |
| 9 | MSQ | A, B, D |
| 10 | MCQ | B |
| 11 | NAT | 7 |
| 12 | MSQ | A, B, C |

## Detailed Solutions

### Q1

Answer: **A**

Two implicants combine when their bit labels differ in one position and agree everywhere else, including the positions that are already dashed. The resulting label puts a dash in the bit that was eliminated. Differing in two bits is the condition for a quad only after two separate pairings; those two minterms do not combine directly. Two implicants with the same number of 1s differ in an even number of bits, so they are not a legal pair. Don't cares are optional fuel for combinations, not the combining rule.

### Q2

Answer: **A, B, C**

Don't cares are inserted into the combination tables so that larger cubes can form. They are omitted from the prime-implicant chart, because the specification does not require them to be 1. During combination, every implicant that participates in a successful merge is checked off. Checked implicants are not prime. Only the unchecked implicants that still cover at least one required minterm are prime.

Option (D) is false. A nonessential prime is absent from at least one minimal sum. Only an essential prime implicant, one that alone covers some required minterm, belongs to every minimal sum.

### Q3

Answer: **2**

\(m_0 = 000\) and \(m_7 = 111\) differ in all three bits. They cannot be combined, and there is no third minterm to bridge them. Each required minterm is an unchecked implicant at the end of the table, so there are two prime implicants, \(A'B'C'\) and \(ABC\). The trap is to treat "far apart on the number line" as irrelevant and answer 1, or to imagine a quad that the onset does not contain.

### Q4

Answer: **A**

\(0101\) and \(1101\) differ only in the \(A\) bit. The combined label is \(-101\), which is \(B = 1\), \(C = 0\), \(D = 1\), written \(BC'D\). Option (B) flips \(B\). Option (C) keeps \(A\), the bit that was eliminated. Option (D) keeps the wrong fixed bits: \(BD'\) is \(-1-0\), not \(-101\).

### Q5

Answer: **4**

Sorting the onset by the number of 1s and combining until nothing new merges leaves four unchecked implicants:

| Prime | Pattern | Required minterms |
|---|---|---|
| \(BD'\) | \(-1-0\) | \(m_4, m_6, m_{12}, m_{14}\) |
| \(BC'\) | \(-10-\) | \(m_4, m_5, m_{12}, m_{13}\) |
| \(AD'\) | \(1--0\) | \(m_8, m_{10}, m_{12}, m_{14}\) |
| \(AC'\) | \(1-0-\) | \(m_8, m_9, m_{12}, m_{13}\) |

Each is the unique cover of some minterm: \(m_6\) is only in \(BD'\), \(m_9\) is only in \(AC'\), \(m_{10}\) is only in \(AD'\), and \(m_5\) is only in \(BC'\). All four primes are essential.

### Q6

Answer: **A, B, D**

\(BD'\) and \(BC'\) are two of the four essential primes from Q5, so both (A) and (B) hold, and every minimal sum must take all four primes. That sum has four product terms.

\(AB\) would be the cube \(11-- = \{m_{12}, m_{13}, m_{14}, m_{15}\}\). Minterm \(m_{15}\) is not in the onset, so \(AB\) is not even an implicant. A dash pattern generated by a legal merge never covers a non-onset, non-don't-care minterm; \(AB\) simply is not one of those merges.

### Q7

Answer: **A**

The six primes are

| Prime | Covers |
|---|---|
| \(CD'\) | \(m_2, m_6, m_{10}, m_{14}\) |
| \(B'D'\) | \(m_0, m_2, m_8, m_{10}\) |
| \(B'C'\) | \(m_0, m_1, m_8, m_9\) |
| \(A'C'D\) | \(m_1, m_5\) |
| \(A'BD\) | \(m_5, m_7\) |
| \(A'BC\) | \(m_6, m_7\) |

\(CD'\) is the only prime on \(m_{14}\), and \(B'C'\) is the only prime on \(m_9\). After those two essential primes are selected, \(m_5\) and \(m_7\) remain. The single prime \(A'BD\) covers both. The resulting sum is \(CD' + B'C' + A'BD\).

Option (B) misses \(m_5\) and \(m_7\). Option (C) misses \(m_5\) and \(m_{14}\). Option (D) misses \(m_1\) and \(m_9\), because \(B'D'\) has \(D = 0\) while those two minterms have \(D = 1\).

### Q8

Answer: **6**

The combination stages leave exactly the six unchecked patterns listed in Q7. None of them contains another, so all six are prime. Counting only the essential ones undercounts by four. Counting every intermediate pair, including pairs that were later checked off, overcounts.

### Q9

Answer: **A, B, D**

The care minterms are \(0, 4, 5, 7, 8, 12\). The don't cares \(1, 9, 13\) enter the combination table only. The unchecked primes that meet the onset are \(C'\) (the cube with only \(C\) fixed at 0, using don't cares \(1, 9, 13\)) and \(A'BD\) (pattern \(01-1\)). They are essential: \(m_0\) lies only in \(C'\), and \(m_7\) lies only in \(A'BD\). The minimal sum is \(C' + A'BD\), with four literal occurrences. Minterm 7 is required. Minterm 1 is a don't care, so the final cover may include it but need not be charged with covering it.

Forcing the don't cares to 0 removes \(C'\), because that cube contains \(m_1, m_9, m_{13}\). The literal-minimum sum on the reduced onset is \(C'D' + A'BD\), which has five literals. It satisfies the original care rows, but it is not the literal minimum available when don't cares may be 1. Option (C) is the don't-care misuse: treating \(X\) as a required 0 throws away a larger legal cube.

### Q10

Answer: **B**

By definition, a prime is essential when at least one required minterm lies in no other prime. In Q7, \(m_5\) also lies in \(A'C'D\), and \(m_7\) also lies in \(A'BC\). Therefore \(A'BD\) is not essential.

It is still present in every minimal sum. The two essential primes \(CD'\) and \(B'C'\) leave \(\{m_5, m_7\}\). Covering those two with other primes takes both \(A'C'D\) and \(A'BC\), which yields a four-term sum. The only three-term sum uses \(A'BD\). "Belongs to every minimum-cost cover" is a consequence one must check; it is not the definition that makes a prime essential. Option (A) uses that incorrect definition.

\(CD'\) uniquely covers \(m_{14}\), so (C) is false. \(B'D'\) covers only minterms that \(CD'\) or \(B'C'\) also cover, and the minimal sum does not use it, so (D) is false.

### Q11

Answer: **7**

The only minimal sum is \(CD' + B'C' + A'BD\). The literal counts are 2, 2 and 3, and the total is 7. Any cover that avoids \(A'BD\) needs at least four primes. Even if those primes were as small as two literals each, the cost would be at least 8, which is worse. So 7 is the literal minimum, not merely the term minimum.

### Q12

Answer: **A, B, C**

Group the onset by the number of 1s:

- 0 ones: \(m_0 = 000\)
- 1 one: \(m_1 = 001\), \(m_2 = 010\)
- 2 ones: \(m_5 = 101\), \(m_6 = 110\)
- 3 ones: \(m_7 = 111\)

The legal pairs, and there is no quad, are

\[
\begin{align*}
m_0, m_1 &\to A'B', \\
m_0, m_2 &\to A'C', \\
m_1, m_5 &\to B'C, \\
m_2, m_6 &\to BC', \\
m_5, m_7 &\to AC, \\
m_6, m_7 &\to AB.
\end{align*}
\]

These six implicants are unchecked, so they are the primes. Every onset minterm sits in two of them, so none is essential. One minimum cover of three primes is \(A'B'\) on \(\{m_0, m_1\}\), \(BC'\) on \(\{m_2, m_6\}\) and \(AC\) on \(\{m_5, m_7\}\). The other is \(A'C' + B'C + AB\).

Option (D) confuses the two tables. Combining \(m_0\) with \(m_1\) checks off those smaller implicants so they are not listed as primes. The covering chart is built afterwards, and its columns are the required minterms. A column is covered only when a selected prime contains it. Forming a pair does not by itself delete the column.
