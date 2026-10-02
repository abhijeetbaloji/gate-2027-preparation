# LU Decomposition — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| A = LU | LU factorization | A square | No zero pivot w/o swap | Gaussian elimination | Setup | Swapping L,U roles |
| PA = LU | Pivoting | A square | Pivoting used | Row permutations | Stability | Forgetting P on b |
| Ly = b | Forward solve | L unit lower | — | Substitution | Step 1 of solve | Wrong order |
| Ux = y | Back solve | U upper | — | Substitution | Step 2 | Solving Ux=b first |
| det(A)=Π u_{ii} | Determinant via U | P=I | LU exists | det(L)=1 | Quick det | Ignoring P sign |
| ℓ_{ik}=a_{ik}/a_{kk} | Multiplier | Column k | a_{kk}≠0 | Elimination | Build L | Using wrong pivot |
| Cost ~2n³/3 | Factorization flops | Large n | — | Analysis | Compare methods | Expecting O(n²) factor |
