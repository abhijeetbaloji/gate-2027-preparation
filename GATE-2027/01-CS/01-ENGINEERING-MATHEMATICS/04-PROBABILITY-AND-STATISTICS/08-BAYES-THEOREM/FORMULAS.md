# Bayes' Theorem — Formulas

Reference only. Learn concepts in `NOTES.md` first.

| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| P(A\|B)=P(B\|A)P(A)/P(B) | Bayes' theorem | P(B)>0 | — | From P(A∩B) | Invert conditioning | Swap A,B |
| P(B)=ΣP(B\|Aᵢ)P(Aᵢ) | Denominator | Partition Aᵢ | Exhaustive, disjoint | Total probability | Medical/factory | Missing branch |
| Two-hypothesis | P(H\|D)=P(D\|H)P(H)/[P(D\|H)P(H)+P(D\|¬H)P(¬H)] | — | — | Bayes + total | Test accuracy | Sensitivity as answer |
| Posterior odds | prior odds × likelihood ratio | — | — | Odds form | Quick check | Rare disease neglect |
| P(A∩B)=P(B\|A)P(A) | Joint from likelihood | — | — | Multiplication rule | Tree paths | Wrong order |
