# Karnaugh Map — Formulas

Reasons are in `NOTES.md`.

| Rule | Meaning | Condition |
|------|---------|-----------|
| \(2^n\) cells | One cell per minterm | \(n\) variables |
| \(n\) neighbours | Hamming distance 1, wrap included | The cell itself is not a neighbour |
| Group size \(2^k\) | The onset of one product term | \(k = 0,1,\ldots,n\). Sizes 3, 5, 6, 7, 12 are illegal |
| Literals in that product | \(n - k\) | Every doubling drops one variable |
| SOP literal | Kept variable is complemented iff it is 0 throughout the 1-group | Variable that changes is omitted |
| POS literal | Kept variable is complemented iff it is 1 throughout the 0-group | Groups are groups of 0s |
| Don’t-care | May enter a group; need not be covered | A required 0 must not enter a 1-group |
| Essential prime | The unique prime containing some onset minterm | Don’t-care-only groups are never essential |
| Cells in a subcube | Two cells combine iff their labels differ in one bit and their dashes already match | Same test the tabular method uses |

**Example.** The eight minterms \(\sum m(0,1,2,3,8,9,10,11)\) are one group of \(2^3\). On four variables the product has \(4-3 = 1\) literal: \(B'\), when \(B\) is the second variable.

**Example.** A pair of 0s at \(m_4=100\) and \(m_6=110\) is the sum \(A' + C\). \(A\) is constantly 1, so it appears complemented; \(C\) is constantly 0, so it appears uncomplemented; \(B\) changes and is deleted.
