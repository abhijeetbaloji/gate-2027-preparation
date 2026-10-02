# Continuity and Differentiability — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| Continuous at a | lim f(x)=f(a) | a in domain | Limit exists | Definition | Piecewise k | Value only, not limit |
| f'(a)=lim [f(a+h)−f(a)]/h | Derivative | h→0 | Limit exists | Difference quotient | Slope at a | Left≠right derivative |
| Differentiable ⇒ continuous | Stronger property | at a | f' exists | MVT-style proof | Eliminate MCQs | Reverse implication |
| (fg)'=f'g+fg' | Product rule | — | Differentiable | Log trick / limit | Products | Wrong order |
| (f/g)'=(f'g−fg')/g² | Quotient rule | g≠0 | Differentiable | Product on f·g⁻¹ | Rational derivatives | Sign error |
| (f∘g)'=f'(g)·g' | Chain rule | — | Composable | Δy/Δx chain | sin(2x), e^{x²} | Forget inner g' |
| ln y=g ln f; y'/y=... | Log differentiation | f,g>0 where needed | Implicit diff | ln both sides | x^x | Domain x>0 |
| \|x−a\| corner | Non-diff at a | — | — | One-sided slopes | \|x\| at 0 | Claiming differentiable |
