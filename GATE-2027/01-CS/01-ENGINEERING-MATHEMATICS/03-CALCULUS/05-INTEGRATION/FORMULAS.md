# Integration — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| ∫x^n dx = x^{n+1}/(n+1)+C | Power rule | n≠−1 | — | Reverse power rule | Polynomials | n=−1 case |
| ∫_a^b f = F(b)−F(a) | FTC Part 2 | F'=f | f continuous on [a,b] | FTC | Evaluate definite | Wrong antiderivative |
| F'(x)=f(x) for F=∫_a^x f | FTC Part 1 | f continuous | [a,b] | MVT on integrals | Derivative of integral | Discontinuous f |
| ∫u dv = uv−∫v du | Integration by parts | — | Differentiable u,v | Product rule reverse | ∫x e^x, ln x | Wrong u,dv choice |
| u=g(x), ∫f(g)g'dx=∫f(u)du | Substitution | g differentiable | du=g'dx present | Chain rule reverse | Composite integrands | Missing g' factor |
| f_avg=(1/(b−a))∫_a^b f | Average value | b>a | Integrable f | Definition | Mean of function | Wrong interval length |
| ∫_a^b f+∫_a^b g=∫_a^b(f+g) | Linearity | — | Integrable | Sum rule | Split integrals | Sign errors |
| Area=∫_a^b (top−bottom) dx | Between curves | f≥g on [a,b] | — | Geometric | Area problems | Wrong order |
