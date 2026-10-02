# Combinatorics: Counting — Formulas

Reference only. Learn concepts in `NOTES.md` first.


| Formula | Meaning | Variables | Conditions | Derivation | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------|------------------|----------------|
| C(n,r)=n!/(r!(n−r)!) | Binomial | 0≤r≤n | Integer | Divide P(n,r) by r! | Selections | Order ignored wrongly |
| P(n,r)=n!/(n−r)! | Permutation | r≤n | — | Product rule | Arrangements | Use C when order matters |
| C(n+r−1,r) | Multisets | n types, r picks | — | Stars and bars | Distributions | Wrong formula |
| |A∪B∪C| | IEP 3 sets | Finite | — | Inclusion-exclusion | Union size | Sign errors |
| ⌈N/k⌉ | Pigeonhole bound | N items, k boxes | — | Pigeonhole | Existence | Wrong k |
