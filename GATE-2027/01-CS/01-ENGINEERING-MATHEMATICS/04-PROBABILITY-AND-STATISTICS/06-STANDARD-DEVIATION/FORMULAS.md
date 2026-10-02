# Standard Deviation — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| Var(X)=E[X²]−(E[X])² | Computational variance | — | E[X²] exists | Expand (X−μ)² | PMF/data variance | Forgetting square on E[X] |
| σ=√Var(X) | Standard deviation | — | Var≥0 | Definition | Units match X | Using σ² as σ |
| Var(aX+b)=a²Var(X) | Scaling | a,b constant | — | Spread scales by \|a\| | SD(3X+2) | Adding b to SD |
| SD(aX+b)=\|a\|σ | SD scaling | — | — | Square root of above | Linear transform | σ_X+σ_Y for sum |
| Var(X+Y)=Var(X)+Var(Y) | Sum variance | — | **Independent** | Cov=0 | SD(X+Y) | Dependent case |
| Binomial | np(1−p) | n,p | X~Bin(n,p) | n Bernoulli sums | Bin SD | Using np for var |
| Poisson | λ | X~Poisson(λ) | — | Limit of Binomial | SD=√λ | Confusing mean/var |
| Uniform [a,b] | (b−a)²/12 | a<b | Continuous uniform | Integration | Spread on interval | Wrong formula |
| Normal N(μ,σ²) | σ² | — | — | Definition | Notation trap | σ vs σ² |
