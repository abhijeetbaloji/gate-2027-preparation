# Karnaugh Map

These notes teach minimization from the map. Algebraic identities are in the previous folder; the Quine–McCluskey table is the next one. A K-map is those identities drawn so that adjacent cells differ by one variable.

Mapped stems that really are K-maps (see `PYQ.md`) ask for a minimal SOP or POS, often with don’t-care cells marked X, or ask which of several expressions match a drawn map. The 2011 cache question stored in the same file is not a K-map question.

---

## 1. Why the map is shaped the way it is

**Intuition.** Two input rows that differ in one bit can be merged by the identity \(x y + x y' = x\). A map places those rows next to each other, including the wrap from the ends, so a legal merge is a rectangle you can see.

**Gray-code labels.** Rows and columns are numbered \(00, 01, 11, 10\), not \(00, 01, 10, 11\). Consecutive labels, and the first with the last, differ by one bit. That is the whole reason the code is Gray. Ordinary binary order would put a two-bit jump between \(01\) and \(10\), and a rectangle there would not be a legal implicant.

**Cell count.** An \(n\)-variable map has \(2^n\) cells, one per minterm.

| Variables | Cells | Usual picture |
|----------:|------:|---------------|
| 2 | 4 | \(2 \times 2\) |
| 3 | 8 | \(2 \times 4\) |
| 4 | 16 | \(4 \times 4\) |
| 5 | 32 | two 4-variable maps |

GATE minimization is almost always 3 or 4 variables. Five-variable maps appear rarely; the tabular method is the safer tool once the onset is a long list.

**Adjacency.** In an \(n\)-variable map every cell has \(n\) neighbours. A cell is not a neighbour of itself. Neighbours are exactly the minterms at Hamming distance 1.

For \(m_0 = 0000\) on variables \(ABCD\), the neighbours are \(m_1\) (0001), \(m_2\) (0010), \(m_4\) (0100), and \(m_8\) (1000). The cell \(m_5 = 0101\) differs in two bits, so it is not adjacent, even if a badly ordered map draws it nearby.

**Standard 4-variable layout.** \(A,B\) label rows, \(C,D\) label columns, \(A\) and \(C\) are the higher bits of their pairs.

| \(AB \backslash CD\) | 00 | 01 | 11 | 10 |
|----------------------|---:|---:|---:|---:|
| 00 | 0 | 1 | 3 | 2 |
| 01 | 4 | 5 | 7 | 6 |
| 11 | 12 | 13 | 15 | 14 |
| 10 | 8 | 9 | 11 | 10 |

The corners \(m_0, m_2, m_8, m_{10}\) are one group of four: they are the cells with \(B=0, D=0\). The wrap is real.

---

## 2. What a legal group is

A group represents one product term. It must be a rectangle of \(2^k\) cells (1, 2, 4, 8, or 16 on a 4-variable map), using the Gray topology, wraps included. A group of 3, 5, 6, 7, 9, … is not a product term.

**Why the size is a power of two.** A product that fixes \(n-k\) variables and leaves \(k\) variables free is 1 on exactly \(2^k\) rows. Those rows form a subcube. There is no product whose onset has 3 or 6 rows.

**Which literal survives.** Inside the group, a variable that is 0 in every cell stays as a complemented literal. A variable that is 1 in every cell stays uncomplemented. A variable that takes both values is deleted. Each doubling of the group deletes one literal. A group of \(2^k\) cells on \(n\) variables is a product of \(n-k\) literals.

**Largest groups.** A single 1 that cannot join any other 1 is a minterm, \(n\) literals. An octet on a 4-variable map is one literal. A full map of 1s is the constant 1.

**Worked SOP.** \(F(A,B,C,D) = \sum m(0,1,2,3,8,9,10,11)\).

Those are all cells with \(B = 0\): the entire top row \(AB=00\) and the entire bottom row \(AB=10\). They form one group of 8. \(B\) is constantly 0, and \(A,C,D\) all vary. So \(F = B'\). One product, one literal.

Check the complement: every cell with \(B=1\) is absent from the list. This is the shape of the 2026 CS-2 minterm list \(\sum m(0,1,2,3,8,9,10,11)\), which is filed under algebraic technique because the stem does not draw a map. The map is still the fastest way to see \(B'\).

---

## 3. Minimal covers

**Implicant.** Any legal group of 1s (and allowed don’t-cares). The product is never 1 on a cell where \(F\) is required to be 0.

**Prime implicant.** A group that is not contained in a larger legal group. You stop enlarging when every direction is blocked by a required 0 or by the edge in a way that breaks the rectangle.

**Essential prime implicant.** A prime that is the only one covering some required 1. That 1 is a distinguished minterm. Every minimal sum uses every essential prime.

**Minimal SOP.** A cover of all required 1s by prime implicants, with as few products as possible, and among those as few literals as possible. Don’t-care cells need not be covered. They may be included when they make a larger or fewer groups.

**Procedure.**

1. Write 1, 0, and X. Empty cells in a minterm list are 0s, not don’t-cares.
2. Circle the largest groups that cover a 1 no other largest group can cover. Those are the candidates for essential primes.
3. Cover the remaining 1s. If two primes both cover a leftover 1 and nowhere else that is still uncovered, either prime may be chosen. The function then has more than one minimal SOP.
4. Write the product for each chosen group and OR them.

**Worked example with a choice.** \(F(A,B,C) = \sum m(0,1,2,5)\).

| \(AB \backslash C\) | 0 | 1 |
|---------------------|--:|--:|
| 00 | 1 | 1 |
| 01 | 0 | 1 |
| 11 | 0 | 0 |
| 10 | 1 | 0 |

Pairs: \(m_0 m_1 = A'B'\), \(m_0 m_2 = A'C'\), \(m_1 m_5 = B'C\). No quad. One minimal cover is \(A'C' + B'C\). It uses two products and four literals. \(A'B'\) is prime but not needed in that cover: \(m_0\) is already in \(A'C'\) and \(m_1\) is already in \(B'C\).

So “a prime implicant” and “a term in the minimal SOP” are different. The second is what the question usually wants.

---

## 4. Don’t-cares

An X may sit inside a group. It must not be treated as a 1 that has to be covered, and it must not be treated as a 0 that blocks a group you want, unless you have decided to set it to 0.

**Illegal.** Grouping a required 0 with anything. Also grouping two X cells that touch no required 1, if your only goal is a cover of the onset: that group does not belong in the SOP. It is an implicant of a different function.

**Worked example.** \(F(A,B,C) = \sum m(0,2,6) + d(1,7)\).

\(m_4 = 100\) is a required 0. The octet “all of \(C'\)” includes \(m_4\), so \(F\) is not \(C'\). The product \(A'\) includes \(m_3 = 011\), also a required 0, so \(A'\) is illegal.

Legal minimal SOP: \(A'B'\) (cells \(m_0\) and don’t-care \(m_1\)) together with \(BC'\) (cells \(m_2\) and \(m_6\)). Both onset cells \(m_0, m_2, m_6\) are covered, and no required 0 is inside a group.

If every don’t-care is forced to 0, the onset is only \(\{0,2,6\}\) and the groups get smaller. Forcing X to 0 is a different function. Do it only when the stem says the don’t-cares are absent.

---

## 5. Product of sums from the same map

Group the **0s**, with the same rectangle rules. Don’t-cares may join a 0-group and need not.

**Writing the sum.** For a group of 0s, keep a variable that is constant. Complement it if that constant is **1**. Delete a variable that changes. OR those literals. AND the sums from each group.

**Why the complement is flipped relative to SOP.** A sum \(A + C'\) is 0 only when \(A=0\) and \(C'=0\), i.e. only on \(A=0, C=1\). Matching a block of 0s means writing the sum that is 0 exactly on that block. The SOP rule was “literal 0 means complemented variable in a product.” The POS rule is “literal 1 in a block of 0s means complemented variable in a sum.”

**Same example.** Zeros of \(\sum m(0,1,2,5)\) are \(m_3, m_4, m_6, m_7\).

- \(m_4, m_6 = 100, 110\): \(A=1\), \(C=0\), \(B\) changes. Sum: \(A' + C\).
- \(m_3, m_7 = 011, 111\): \(B=1\), \(C=1\), \(A\) changes. Sum: \(B' + C'\).

\(F = (A' + C)(B' + C')\). Two sums, four literals. Expanding and deleting the consensus term returns \(A'C' + B'C\), the SOP from section 3. Same function.

**Trap from the 2017 stem.** A minimum POS is not “the SOP with bars drawn over it,” and it is not the SOP of \(F\) factored in a random way. Group the 0s, or minimize \(F'\) and apply De Morgan.

---

## 6. Essential primes, and maps with several minima

A column of the covering (one required 1) that sits in only one prime circle makes that circle essential.

**Pattern that produces a count.** If every 1 you care about can be circled in two ways, the number of essential primes is 0, and the number of minimal SOPs is greater than 1. The 2012 and 2008 stems are this kind of picture: a drawn map, X for don’t-care, “minimal form.” Several options differ by a redundant product. Delete any product that is the consensus of two others, and delete any product that covers only X cells.

**Static-1 hazard on the map.** Prime circles \(xy\) and \(x'z\) that both contain the cell where \(y=z=1\), but that cell is not inside a circle of its own, leave a hazard when \(x\) switches. Drawing the consensus circle \(yz\) does not change which cells are 1. It removes the hazard. A question that asks only for the minimal SOP does not want that extra circle. A question that asks for a hazard-free sum does.

---

## 7. Reading a map against an expression

The 2025 CS-2 stem shows a map and several Boolean expressions, more than one of which may match. The check:

1. Every 1-cell of the map must make the expression 1.
2. Every 0-cell must make the expression 0.
3. An X cell may go either way, **if** the stem’s map uses X. If the map is fully specified, there is no freedom.
4. A sum of the prime circles is enough. A sum that also lists some uncombined minterms can still be equal to \(F\). “Equal to \(F\)” is weaker than “minimal.”

One cell is enough to reject an option. Matching the circles is enough to accept a minimal option.

---

## 8. Solving procedure for the usual paper

1. Fix the variable order printed on the map. Do not assume \(AB\) on rows if the figure says otherwise.
2. Copy 1, 0, X into the Gray layout above if the printed order is scrambled by a bad figure. The minterm numbers in the table of section 1 are the check.
3. If the stem gives a minterm list and says “Karnaugh map,” draw the map. Do not expand 16 minterms by algebra first.
4. Circle power-of-two groups only. Wraps and corners count.
5. Prefer a group of 8 over two groups of 4, and a group of 4 over two pairs, unless the larger group covers a 0.
6. For POS, circle 0s and use the flipped complement rule. Alternatively minimize the SOP of \(F'\) and complement.
7. Count what the stem names: products, literals, essential primes, or distinct minimal expressions. Those four numbers are different.
8. If options are expressions, evaluate each on one cell you can see, starting with a cell that looks distinctive.

---

## 9. Traps

| Trap | Correction |
|------|------------|
| Binary column order \(00,01,10,11\) | Gray order \(00,01,11,10\) |
| Group of 6 or 3 | Only powers of two |
| X must be covered | Only required 1s must be covered |
| X blocks a group | X may be inside the group |
| A 0 is inside a “clever” octet | The octet is illegal |
| Corner cells are not adjacent | \(m_0, m_2, m_8, m_{10}\) is a legal quad |
| Prime implies essential | A prime can be absent from some minimal cover |
| SOP circles used unchanged as POS | POS comes from the 0s, with the complement rule flipped |
| Minimal SOP is unique | Cyclic covers have several |

---

## 10. Connections

- **Algebra.** Each circle is one use of \(xy + xy' = x\). Consensus on the map is the optional third circle.
- **Tabular method.** The same primes, found by combining bit strings instead of drawing. Use it when the list is long or a count of all primes is required. The 2015 prime-implicant count is that situation.
- **Muxes.** After the map, a 4-to-1 mux implements the function by tying each data input to \(0\), \(1\), \(C\), or \(C'\). The map, split by the select variables, shows which.
- **Static hazards.** A minimal map and a hazard-free map are allowed to differ by consensus circles.
