# Binomial Distribution — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| PMF | C(n,k)p^k(1−p)^{n−k} | k=0..n | Independent trials | Count successes | n trials | Dependent trials |
| Mean | np | — | Linearity | Σ Bernoulli | Expected successes | — |
| Variance | np(1−p) | — | Sum of Bernoulli var | Spread | SD=√(np(1−p)) | — |
| At least one | 1−(1−p)^n | — | Complement | Avoid summation | Reliability | Summing PMF |
