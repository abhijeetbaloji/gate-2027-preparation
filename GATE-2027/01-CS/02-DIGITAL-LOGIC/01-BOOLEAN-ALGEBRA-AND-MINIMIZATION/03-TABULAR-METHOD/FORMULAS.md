# Tabular Method — Formulas

Reasons are in `NOTES.md`.

| Rule | Statement | Condition |
|------|-----------|-----------|
| Combine | \(Px + Px' = P\) | The two strings differ in exactly one bit; existing dashes occupy the same positions |
| Prime | A string that never combines further | Includes an isolated minterm |
| Don’t-care generation | Don’t-cares are listed and combined | They are not chart columns |
| Essential | A prime that alone covers some onset minterm | Look for a column with one mark |
| Literals in a prime | Number of non-dash bits | \(n\) variables, \(k\) dashes → \(n-k\) literals |
| Cover size | Not equal to the prime count | Unused primes are still primes |

**Example.** \(0101\) and \(1101\) differ only in the first bit. The prime string is \(-101\). On \(ABCD\) that product is \(BC'D\), with 3 literals.

**Example.** A column with marks in two rows means neither row is essential on account of that column. Essential status can still come from a different column.
