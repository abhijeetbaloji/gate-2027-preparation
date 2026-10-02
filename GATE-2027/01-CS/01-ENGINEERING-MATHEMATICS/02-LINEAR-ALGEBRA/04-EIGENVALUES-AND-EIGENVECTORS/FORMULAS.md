# Eigenvalues and Eigenvectors — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| det(A−λI)=0 | Characteristic equation | Square A | — | Eigenvalue def | Find λ | Sign errors in det |
| Av=λv | Eigenpair | v≠0 | — | Definition | Verify candidate | Accepting v=0 |
| Σλᵢ=tr(A) | Trace-eigenvalue sum | Square A | Over ℂ | Char poly coeff | Quick sum | Using on rectangular |
| Πλᵢ=det(A) | Product relation | Square A | — | Constant term | Quick det | Missing λ=0 factor |
| (A−λI)v=0 | Eigenspace | Each λ | — | Homogeneous | Find v | Full solve skip |
| A^k=PD^kP^{-1} | Diagonalization power | A diagonalizable | P cols = eigenvectors | A=PDP^{-1} | Compute A^n | Using when not diag. |
| A=QΛQ^T | Spectral theorem | A real symmetric | Q orthogonal | Symmetry | Orthogonal diag | Q not orthogonal |
| geom mult = n−rank(A−λI) | Eigenspace dimension | — | — | Nullity | Diagonalizability | Confusing with algebraic |
