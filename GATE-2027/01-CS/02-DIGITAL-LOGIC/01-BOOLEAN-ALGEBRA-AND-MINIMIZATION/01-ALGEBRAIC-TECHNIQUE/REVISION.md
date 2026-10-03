# Boolean Algebra (Algebraic Technique) — Revision

Use after `NOTES.md`.

## Counts

| Object | Formula |
|--------|---------|
| Functions of \(n\) variables | \(2^{2^n}\) |
| Self-dual functions of \(n\) variables | \(2^{2^{n-1}}\) |
| Minterms of \(n\) variables | \(2^n\) |
| Minterms of \(F'\) | \(2^n\) minus the number of onset rows of \(F\) |

## Identities to apply without re-deriving

- \(x+x = x\), \(xx = x\), \(x+x' = 1\), \(xx' = 0\)
- \(x+1 = 1\), \(x\cdot 0 = 0\), \(x+0 = x\), \(x\cdot 1 = x\)
- \(x+xy = x\), \(x(x+y) = x\)
- \(x + x'y = x+y\)
- \(xy + x'z = xy + x'z + yz\) (the \(yz\) term is optional)
- \((x+y)' = x'y'\), \((xy)' = x'+y'\)
- \(x + yz = (x+y)(x+z)\)
- \(x \oplus y = x'y + xy' = (x+y)(x'+y')\)
- \(x \odot y = xy + x'y' = (x \oplus y)'\)
- \(x \oplus 0 = x\), \(x \oplus 1 = x'\), \(x \oplus x = 0\)

## Dual

Swap \(+\) with \(\cdot\), and 0 with 1. Leave variables uncomplemented. Dual of an identity is an identity.

## Canonical forms

- \(m_i\) is the product for input row \(i\). \(M_i = m_i'\).
- \(\sum m(\ldots)\) lists rows of 1. \(\prod M(\ldots)\) lists rows of 0.
- Literal = one occurrence of a variable or its complement.

## Cofactors

\(F = x F(1) + x' F(0) = (x + F(0))(x' + F(1))\).

## Prime vs essential

- Prime: implicant that cannot lose a literal.
- Essential: the only prime that covers some required onset minterm.
- Don’t-care: may be used, need not be covered.

## Hazard

\(xy + x'z\) equals \(xy + x'z + yz\). In two-level AND-OR, the extra \(yz\) removes the static-1 hazard when \(x\) switches and \(y = z = 1\).

## Fast checks

- One failing input row kills a claimed identity.
- \(n \le 3\): write the table.
- Absorption drops a longer product. Covering \(x+x'y\) keeps \(y\).
- Majority of three inputs is \(ab+bc+ca\). Parity is \(a \oplus b \oplus c\).

## Traps

- \((x+y)'\) is not \(x'+y'\).
- XOR is not \(xy+x'y'\).
- Self-dual count is \(2^{2^{n-1}}\), not \(2^{n-1}\).
- “Minimal” can mean fewest products, fewest literals, or fewest gates. The stem says which.
