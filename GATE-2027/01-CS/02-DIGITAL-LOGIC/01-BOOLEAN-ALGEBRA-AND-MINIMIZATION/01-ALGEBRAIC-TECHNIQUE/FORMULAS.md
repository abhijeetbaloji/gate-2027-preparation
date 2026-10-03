# Boolean Algebra (Algebraic Technique) — Formulas

The reasons are in `NOTES.md`.

## Counts

| Formula | Meaning | Condition |
|---------|---------|-----------|
| \(2^{2^n}\) | Number of distinct Boolean functions of \(n\) variables | Each of the \(2^n\) rows is 0 or 1 |
| \(2^{2^{n-1}}\) | Number of self-dual functions of \(n\) variables | \(F(\text{complement of inputs}) = \text{complement of } F\) |
| \(2^n\) | Number of minterms, and of maxterms | \(n\) variables |
| \(2^n - \|onset\|\) | Number of minterms of \(F'\) | No don’t-cares. With don’t-cares, unspecified rows are not onset |

## Laws

| Law | Statement | When to use |
|-----|-----------|-------------|
| Idempotent | \(x+x = x\), \(xx = x\) | Delete a repeated term or literal |
| Complement | \(x+x' = 1\), \(xx' = 0\) | A variable and its complement |
| Null | \(x+1 = 1\), \(x\cdot 0 = 0\) | A term ORed with 1, or ANDed with 0 |
| Absorption | \(x+xy = x\) | A product contains a shorter term already present |
| Covering | \(x + x'y = x+y\) | One term is a single literal, the other contains its complement |
| Distributive (both) | \(x(y+z)=xy+xz\), \(x+yz=(x+y)(x+z)\) | Factor or expand. The second has no ordinary-algebra analogue |
| Consensus | \(xy + x'z + yz = xy + x'z\) | Drop the term that uses neither \(x\) nor \(x'\) alone, when the other two products are present |
| De Morgan | \((x+y)'=x'y'\), \((xy)'=x'+y'\) | Complement a sum or a product. Extends to any arity |
| Shannon | \(F = x F(1) + x' F(0)\) | Split on one variable. \(F(1), F(0)\) are cofactors |
| Shannon POS | \(F = (x + F(0))(x' + F(1))\) | Same split, written as a product of sums |

## XOR

| Formula | Meaning |
|---------|---------|
| \(x \oplus y = x'y + xy'\) | 1 exactly when the bits differ |
| \(x \oplus y = (x+y)(x'+y')\) | Same function, factored |
| \(x \odot y = xy + x'y' = (x \oplus y)'\) | 1 exactly when the bits agree |
| \(x \oplus 0 = x\), \(x \oplus 1 = x'\), \(x \oplus x = 0\) | Constants and cancellation |
| \(x \oplus y \oplus z\) | 1 when an odd number of inputs are 1 |
| Majority \(ab+bc+ca\) | 1 when at least two of \(a,b,c\) are 1. Not the same as XOR of the three |

**Example.** \(1 \oplus P = P'\). So a leading \(1 \oplus\) complements the rest of an XOR chain only after associativity is applied carefully: \((1 \oplus P) \oplus Q = P' \oplus Q\).

## Dual

Swap \(+\) and \(\cdot\). Swap 0 and 1. Do not complement variables. The dual of a theorem is a theorem.

## Minterm index

If \(A\) is the MSB, the minterm for bits \(A B C =\) binary of \(i\) is \(m_i\). Example: \(m_5 = AB'C\) when the row is 101.

## Gate conversions used with these formulas

| Target | Built from 2-input NOR | Gate count if complements are not free |
|--------|------------------------|----------------------------------------|
| NOT \(x\) | \((x+x)'\) | 1 |
| OR | NOR, then NOT | 2 |
| AND \(xy\) | invert both inputs, then NOR | 3 |

Counts change when the stem says complements are already available. Minimize the expression before converting.
