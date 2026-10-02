# Recurrence Relations — Formulas

Reference only. Learn concepts in `NOTES.md` first.


| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| r^k+c₁r^{k−1}+…=0 | Characteristic | Order k | Constant coeffs | Substitute a_n=r^n | Homogeneous sol | Wrong polynomial |
| a_n=Σ C_i r_i^n | Distinct roots | — | Distinct r_i | Linear combo | Closed form | Missing IC solve |
| T(n)=aT(n/b)+f(n) | Divide-conquer | a,b constant | Regularity | Master theorem | Algo analysis | Case mis-pick |
