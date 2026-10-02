# Relations — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** Define a binary relation on A = {1,2,3} with exactly 4 pairs including (1,2).

**2.** Is R = {(1,1), (2,2)} on {1,2,3} reflexive?

**3.** How many relations on a 2-element set?

**4.** What makes a relation an equivalence relation?

**5.** Give an example of a partial order on {1,2,3,6}.

---

## Level 2 — Standard GATE Style

**6.** R = {(1,1),(2,2),(3,3),(1,2),(2,1)} on {1,2,3}. List all properties that hold.

**7.** How many reflexive relations on a 3-element set?

**8.** R = {(a,b): a divides b} on {1,2,3,6}. Is it a partial order?

**9.** Find equivalence classes of R = {(a,b): a≡b (mod 2)} on {0,1,2,3,4,5}.

**10.** |A| = 4. How many symmetric relations?

---

## Level 3 — Multi-Step

**11.** R = {(1,2),(2,3),(3,4)}. Find transitive closure on {1,2,3,4}.

**12.** Composition: R = {(1,2),(2,3)}, S = {(3,1),(3,4)}. Find S∘R and R∘S (define as (a,c) with ∃b:(a,b)∈R,(b,c)∈S).

**13.** Minimum number of pairs to add to {(1,2),(2,3)} to make it reflexive and symmetric on {1,2,3}?

**14.** Prove: if R is equivalence, then [a]=[b] iff aRb.

---

## Level 4 — Trap Questions

**15.** R symmetric and transitive on {1,2}. Must R be reflexive?

**16.** Antisymmetric relation with (1,2) and (2,1). Possible?

**17.** Someone counts 2^6 relations on 3 elements. Error?

**18.** Is "≤" on ℝ an equivalence relation?

---

## Level 5 — Challenge

**19.** How many relations on {1,2,3} are both reflexive and antisymmetric?

**20.** On n elements, how many equivalence relations? (n=3 case: enumerate.)

**21.** R reflexive, |A|=n. Maximum number of pairs in antisymmetric R?

---

## Answers and Explanations

**1.** Example: {(1,2),(2,1),(3,3),(1,1)}.

**2.** **No** — missing (3,3).

**3.** 2^(2²) = 2⁴ = **16**.

**4.** Reflexive + symmetric + transitive.

**5.** **Divisibility** (1 divides all; transitive; antisymmetric).

**6.** Reflexive ✓, symmetric ✓, transitive ✓, antisymmetric ✗ (1↔2).

**7.** 2^(9−3) = 2⁶ = **64**.

**8.** **Yes** — reflexive, antisymmetric, transitive on positive divisors.

**9.** **[0]={0,2,4}**, **[1]={1,3,5}**.

**10.** 2^(4×5/2) = 2¹⁰ = **1024**.

**11.** Add (1,3),(1,4),(2,4): **{(1,2),(2,3),(3,4),(1,3),(1,4),(2,4)}** + reflexive if needed.

**12.** S∘R: (2,3)∈R,(3,1)∈S→(2,1); (2,3)∈R,(3,4)∈S→(2,4). **{(2,1),(2,4)}**. R∘S: (3,1)∈S,(1,2)∈R→(3,2); (3,4)∈S — no (4,?) in R. **{(3,2)}**.

**13.** Reflexive: add (1,1),(2,2),(3,3). Symmetric: add (2,1),(3,2). **5 pairs** added.

**14.** If aRb, x∈[a]⇒xRa; by symmetry aRx; by transitivity xRb ⇒ x∈[b] ⇒ [a]⊆[b]. Reverse similar.

**15.** **No** — R=∅ counterexample.

**16.** **No** — antisymmetric forces a=b when both directions.

**17.** Used 2^6 instead of 2^9 — should be **512**.

**18.** **No** — not symmetric (2≤3 but 3≰2).

**19.** Reflexive + antisymmetric: off-diagonal at most one direction each → 2^(n(n−1)/2) choices on off-diagonal? For n=3: diagonal fixed, 3 off-diagonal pairs each {in, out, none}? Antisymmetric: each unordered pair {i,j}, i≠j: options (i,j), (j,i), or neither — 3 choices per pair → 3^3=27 for n=3. General: **3^(n(n−1)/2)**.

**20.** n=3: partitions {123}, {12|3}, {13|2}, {23|1}, {1|2|3} → **5** (Bell B₃=5).

**21.** Maximum antisymmetric reflexive: diagonal all n pairs + at most one direction per off-diagonal pair → n + n(n−1)/2 = **n(n+1)/2**.
