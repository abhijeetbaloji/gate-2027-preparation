# System of Linear Equations — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| Ax = b | Matrix form | A: m×n | — | Definition | Setup | Dimension mismatch |
| rank(A)=rank([A\|b])=n | Unique solution | Square or general | Consistent | Rouché–Capelli | Count solutions | Ignoring b |
| rank(A)=rank([A\|b])<n | Infinite solutions | — | Consistent | Free variables | Parameterize | Forgetting free vars |
| rank(A)<rank([A\|b]) | No solution | — | Inconsistent | Pivot in b col | MSQ | Assuming m<n ⇒ infinite |
| Nullity = n − rank(A) | Free variable count | — | — | Dimension theorem | Homogeneous | Confusing with m |
| x = A^{-1}b | Inverse method | A: n×n | det(A)≠0 | Multiply both sides | Small n | Using when singular |
| x_i = det(A_i)/det(A) | Cramer's rule | Square | det≠0 | Determinants | 2×2/3×3 | When det=0 |
