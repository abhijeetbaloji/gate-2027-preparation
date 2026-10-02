# Limits — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| lim sin x/x = 1 | Standard trig limit | x→0 | — | Squeeze / geometry | sin(ax)/x → a | Using at x→∞ |
| lim (eˣ−1)/x = 1 | Exponential limit | x→0 | — | Substitute t=eˣ−1 | e^{kx} forms | Wrong base |
| lim (1+x)^{1/x} = e | Definition of e | x→0 | — | Compound interest limit | (1+kx)^{1/x} | Missing power k |
| lim (1−cos x)/x² = 1/2 | Cosine limit | x→0 | — | L'Hôpital or series | Trig 0/0 | Using sin limit |
| Rational x→∞ | Leading coeff ratio | deg equal | — | Divide by x^n | Polynomial limits | L'Hôpital when unnecessary |
| L'Hôpital | lim f/g = lim f'/g' | 0/0 or ∞/∞ | f',g' exist | MVT sketch | Indeterminate forms | Quotient rule on f/g |
| Squeeze | g≤f≤h, same limit ⇒ f→L | — | Near a | Sandwich theorem | sin(1/x) type | Bounds don't match |
| One-sided | lim exists iff L=R | — | — | Definition | \|x\|, piecewise | Ignoring mismatch |
