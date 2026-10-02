# Random Variables — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| E[X] discrete | Σ x·p(x) | x: values | — | Definition | Expectation MCQs | Forgetting weights |
| Var(X) | E[X²]−(E[X])² | — | — | Expand (X−μ)² | Given moments | Using E[X]² alone |
| E[aX+b] | aE[X]+b | a,b constants | — | Linearity | Transformations | Adding b inside Var |
| Var(aX+b) | a²Var(X) | — | — | Shift irrelevant | Scaling | Forgetting a² |
| Independent sum | Var(X+Y)=Var(X)+Var(Y) | X,Y independent | Cov=0 | Variance additivity | Sums of RVs | Without independence |
