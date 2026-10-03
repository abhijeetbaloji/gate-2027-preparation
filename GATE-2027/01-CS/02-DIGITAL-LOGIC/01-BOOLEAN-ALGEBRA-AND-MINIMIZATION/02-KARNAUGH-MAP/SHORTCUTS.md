# Karnaugh Map — Shortcuts

## 1. Full rows with one fixed bit

- **Solves.** A minterm list that fills every cell in which one variable has one value.
- **When.** The list has \(2^{n-1}\) minterms and you can see the fixed bit.
- **Why.** That set is one subcube of dimension \(n-1\), so the SOP is a single literal.
- **Example.** \(\sum m(0,1,2,3,8,9,10,11)\) on \(ABCD\) is every row with \(B=0\), so \(F = B'\).
- **Limit.** If any cell with \(B=0\) is missing, or any cell with \(B=1\) is present, it is not \(B'\).

## 2. Power-of-two test before circling

- **Solves.** Rejecting an illegal loop.
- **When.** A circle has 3, 5, 6, 7, 9, 10, or 12 cells.
- **Why.** No product term has an onset of that size.
- **Example.** Six 1s in a \(2 \times 3\) block is two legal groups, not one.
- **Limit.** Two legal groups may still be drawn over those six cells. The shortcut forbids one circle, not the function.

## 3. One-cell rejection of an expression

- **Solves.** MSQ options against a drawn map.
- **When.** You can evaluate the option on a single 0-cell or 1-cell.
- **Why.** Equality of functions fails at the first mismatch.
- **Example.** If cell \(m_0\) is 0, any option whose empty-product or whose \(A'B'C'D'\) term is present is false, unless a don’t-care has been declared there.
- **Limit.** A cell that matches does not accept the option. Check a 1 that must be covered and a 0 that must stay 0.

## 4. 0-group written by flipping the SOP habit

- **Solves.** Minimal POS without rewriting the whole table.
- **When.** The 0s form obvious pairs or quads.
- **Why.** The sum must be 0 on that subcube. A variable fixed at 1 is complemented in the sum; a variable fixed at 0 is not.
- **Example.** 0s at 100 and 110 give \(A' + C\).
- **Limit.** Using the SOP rule (complement when the bit is 0) on a 0-group writes the complement of the correct sum.

## 5. Distinguished 1 means essential

- **Solves.** “How many essential prime implicants?”
- **When.** You have circled primes and some 1 sits in only one circle.
- **Why.** That circle is the only product that can cover the minterm, so every minimal cover includes it.
- **Example.** A lone 1 with no adjacent 1 is an essential minterm.
- **Limit.** A 1 that sits in two circles does not make either circle essential. Don’t-care cells never create an essential prime by themselves.
