# Boolean Algebra (Algebraic Technique) — Mistakes

These are recurring errors on this syllabus line. The mapping file’s answer field is `VERIFICATION REQUIRED`, so nothing below is a claimed official key. The empty table is for your own misses.

### Common mistakes

| Mistake | What goes wrong | Correct rule |
|---------|-----------------|--------------|
| Reversed De Morgan | \((x+y)'\) written as \(x'+y'\) | Complement of OR is AND of complements |
| Absorption vs covering | \(x + x'y\) simplified to \(x\) | \(x + x'y = x + y\) |
| Dual complements variables | Dual of \(xy\) written as \(x'+y'\) | Dual swaps \(+\) and \(\cdot\), and 0 and 1 |
| XOR / XNOR swap | \(xy + x'y'\) called XOR | That is XNOR. XOR is \(x'y + xy'\) |
| Function count | \(2^n\) or \(2n\) functions | \(2^{2^n}\) functions |
| Self-dual count | Half of all functions, or \(2^{n-1}\) | \(2^{2^{n-1}}\) |
| Literal vs term | “Minimal” answered with the wrong count | Read whether the stem wants products, literals, or gates |
| Don’t-care must be 1 | A don’t-care is forced into the onset | It may be used and need not be covered |
| Consensus changes the function | Deleting \(yz\) from \(xy+x'z+yz\) treated as a new function | The functions are equal. The hazard behaviour is not |
| Minterms of a complement | Number of products in a minimal SOP used as the minterm count | Canonical minterm count is the size of the onset |
| Majority vs parity | “At least two 1s” written as \(a \oplus b \oplus c\) | Majority is \(ab+bc+ca\) |
| Overlapping minterm counts | \(|AB| + |AC|\) added directly | Shared rows are counted twice |

### PYQ-shaped traps

- A long SOP such as \(PQ + PQR + PQRS\) is already \(PQ\). Further “minimization” that leaves three products has not used absorption.
- An XOR nest with a constant 1 complements the variable it touches. Associativity lets repeated variables cancel only after that complement is written.
- “Number of minterms after minimizing \([expression]'\)” asks for the onset size of the complement, not the number of terms in a short formula.
- A gate-count stem that says complements are available must not be solved by inserting inverters. A stem that does not say that must.
- Equivalence MSQs often have more than one right expression. One matching row is not a proof; one mismatch is a disproof.

### Calculation slips

- Minterm index with the wrong bit as MSB. The stem’s variable order is the binary weight order.
- Expanding \(x + yz\) as \(xy + xz\). That is the other distributive law. The factorisation is \((x+y)(x+z)\).
- Complementing \(AB + A'C\) by complementing each product and leaving the OR. The complement is a product of the complemented sums.

### My Mistakes

Record your own errors after practice and past papers. Do not pre-fill this table.

| Date | Source | Question | Mistake | Root Cause | Correct Rule | Prevention |
|------|--------|----------|---------|------------|--------------|------------|
| | | | | | | |
