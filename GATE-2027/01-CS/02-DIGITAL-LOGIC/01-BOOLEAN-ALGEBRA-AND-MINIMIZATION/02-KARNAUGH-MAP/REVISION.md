# Karnaugh Map — Revision

## Layout

- \(n\) variables, \(2^n\) cells, \(n\) neighbours each.
- Labels run \(00, 01, 11, 10\). Ends wrap. Corners touch.
- 4-variable cell numbers, rows \(AB\), columns \(CD\):

| \(AB \backslash CD\) | 00 | 01 | 11 | 10 |
|----------------------|---:|---:|---:|---:|
| 00 | 0 | 1 | 3 | 2 |
| 01 | 4 | 5 | 7 | 6 |
| 11 | 12 | 13 | 15 | 14 |
| 10 | 8 | 9 | 11 | 10 |

## Groups

- Size \(1, 2, 4, 8, 16\) only.
- A group of \(2^k\) cells deletes \(k\) variables.
- Constant 0 in the group → complemented literal in SOP.
- Constant 1 in the group → uncomplemented literal in SOP.
- A variable that changes is deleted.

## Cover

- Cover every 1. Do not cover a required 0. X may be used and need not be covered.
- Prime: cannot be enlarged.
- Essential: some 1 lies in no other prime.
- Minimal: fewest primes, then fewest literals. Not always unique.

## POS

Group the 0s. Constant 1 in that group → complemented literal in the **sum**. AND the sums.

## Fast checks

- Eight cells in two full rows that share one constant bit are one literal.
- One mismatched cell rejects an expression.
- Extra consensus circle: same function, fewer static-1 hazards, not fewer products.

## Traps

Group of 6. Binary label order. Forcing every X to 1. Calling every prime essential. Reading a 0-group with the SOP complement rule.
