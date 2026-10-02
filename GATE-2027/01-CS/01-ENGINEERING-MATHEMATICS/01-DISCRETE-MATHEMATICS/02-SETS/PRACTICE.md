# GATE-STYLE PRACTICE — Sets

## Level 1 — Concept Check

**1.** Which is true for A = {1, {2}}?
(a) 2 ∈ A  (b) {2} ∈ A  (c) {2} ⊆ A  (d) |A| = 3

**2.** |P(A)| if |A| = 7?

**3.** (A ∩ B) ∪ (A ∩ B^c) equals?

**4.** If A ⊆ B, then A ∩ B = ?

**5.** |A × B| if |A| = 0, |B| = 5?

---

## Level 2 — Standard GATE

**6.** |A|=45, |B|=38, |A∩B|=12. Find |A ∪ B|.

**7.** How many subsets of {1,2,…,12} contain both 1 and 12?

**8.** Integers 1..100 divisible by 2 or 3: count?

**9.** Simplify (A ∪ B)^c ∩ (A ∪ C) using De Morgan (set equivalent form).

**10.** A={1,2,3}, B={2,3,4}. List A △ B and |A △ B|.

---

## Level 3 — Multi-Step

**11.** Universal set U has 120 elements. |A|=70, |B|=55, |C|=40, |A∩B|=20, |A∩C|=15, |B∩C|=10, |A∩B∩C|=5. Find |A∪B∪C|.

**12.** How many 8-bit strings contain at least one 1? (Use complement.)

**13.** |A|=n. How many subsets of A have even cardinality? (Hint: bijection with odd.)

**14.** A×B has 24 elements. |A|=6. Find |B|. If additionally |A×A|=36, find A?

**15.** In a survey of 200: 120 like tea, 100 like coffee, 50 like both. How many like neither?

---

## Level 4 — Trap Questions

**16.** Number of elements in P(P({∅}))?

**17.** Is {∅} ⊆ {∅, {∅}}? Is {∅} ∈ {∅, {∅}}?

**18.** If A×B = B×A and both nonempty, must A = B?

**19.** |A∪B| = |A| + |B|. What can you conclude about A∩B?

**20.** Complement of A in U: |A^c| = |U| − |A|. If we shrink U, does A^c always shrink?

---

## Level 5 — Challenge

**21.** How many subsets of {1,…,n} contain no two consecutive integers? (Classic: Fibonacci — state F_{n+2} for n≥1.)

**22.** Prove |A△B| = |A| + |B| − 2|A∩B|.

**23.** For finite U, show |(A△B)△C| counts elements in odd number of sets (inclusion in A,B,C).

**24.** Count solutions to x+y+z=10 with x,y,z nonnegative integers (stars and bars).

**25.** If f: P(A) → {0,1} maps subset to parity of |X|, how many fibers of size 1?

---

## Answers (Full Reasoning)

**1.** (b) and (c). {2} is an element; {2} is also subset if we read {2} as element only — actually 2∉A, {2}∈A, {2}⊈A since 2∉A but {2}∈A means subset {2} would require 2∈A. |A|=2. **Answer: (b) only** among listed — (c) false. Best: **(b)**.

**2.** 2^7 = **128**.

**3.** A ∩ (B ∪ B^c) = A ∩ U = **A**.

**4.** **A** (since A⊆B ⇒ every element of A is in B).

**5.** Empty product: **0**.

**6.** 45+38−12 = **71**.

**7.** Fix 1 and 12; choose any of remaining 10 elements: 2^10 = **1024**.

**8.** |2|=50, |3|=33, |6|=16 → 50+33−16 = **67**.

**9.** **A^c ∩ B^c ∩ (A ∪ C)** (De Morgan on first part only).

**10.** A△B = {1,4}, size **2**. |A|+|B|−2|A∩B| = 3+3−2·2 = 2 ✓

**11.** 70+55+40−20−15−10+5 = **125**.

**12.** Total 2^8 − string of all zeros = 256−1 = **255**.

**13.** Exactly half of 2^n subsets: **2^(n−1)** for n≥1 (bijection X↦X△{a}).

**14.** |B|=24/6=**4**. |A×A|=36 ⇒ |A|=**6** consistent.

**15.** |T∪C|=120+100−50=170; neither=200−170=**30**.

**16.** |P({∅})|=2, then P of 2-element set: **4**.

**17.** {∅}⊆{∅,{∅}} **True** (empty set subset of every set). {∅}∈{∅,{∅}} **True** (explicit element).

**18.** Not necessarily: A={1}, B={2} gives A×B ≠ B×A unless |A|=|B| and more — actually if A×B=B×A with A,B nonempty, then |A|=|B| and often A=B when |A|=|B|=1 etc. Counter: A={1,2}, B={1,2} works; for unequal — **need |A|=|B|**; still A≠B possible? If (a,b) order matters, A×B=B×A forces same ordered pairs ⇒ typically **A=B** when nonempty. Rigorous: **Yes, A=B** if A×B=B×A and both nonempty.

**19.** **A∩B = ∅** (disjoint).

**20.** **No** — complement is relative to U; removing elements from U changes A^c.

**21.** **F_{n+2}** (Fibonacci); e.g. n=5 → 13 subsets.

**22.** A△B splits into A−B, B−A disjoint; |A−B|=|A|−|A∩B|, |B−A|=|B|−|A∩B|; sum gives formula.

**23.** Symmetric difference associativity; triple △ corresponds to XOR of characteristic vectors.

**24.** C(10+3−1,3−1)=C(12,2)=**66**.

**25.** Each subset maps to parity; each fiber has many subsets unless |A|=0 — trick question: **2^(n−1)** subsets map to each parity class for |A|=n≥1.

