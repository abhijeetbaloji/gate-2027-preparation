# Tabular Method (Quine–McCluskey)

The K-map finds prime implicants by eye. The tabular method finds the same primes by combining minterms whose binary labels differ in one bit. GATE uses it when the question asks for the **number** of prime implicants or essential prime implicants, especially on four variables with a scattered onset. The only mapped stem that sits in this folder is that kind of count (2015). The procedure below is what that count requires.

---

## 1. What is being listed

**Implicant.** A product that is 1 only on the onset or on don’t-cares.

**Prime implicant.** An implicant that is not contained in a larger one. In the table, it is a term that was never combined further.

**Essential prime implicant.** A prime that is the only prime covering some onset minterm. Don’t-care minterms do not create essential primes, because they do not have to be covered.

**Why combining distance-1 labels works.** If two products are identical except that one has \(x\) where the other has \(x'\), then

\[
P x + P x' = P.
\]

Their labels differ in one bit. Replacing that bit by a dash is exactly deleting the variable. Two terms may be combined only when their dashes are already in the same positions and exactly one remaining bit differs. Differing in two bits is not one application of the identity; those minterms are not adjacent.

---

## 2. The steps

1. **List** every onset minterm and every don’t-care, in binary. Group them by the number of 1s. Do not list required 0s.
2. **Combine** terms from adjacent groups (counts of 1s differ by 1) when the bit strings differ in one position. Write the result once, with a dash in that position. Tick every term that entered a combination.
3. **Repeat** on the dashed terms. Dashes must line up. Tick terms that combine further.
4. **Prime implicants** are the unticked terms, including a minterm that never paired.
5. **Chart.** Rows are primes. Columns are onset minterms only. Put a mark where the prime covers the minterm. A dash covers both 0 and 1 in that bit.
6. **Essential primes** are the rows that own a column with a single mark.
7. **Cover** the remaining columns with as few of the other primes as possible. Several covers of the same size are several minimal SOPs.

Don’t-cares are used in steps 1–4. They are omitted in steps 5–7.

---

## 3. Worked count: onset \((0,2,4,5,6,10)\)

This is the onset written in the 2015 stem \(f(w,x,y,z) = \sum(0,2,4,5,6,10)\). The mapping does not store a verified official key. The count below is the table for that onset.

Binary, by number of 1s. Order is \(wxyz\).

| Ones | Minterm | Bits |
|-----:|--------:|------|
| 0 | 0 | 0000 |
| 1 | 2 | 0010 |
| 1 | 4 | 0100 |
| 2 | 5 | 0101 |
| 2 | 6 | 0110 |
| 2 | 10 | 1010 |

**Pairs.**

| Combined | Result | Covers |
|----------|--------|--------|
| 0, 2 | \(00\text{-}0\) | 0, 2 |
| 0, 4 | \(0\text{-}00\) | 0, 4 |
| 2, 6 | \(0\text{-}10\) | 2, 6 |
| 2, 10 | \(\text{-}010\) | 2, 10 |
| 4, 5 | \(010\text{-}\) | 4, 5 |
| 4, 6 | \(01\text{-}0\) | 4, 6 |

5 does not combine with 10: \(0101\) and \(1010\) differ in three bits. 6 does not combine with 10: \(0110\) and \(1010\) differ in two bits. Every minterm entered a pair, so no minterm is itself prime.

**Quads.** \(00\text{-}0\) combines with \(01\text{-}0\) to give \(0\text{--}0\), covering 0, 2, 4, 6. The same quad comes from \(0\text{-}00\) with \(0\text{-}10\). The pair \(\text{-}010\) does not combine with \(0\text{-}10\): the dashes are not in the same column. The pair \(010\text{-}\) does not combine with anything else.

Tick every pair that entered the quad: \(00\text{-}0\), \(0\text{-}00\), \(0\text{-}10\), \(01\text{-}0\).

**Unticked, hence prime.**

| Prime | Bits | Product |
|-------|------|---------|
| \(P_1\) | \(0\text{--}0\) | \(w'z'\) |
| \(P_2\) | \(\text{-}010\) | \(x'yz'\) |
| \(P_3\) | \(010\text{-}\) | \(w'xy'\) |

Three prime implicants.

**Chart** (onset columns only):

| Prime | 0 | 2 | 4 | 5 | 6 | 10 |
|-------|---|---|---|---|---|----|
| \(w'z'\) | x | x | x | | x | |
| \(x'yz'\) | | x | | | | x |
| \(w'xy'\) | | | x | x | | |

Column 10 has a single mark, so \(x'yz'\) is essential. Column 5 has a single mark, so \(w'xy'\) is essential. Column 0 has a single mark, so \(w'z'\) is essential. All three primes are essential, and the unique minimal SOP is

\[
f = w'z' + x'yz' + w'xy'.
\]

**What the question asked.** “Total number of prime implicants,” not the number of essential ones, and not the number of products you feel like keeping. Here the two counts happen to agree. They do not always agree.

---

## 4. A case where prime and essential differ

Take \(f(A,B,C) = \sum m(0,1,2,5,6,7)\). Pairing produces six pair-implicants and no quads (every attempted quad hits a 0 at \(m_3\) or \(m_4\)).

The primes are \(A'B'\), \(A'C'\), \(B'C\), \(BC'\), \(AC\), \(AB\).

Each onset minterm sits in two primes. Example: \(m_0\) sits in \(A'B'\) and \(A'C'\). No column has a single mark, so the number of essential prime implicants is 0. A minimal cover still exists; it uses three of the six primes, for example \(A'C' + B'C + AB\). “Zero essential” does not mean “zero primes,” and it does not mean the function has no minimal SOP.

---

## 5. Don’t-cares in the table

List don’t-care minterms with the onset and combine them freely. In the chart, give them no column.

**Consequence.** A prime that covers only don’t-cares plus nothing new can appear in the prime list and then be useless in the cover. Do not count it as essential. A minimal SOP may leave every don’t-care equal to 0.

**The other direction.** Forcing every don’t-care to 0 before the table deletes combinations and can create extra literals. That is the minimal SOP of a smaller function.

**Chart trap.** Once \(m_0\) has been combined into a larger implicant, \(m_0\) is ticked, so \(m_0\) is not itself a prime. It remains a **column**. Ticking means “not prime.” It does not mean “already covered, delete the column.” The column is covered only when a selected prime contains that minterm.

---

## 6. Reading a product off a dashed string

Bits are \(ABCD\) from the left. A dash deletes that variable. A fixed 1 is the uncomplemented variable. A fixed 0 is the complement.

| String | Product on \(ABCD\) |
|--------|---------------------|
| \(010\text{-}\) | \(A'BC'\) |
| \(\text{-}010\) | \(B'CD'\) |
| \(0\text{--}0\) | \(A'D'\) |
| \(\text{-}101\) | \(BC'D\) |

The last row is the pair \(m_5 = 0101\) and \(m_{13} = 1101\): they differ only in \(A\), and the product is \(BC'D\).

---

## 7. How many primes versus how the chart finishes

| Question wording | What to count |
|------------------|---------------|
| Prime implicants | Unticked terms after combining stops |
| Essential prime implicants | Columns with a single mark |
| Products in a minimal SOP | Size of a smallest cover, which includes every essential prime plus a cheapest set for the rest |
| Literal occurrences | Sum of the non-dash bits over the chosen primes |

A prime that appears in every minimal SOP is not automatically essential. Essential is about a private minterm. A prime can be in every minimum cover because of a global tradeoff and still share every one of its minterms with other primes. If the question says “essential,” look for a single-mark column. If it says “in every minimal SOP,” the chart’s remaining cover can force a prime that is not essential. Do not swap the words.

---

## 8. When to use the table instead of the map

Use the map for three and four variables when you need one minimal expression and the 1s form obvious blocks. Use the table when:

- the stem asks for the number of primes, not one expression,
- don’t-cares and onset are interleaved and a picture is easy to mis-group,
- you need to show that a particular product is or is not prime.

Both methods must agree. If a map circle cannot be enlarged and the table ticked that term, one of the two was mis-drawn.

---

## 9. Traps

| Trap | Correction |
|------|------------|
| Combining labels two bits apart | Only distance 1, dashes already aligned |
| Don’t-care omitted from pairing | Include it while generating primes |
| Don’t-care given a chart column | Columns are onset only |
| Ticked minterm deleted from the chart | Tick means “not a prime row.” The column stays |
| All primes reported as essential | Only single-mark columns |
| A combined term’s binary value “averaged” | The dash is a deleted variable, not a digit |
| Minimal SOP used as the prime count | The prime count includes primes the cover rejects |

---

## 10. Connections

- **K-map.** Each successful combine is one adjacent circle growing. The chart is the same covering problem the map solves by inspection.
- **Algebra.** \(Px + Px' = P\) is the only identity the table uses. Consensus shows up later, as a non-essential prime.
- **Hazards.** A minimal cover from the chart can omit a consensus prime and still be minimal. That omitted prime is what a static-1 hazard discussion puts back.
