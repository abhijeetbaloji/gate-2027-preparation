# System of Linear Equations — Revision Sheet

Use **after** studying `NOTES.md`.

## Form

Ax = b; augmented [A|b].

## Rouché–Capelli

| rank(A) vs rank([A|b]) | vs n | Result |
|------------------------|------|--------|
| equal = n | | Unique |
| equal < n | | Infinite |
| rank(A) < rank([A|b]) | | No solution |

## Homogeneous Ax=0

- Always x=0.
- Non-trivial iff rank(A) < n.
- Nullity = n − rank(A) = free variables.

## Methods

- Gaussian elimination → REF → back-substitute.
- Gauss–Jordan → RREF.
- x = A^{-1}b if A invertible.

## Traps

- Underdetermined ≠ always infinite (check consistency).
- Overdetermined can be inconsistent.
- Row ops preserve solution set (not det unchanged for scaled rows in det context).

## Mini example

rank(A)=rank([A|b])=2, n=3 → one free variable → infinite solutions.
