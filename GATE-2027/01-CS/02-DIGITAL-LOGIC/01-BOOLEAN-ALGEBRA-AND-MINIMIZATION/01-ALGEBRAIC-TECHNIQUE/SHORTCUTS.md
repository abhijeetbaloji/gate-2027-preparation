# Boolean Algebra (Algebraic Technique) — Shortcuts

Each shortcut is an identity from `NOTES.md` used as a check. None of them is a guess.

## 1. One-row counterexample

- **Solves.** “Is this equation always true?”
- **When.** The claimed identity has only a few variables, or you suspect De Morgan was reversed.
- **Why.** Two functions are equal only when every row matches. One mismatch is enough to reject.
- **Example.** \((x+y)' = x'+y'\) fails at \(x=0, y=1\): left is 0, right is 1.
- **Limit.** A row that matches does not prove the identity. You still need every row, or a real proof.

## 2. Absorption in one glance

- **Solves.** Minimal SOP of a sum in which every product contains the same shorter product.
- **When.** The expression is \(PQ + PQR + PQRS + \cdots\).
- **Why.** \(x + xy = x\). Extra literals AND-ed onto an existing term cannot add a 1 that the short term missed, and they are 0 wherever you might have hoped they help.
- **Example.** \(PQ + PQR + PQRS = PQ\).
- **Limit.** The short term must actually appear. \(PQR + PQRS\) does not equal \(PQ\).

## 3. Covering, not absorption

- **Solves.** \(x + x'y\).
- **When.** One term is a single literal and another term contains that literal’s complement.
- **Why.** If \(x=1\), the sum is 1. If \(x=0\), the second term equals \(y\). So the function is \(x+y\).
- **Example.** \(A + A'B = A+B\).
- **Limit.** \(x + xy\) is absorption and drops \(y\). Using covering there is wrong.

## 4. Consensus is redundant, and is the hazard fix

- **Solves.** Whether \(yz\) can be deleted from \(xy + x'z + yz\), and whether a two-level AND-OR of \(xy + x'z\) glitches.
- **When.** Two products contain \(x\) and \(x'\), and the third product is exactly the remaining literals.
- **Why.** \(yz = xyz + x'yz\), and each piece is absorbed. Adding \(yz\) back does not change any stable output, but it stays 1 while \(x\) switches if \(y=z=1\).
- **Example.** \(XY + X'Z + YZ\) equals \(XY + X'Z\). The implementation of the shorter sum has a static-1 hazard.
- **Limit.** All three products must be present in that pattern. \(xy + z\) is not a consensus pair. The shortcut says nothing about static-0 hazards in OR-AND logic; the dual statement is the one to use there.

## 5. XOR cancellation

- **Solves.** A chain of XORs with repeated variables or constants.
- **When.** The expression is only XOR, OR-nested inside XOR, and you may use \(a \oplus a = 0\), \(a \oplus 0 = a\), \(a \oplus 1 = a'\).
- **Why.** XOR is associative, commutative, and every bit is its own inverse.
- **Example.** \((P \oplus Q) \oplus (P \oplus Q) = 0\). And \((1 \oplus P) = P'\).
- **Limit.** XOR does not distribute over AND in the way OR does. Do not “cancel” \(P\) inside \(P \oplus (PQ)\) as if it were a sum. Compute \(a \oplus (ab) = ab'\) instead (set \(a\) as the first factor).

## 6. Onset size from a simple expression

- **Solves.** “How many minterms?” when the simplified function is an OR or AND of a few literals.
- **When.** You have already simplified, and the remaining expression is a single product, a single sum, or a disjoint union.
- **Why.** A product of \(k\) literals on \(n\) variables is 1 on \(2^{n-k}\) rows. A sum \(x+y\) on \(n\) variables is 0 only when both are 0, so the onset has \(2^n - 2^{n-2}\) rows if \(x\) and \(y\) are distinct variables.
- **Example.** \(F = A+B\) on three variables is 0 only on rows 000 and 001, so it has 6 minterms.
- **Limit.** Overlapping products cannot be added by summing the separate counts. \(AB + AC\) is not \(2+2\) minterms on three variables; row 111 is counted twice. Use inclusion or a table.

## 7. Cofactor instead of a 16-row table

- **Solves.** Equality of two 4-variable expressions that both mention one variable cleanly.
- **When.** You can set one variable to 0 and to 1 and compare the smaller functions.
- **Why.** Shannon: \(F = G\) if and only if the two cofactors match.
- **Example.** To test \(AB + A'C = (A+C)(A'+B)\), set \(A=1\): both sides become \(B\). Set \(A=0\): both sides become \(C\).
- **Limit.** The cofactors themselves must actually be equal. A matching cofactor on \(A=1\) alone is not enough.
