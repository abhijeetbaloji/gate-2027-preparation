# Boolean Algebra — Algebraic Technique

These notes are for learning the topic. After that, use `REVISION.md`. Karnaugh maps and the Quine–McCluskey table are the other two minimization methods in the syllabus; the identities here are what those methods are applying.

The mapped questions that actually ask Boolean algebra (see `PYQ.md`) keep returning to the same jobs: prove two expressions equal, write the minimal sum of products, expand into minterms, count functions or self-dual functions, simplify an XOR nest, and count gates. Parser, grammar, and database rows that sit in the same mapping file are not this topic.

---

## 1. What a Boolean function is

**Intuition.** A Boolean variable is a switch. It is either open or closed, written 0 or 1. A function of \(n\) switches is completely described by what it outputs on each of the \(2^n\) possible settings.

**Definition.** The set \(B = \{0, 1\}\) with operations OR (\(+\), also \(\vee\)), AND (\(\cdot\), often written by juxtaposition), and NOT (\('\), also \(\bar{x}\) or \(\neg x\)) is a Boolean algebra when the axioms below hold. A Boolean function \(F: B^n \to B\) assigns one output bit to every input combination.

**Why the count is \(2^{2^n}\).** There are \(2^n\) rows in the truth table. Each row may be 0 or 1, independently. So there are \(2^{(2^n)}\) different functions of \(n\) variables. For \(n = 3\) that is 256. This is the 2007 question pattern: “maximum number of different Boolean functions of \(n\) variables.”

| \(n\) | Input combinations | Functions |
|------:|-------------------:|----------:|
| 1 | 2 | 4 |
| 2 | 4 | 16 |
| 3 | 8 | 256 |
| 4 | 16 | 65536 |

**Edge.** “Different functions” means different truth tables, not different formulas. \(x + xy\) and \(x\) are the same function.

---

## 2. Why the algebra works

The operations are defined by these tables. Every later identity is a consequence of these tables, not an extra rule.

| \(x\) | \(y\) | \(x+y\) | \(xy\) | \(x'\) |
|------:|------:|--------:|-------:|-------:|
| 0 | 0 | 0 | 0 | 1 |
| 0 | 1 | 1 | 0 | 1 |
| 1 | 0 | 1 | 0 | 0 |
| 1 | 1 | 1 | 1 | 0 |

Reading the table:

- OR is 1 when **at least one** input is 1. That is why \(x + 1 = 1\) and \(x + 0 = x\).
- AND is 1 only when **both** inputs are 1. That is why \(x \cdot 0 = 0\) and \(x \cdot 1 = x\).
- NOT swaps the bit. So \(x + x' = 1\) (one of them is 1) and \(xx' = 0\) (one of them is 0).

**Axioms used in proofs.**

| Name | Form |
|------|------|
| Commutative | \(x+y = y+x\), \(xy = yx\) |
| Associative | \((x+y)+z = x+(y+z)\), same for AND |
| Distributive | \(x(y+z) = xy + xz\), and \(x + yz = (x+y)(x+z)\) |
| Identity | \(x+0 = x\), \(x\cdot 1 = x\) |
| Complement | \(x+x' = 1\), \(xx' = 0\) |

The second distributive law is the one students miss. In ordinary algebra \(x + yz\) does **not** factor as \((x+y)(x+z)\). In Boolean algebra it does, because expanding the right side gives \(x + xz + xy + yz\), and \(x + xz + xy = x\).

**Idempotent, from the axioms.** \(x + x = x(1) + x(1) = x(1+1)\). More directly from the table: OR of a bit with itself is the bit. So \(x+x = x\) and \(xx = x\).

---

## 3. The identities that GATE actually uses

### Absorption

\[
x + xy = x, \qquad x(x+y) = x
\]

**Why.** \(x + xy = x(1 + y) = x\cdot 1 = x\). The second form is the dual (next section).

**Use.** Drop a product that already contains a shorter term. \(PQ + PQR + PQRS = PQ\). That is the 2014 SET-1 pattern: the longer products are absorbed.

### Covering (the form of \(A + A'B\))

\[
x + x'y = x + y
\]

**Why.** \(x + x'y = (x + x')(x + y) = 1\cdot(x+y) = x+y\). From the switch view: if \(x = 1\) the sum is already 1; if \(x = 0\) the sum equals \(y\). So the \(x'\) in the second term never changes the function.

**Trap.** \(x + xy = x\) drops \(y\). \(x + x'y = x+y\) drops the complement on \(y\)'s term, and **keeps** \(y\). Mixing these two is the standard algebraic error.

### Consensus

\[
xy + x'z + yz = xy + x'z
\]

**Why.** \(yz = yz(x+x') = xyz + x'yz\). The first piece is absorbed by \(xy\), the second by \(x'z\). So \(yz\) adds no new 1s.

**When you add it back.** The same identity says \(xy + x'z = xy + x'z + yz\). The extra product does not change the function. It does change the circuit: if \(x\) and \(x'\) are produced by an inverter, they are briefly both 0 (or, in the dual circuit, both 1) while the inverter switches. With \(y = z = 1\), both products \(xy\) and \(x'z\) can be 0 for an instant even though the function is 1. That momentary 0 is a **static-1 hazard**. The consensus term \(yz\) stays 1 through the transition and removes it.

**GATE use.** “Which term is redundant?” Answer: the consensus term. “Does adding \(yz\) change the function?” No. “Does it remove a static-1 hazard?” Yes, in two-level AND-OR.

### De Morgan

\[
(x+y)' = x'y', \qquad (xy)' = x' + y'
\]

**Why.** \((x+y)'\) is 1 only when the OR is 0, which is only when both inputs are 0, which is \(x'y'\). The second law is the dual. It extends to any number of variables: the complement of a sum is the product of complements, and the complement of a product is the sum of complements.

**The broken “identity”.** \((x+y)' = x' + y'\) is false. Counterexample: \(x = 0\), \(y = 1\). Left side is \(1' = 0\). Right side is \(1 + 0 = 1\).

**Complement of a whole expression.** Push NOT to the variables: swap \(+\) with \(\cdot\), and complement each literal. Example: \((AB + A'C)' = (A'+B')(A+C')\).

### XOR and XNOR

\[
x \oplus y = x'y + xy' = (x+y)(xy)' = (x+y)(x'+y')
\]

\[
x \odot y = (x \oplus y)' = xy + x'y' = (x+y')(x'+y)
\]

**Why the factorizations.** \(x'y + xy' = (x+y)(x'+y')\) expands to \(xx' + xy' + yx' + yy' = xy' + x'y\). And \((xy)' = x'+y'\), so \((x+y)(xy)'\) is the same product.

**Properties that questions use.**

| Fact | Why |
|------|-----|
| \(x \oplus 0 = x\) | \(x'0 + x\cdot 1 = x\) |
| \(x \oplus 1 = x'\) | \(x'\cdot 1 + x\cdot 0 = x'\) |
| \(x \oplus x = 0\) | \(x'x + xx' = 0\) |
| \(x \oplus x' = 1\) | always different |
| XOR is associative and commutative | truth table, or the mod-2 sum of bits |
| \(x \oplus y = 0\) iff \(x = y\) | both forms of “equal” |

**Worked pattern (2026 style).** Simplify \(F = (P' + Q) \oplus (P'Q)\).

| \(P\) | \(Q\) | \(P'+Q\) | \(P'Q\) | XOR |
|------:|------:|---------:|--------:|----:|
| 0 | 0 | 1 | 0 | 1 |
| 0 | 1 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 0 | 1 |

So \(F = P \odot Q = PQ + P'Q'\). A four-row table is the reliable check when an XOR nest looks messy. Algebra also works: \(a \oplus (ab) = a(ab)' + a'(ab) = a(a'+b') = ab'\), with \(a = P'+Q\) and \(b = P'Q\), which simplifies to the same XNOR.

**Parity.** \(x \oplus y \oplus z = 1\) when an odd number of inputs are 1. The majority function (“at least two of three inputs are 1”) is **not** parity. Majority of \(a,b,c\) is \(ab + bc + ca\).

---

## 4. Duality and self-dual functions

**Dual.** To dualize an expression, swap \(+\) with \(\cdot\), and swap the constants 0 and 1. Do not complement the variables. The dual of \(x\cdot y + x'\cdot 0\) is \((x+y)(x'+1)\).

**Why duality is valid.** The axioms come in pairs. If an identity was proved from the axioms, the proof with every axiom replaced by its pair is a proof of the dual identity. So you never prove both; you prove one.

**Self-dual function.** \(F\) is self-dual when \(F(x_1',\ldots,x_n') = F(x_1,\ldots,x_n)'\) for every input. Equivalently, the truth table on a vector and on its bitwise complement are opposite.

**Why the count is \(2^{2^{n-1}}\).** The \(2^n\) input vectors form \(2^{n-1}\) pairs \(\{v, v'\}\). On each pair you may choose \(F(v)\) freely; \(F(v')\) is then forced to be the opposite bit. For \(n = 3\) the count is \(2^4 = 16\). For \(n = 2\) it is \(2^2 = 4\).

**Trap.** Self-dual is not the same as “\(F\) equals its dual expression.” The 2014 definition in the mapping says: the dual expression swaps \(+\) and \(\cdot\), and \(F\) is self-dual if that expression equals \(F\). For functions that definition matches the truth-table definition above only when constants are handled carefully. The operational test used in problems is: complement every input, and the output must complement.

**Example.** \(F = xy + yz + zx\) (majority) is self-dual: complementing every variable complements the output. \(F = x+y\) is not: \(F(0,0) = 0\) and \(F(1,1) = 1\), which are not complements of each other.

---

## 5. Minterms, maxterms, SOP, POS

**Minterm.** A product in which every variable appears once, complemented or not. For variables \(A,B,C\) with \(A\) the most significant bit, minterm \(m_5\) is the product that is 1 only on input \(101\), namely \(AB'C\). The index is the integer value of the input row.

**Maxterm.** A sum in which every variable appears once. Maxterm \(M_5 = A' + B + C'\) is 0 only on row 101. In general \(M_i = m_i'\).

**Canonical SOP.** \(F = \sum m(i_1, i_2, \ldots)\) means the OR of those minterms. This is the list of rows where \(F = 1\).

**Canonical POS.** \(F = \prod M(j_1, j_2, \ldots)\) means the AND of those maxterms, the rows where \(F = 0\).

**Why both describe the same function.** A function is fixed by its onset (rows of 1) or by its offset (rows of 0). The two lists partition \(\{0, 1, \ldots, 2^n - 1\}\).

**Expansion example.** \(f(P,Q,R) = PQ + QR + PR\).

- \(PQ = PQ(R+R') = PQR + PQR' = m_7 + m_6\)
- \(QR = (P+P')QR = m_7 + m_3\)
- \(PR = PR(Q+Q') = m_7 + m_5\)

Union: \(m_3, m_5, m_6, m_7\). So \(f = \sum m(3,5,6,7)\). This is the “minterm expansion” pattern.

**Literal.** One occurrence of a variable or its complement. \(AB'C\) has three literals. Gate-count and “minimal form” questions sometimes minimize terms, sometimes literal occurrences. Read which one is asked. A lone literal in a sum is one term and one literal; it needs no AND gate.

**Minimal SOP.** A sum of products that realizes \(F\), and no other SOP has fewer products; among those, none has fewer literals. There can be more than one.

**Minimal POS.** The same idea for a product of sums. Getting it by algebra: simplify \(F'\), then complement back with De Morgan. Grouping 0s on a K-map (next topic) is the same transformation.

**Worked minimal SOP.**

\[
F = A'B + BC' + AC + AB'C'
\]

Check by cases, or expand and absorb.

- \(AC + A'B\) does not collapse by itself.
- \(AB'C' + A'B\) is not an absorption pair.
- Expand nothing yet. Factor \(C\): \(F = A'B + C(B' + A) + AB'C'\).

Use the table for three variables (8 rows) when the expression is short. Compute \(F\):

| \(ABC\) | \(A'B\) | \(BC'\) | \(AC\) | \(AB'C'\) | \(F\) |
|---------|--------:|--------:|-------:|----------:|------:|
| 000 | 0 | 0 | 0 | 0 | 0 |
| 001 | 0 | 0 | 0 | 0 | 0 |
| 010 | 1 | 1 | 0 | 0 | 1 |
| 011 | 1 | 0 | 0 | 0 | 1 |
| 100 | 0 | 0 | 0 | 1 | 1 |
| 101 | 0 | 0 | 1 | 0 | 1 |
| 110 | 0 | 1 | 0 | 0 | 1 |
| 111 | 0 | 0 | 1 | 0 | 1 |

Onset: all rows except 000 and 001, i.e. \(F = A + B\). Check: \(A+B\) is 0 only on 000 and 001. So the minimal SOP is \(A + B\), with two literals.

**How the algebra reaches it.** \(AB'C' + BC' = C'(AB' + B)\). And \(B + AB' = (B+A)(B+B') = A+B\), so that piece is \(C'(A+B)\). Then \(C'(A+B) + AC = A + BC'\). With the remaining \(A'B\), \(F = A + BC' + A'B\). Covering gives \(A + A'B = A+B\), and \(BC'\) is absorbed by the \(B\) inside \(A+B\). Result \(A+B\).

---

## 6. Shannon expansion (cofactors)

\[
F = x F(1) + x' F(0) = (x + F(0))(x' + F(1))
\]

\(F(1)\) means “set \(x = 1\) in \(F\)”; \(F(0)\) means set \(x = 0\). These are the cofactors.

**Why.** On the half of the table where \(x = 1\), \(F\) equals \(F(1)\). On the other half it equals \(F(0)\). The first formula ORs those two halves. The second is the dual (POS) form.

**Example.** \(F = AB + A'C\). Cofactor on \(A\): \(F(1) = B\), \(F(0) = C\). Then \(F = A B + A' C\), which we already had, and also \(F = (A+C)(A'+B)\). Expand the POS to check: \(AA' + AB + CA' + CB = AB + A'C + BC\), and \(BC\) is the consensus term, so this equals \(AB + A'C\).

**Complement.** \((AB + A'C)' = (A'+B')(A+C')\). Expanding that product gives \(A'C' + AB' + B'C'\), not the guess \(A'B' + AC'\). The guess fails on \(A=1, B=0, C=1\): \(F = 0\) so \(F' = 1\), but \(A'B' + AC' = 0\). Complement by De Morgan. Do not swap operators and also drop literals.

---

## 7. Don’t cares, prime implicants, essential prime implicants

An implicant is a product that is 1 only where \(F\) is 1 or don’t-care. It is **prime** when deleting any literal destroys that property. It is **essential** when some required onset minterm is covered by no other prime implicant.

Algebra can produce a minimal expression, but “number of essential prime implicants” is decided by the covering, which is the K-map or the tabular method. The 2018 mapped question is exactly that count, with a don’t-care list. Don’t-care rows may be used inside an implicant. They do not have to be covered. A minterm of the onset does.

**Counting minterms after a complement (2015 pattern).** Minimize the expression inside, or expand it, then complement the onset. If the minimized function has \(k\) onset rows out of \(2^n\), the complement has \(2^n - k\) minterms. “Number of minterms after minimizing” in that question means the number of minterms in the canonical SOP of the complemented function, not the number of products in a minimal form. Read the stem: it asks for a count of minterms of a complemented expression.

---

## 8. Gate realizations that use only the algebra

**Two-input NOR only.** A NOR is \((x+y)'\). It is functionally complete:

- NOT: \((x+x)' = x'\) (one NOR).
- OR: NOR followed by NOT, so two NORs.
- AND: \(xy = (x'+y')'\), so invert each input and NOR them.

**Example.** \((AB + C)\) with only 2-input NOR gates, complements not supplied.

One standard count: \(AB = (A'+B')'\) needs two inverters and one NOR (3), then OR with \(C\) needs a NOR and an inverter (2), total 5. Sharing and alternative factorizations should be checked before locking a minimum; the mapped 2009 question asks this minimum for \((AB+C)\). Draw the NOR network and count gates, and do not count a literal’s complement as free unless the stem says complements are available.

**When complements are free.** The 2019 NOR-count question says all inputs and their complements are available. Then you do not spend gates on inverters. Minimize first, then convert each AND-OR (or OR-AND) stage into NOR form.

---

## 9. How to solve the usual GATE shapes

1. **“Which expression equals \(F\)?”** Build the 4-row or 8-row table if \(n \le 3\). For \(n = 4\), simplify both sides with absorption, consensus, and De Morgan, or compare cofactors. An MSQ can have several correct options; check every option against one counterexample row.
2. **“Minimal SOP of a minterm list.”** This is easier on a K-map. Algebra is for short expressions that are already written with \(+\) and \(\cdot\). If both a K-map and an algebraic form are offered, they must agree.
3. **“Not a property / not a tautology.”** Test the suspicious identity on all four pairs \((0,0), (0,1), (1,0), (1,1)\), or on one counterexample. One failing row kills an identity.
4. **“Number of functions / self-dual functions.”** Use \(2^{2^n}\) and \(2^{2^{n-1}}\). Do not list them.
5. **Circuit of AND, OR, XOR of known minterm lists.** A minterm is in the output according to the gate. For XOR of two functions, the output onset is the symmetric difference of the onsets. For AND, it is the intersection.
6. **Static hazard.** Same function after adding consensus; the implementation is not the same during a single-input change.

---

## 10. Traps

| Trap | What is true |
|------|----------------|
| \((x+y)' = x'+y'\) | False. Right side is \((xy)'\). |
| \(x + x'y = x\) | False. It equals \(x+y\). |
| Dual complements the variables | False. Dual swaps \(+\) and \(\cdot\), and 0 and 1. |
| \(xx' = 1\) | False. It is 0. The sum \(x+x'\) is 1. |
| XOR is \(xy + x'y'\) | That is XNOR. XOR is \(x'y + xy'\). |
| Minimal SOP is unique | Often it is not. “The” minimal form may be any of the minimum ones. |
| Don’t-care must be covered | Only onset minterms must be covered. |
| Literal count equals term count | \(A + BC\) has 2 terms and 3 literals. |
| A hazard means the functions differ | The steady-state functions can be identical. |

---

## 11. Connections

- **K-map and tabular method.** They find the same prime implicants the algebra would find, without requiring you to guess which identity to apply. Use algebra to check a grouped expression.
- **Combinational circuits.** A mux, decoder, or adder output is a Boolean function. Shannon expansion is exactly the 2-to-1 mux formula \(Y = S' I_0 + S I_1\).
- **Sequential circuits.** Next-state equations are Boolean functions of the present state and the input. The algebra here is how those equations are simplified before they are wired to flip-flop inputs.
- **Number systems.** XOR is the sum bit of a half adder; AND is the carry. That is why adder questions feel like Boolean questions.
