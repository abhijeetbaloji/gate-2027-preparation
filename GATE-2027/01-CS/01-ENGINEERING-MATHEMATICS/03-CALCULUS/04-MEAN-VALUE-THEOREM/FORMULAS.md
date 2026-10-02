# Mean Value Theorem — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| f'(c)=0 | Rolle conclusion | c∈(a,b) | f(a)=f(b); C[a,b]; D(a,b) | EVT + Rolle | Existence of stationary point | Wrong interval type |
| f'(c)=(f(b)−f(a))/(b−a) | Lagrange MVT | c∈(a,b) | C[a,b]; D(a,b) | Rolle on auxiliary g | Secant=tangent | Using f(a)=f(b) unnecessarily |
| f'(c)/g'(c)=(Δf)/(Δg) | Cauchy MVT | c∈(a,b) | g'≠0 on (a,b) | Parametric Rolle | Advanced awareness | g'=0 somewhere |
| \|f(b)−f(a)\|≤M\|b−a\| | Lipschitz bound | \|f'\|≤M | MVT | Lagrange + bound | Estimate | Need f' bounded |
| f'>0 ⇒ increasing | Monotonicity | on interval | f' exists interior | MVT sign | Shape proofs | Point derivative only |
| Between roots of f, f' has root | Rolle on poly | f polynomial | — | Rolle | Root counting | Skipping multiplicities |
