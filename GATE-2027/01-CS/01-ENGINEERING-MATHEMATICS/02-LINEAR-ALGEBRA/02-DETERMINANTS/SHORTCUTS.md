# Determinants — Shortcuts

## 1. Two identical/proportional rows → det 0

- **Why it works**: rows linearly dependent ⇒ volume collapses to 0.
- **When to use**: instant answer in MCQs.
- **Trap**: must be exact proportionality; near-equal rows need full compute.

## 2. Row-reduce to triangular

- **Why it works**: triangular det is diagonal product; track swaps (sign) and scaling.
- **When to use**: 3×3 and larger.
- **Trap**: row addition is safe; row scaling multiplies det.

## 3. Eigenvalue product = det(A)

- **Why it works**: characteristic polynomial constant term.
- **When to use**: when eigenvalues are known or easily found.
- **Trap**: repeated eigenvalues still multiply correctly.

## 4. Block triangular determinant

- **Why it works**: det [[A,0],[0,B]] = det(A)det(B).
- **When to use**: block-structured matrices.
- **Trap**: only when off-diagonal blocks are zero.

## 5. det of orthogonal = ±1

- **Why it works**: det(A)² = det(AᵀA) = det(I) = 1.
- **When to use**: rotation/reflection matrices.
- **Trap**: both +1 and −1 possible.
