# Exponential Distribution — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| PDF | λe^{−λx} | x≥0 | λ>0 | Constant hazard | Wait times | x<0 support |
| CDF | 1−e^{−λx} | x≥0 | — | Integrate PDF | P(X≤t) | — |
| Mean | 1/λ | — | — | Reciprocal rate | Identify β | Confusing λ and 1/λ |
| Memoryless | P(X>s+t|X>s)=P(X>t) | — | Unique property | Conditional survival | GATE favourite | Applying to Normal |
