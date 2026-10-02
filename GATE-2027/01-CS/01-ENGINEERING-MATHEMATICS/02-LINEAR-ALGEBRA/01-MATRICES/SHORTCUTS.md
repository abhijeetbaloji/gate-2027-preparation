# Matrices — Shortcuts

## 1. 2×2 inverse by swap-and-negate

- **Why it works**: cofactor formula collapses to swapping diagonal and negating off-diagonal, scaled by 1/det.
- **When to use**: 2×2 invertibility or inverse MCQs.
- **Trap**: only valid when det ≠ 0; does not generalize to 3×3 without cofactors.

## 2. Zero row/column ⇒ singular

- **Why it works**: expanding det along that row/column gives 0.
- **When to use**: instant elimination in "is A invertible?" questions.
- **Trap**: converse false — singular matrices may have no obvious zero row.

## 3. Diagonal matrix powers

- **Why it works**: (diag(d₁,…,dₙ))ᵏ = diag(d₁ᵏ,…,dₙᵏ).
- **When to use**: Aᵏ when A is diagonal or easily diagonalizable.
- **Trap**: off-diagonal entries do not power independently.

## 4. Block-diagonal multiply

- **Why it works**: blocks act independently.
- **When to use**: structured matrices in GATE.
- **Trap**: block sizes must align; off-diagonal blocks must be zero.

## 5. Trace shortcut for 2×2 eigenvalues

- **Why it works**: tr(A) = λ₁+λ₂, det(A) = λ₁λ₂.
- **When to use**: find eigenvalues without full characteristic polynomial.
- **Trap**: works for 2×2 quickly; for 3×3 use full det(A−λI).
