# Tabular Method — Revision

## Steps

1. List onset and don’t-cares in binary, bucketed by the number of 1s.
2. Combine across adjacent buckets if the strings differ in one bit and dashes already agree. Tick both parents.
3. Repeat until nothing combines.
4. Unticked strings are the prime implicants.
5. Chart: columns are onset minterms only. A single mark in a column makes that prime essential.
6. Cover the rest with as few primes as possible.

## Reading a string

On \(ABCD\), dash deletes the variable, 1 keeps it, 0 keeps the complement. \(010\text{-} = A'BC'\). \(-101 = BC'D\).

## Counts, kept distinct

| Asked | Count |
|-------|-------|
| Prime implicants | Unticked strings |
| Essential primes | Single-mark columns |
| Products in a minimal SOP | Essentials plus a smallest set for the leftover columns |
| Literals | Non-dash bits in the chosen strings |

## Don’t-cares

Used while combining. No column in the chart. Need not be covered.

## Traps

Distance-2 combine. Ticked minterm deleted from the chart. Don’t-care column. Every prime called essential. A prime that sits in every minimal SOP called essential when it has no private minterm.
