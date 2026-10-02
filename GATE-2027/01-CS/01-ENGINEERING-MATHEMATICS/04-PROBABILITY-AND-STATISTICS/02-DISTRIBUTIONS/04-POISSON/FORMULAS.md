# Poisson Distribution — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| PMF | e^{−λ}λ^k/k! | k=0,1,2,… | λ>0 | Binomial limit | Rare events | Wrong k range |
| Mean=Var | λ | — | Identifying feature | PMF properties | MSQ identification | Assuming always normal |
| Time scale | Poisson(λt) | Rate λ per unit | — | Poisson process | Interval problems | Forgetting t |
| Binomial approx | Poisson(np) | n large, p small | np moderate | Rare event limit | 1000,0.002→Poi(2) | p not small |
