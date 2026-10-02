# Sets — Detailed Learning Notes (GATE CS)

These notes cover **Engineering Mathematics → Discrete Mathematics → Sets** for GATE Computer Science. Read section by section; use `REVISION.md` only after studying here.

---

## 1. Sets, Elements, and Notation

### Concept
A **set** is a well-defined collection of **distinct** objects called **elements**. We write membership as \(a \in A\) ("a belongs to A") and non-membership as \(a \notin A\).

Standard sets in GATE: **natural numbers** \(\mathbb{N}\), **integers** \(\mathbb{Z}\), **rationals** \(\mathbb{Q}\), **reals** \(\mathbb{R}\). The **empty set** \(\emptyset\) has no elements. A **universal set** \(U\) is the fixed universe for complements in a given problem.

**Roster (listing):** \(A = \{1, 3, 5\}\). **Set-builder:** \(B = \{x \in \mathbb{Z} \mid x^2 < 10\} = \{-3,-2,-1,0,1,2,3\}\).

### Intuition
Think of a set as a bag of unique labels. Order does not matter: \(\{1,2,3\} = \{3,1,2\}\). Repeats collapse: \(\{1,1,2\} = \{1,2\}\).

### Formal Definition
A set \(A\) is a subset of a universe \(U\). **Cardinality** \(|A|\) is the number of elements (GATE focuses on finite sets). Sets \(A\) and \(B\) are **equal** iff \(\forall x,\; x \in A \Leftrightarrow x \in B\).

### Important Properties
- \(\emptyset\) is unique and is a subset of every set: \(\forall A,\; \emptyset \subseteq A\).
- \(\emptyset \in A\) is **false** in general — do not confuse subset with element.
- Singleton: \(\{a\}\) has cardinality 1. Doubleton: two elements.
- **Finite vs infinite:** GATE counting questions almost always use finite sets.

### Derivation/Proof (when useful)
**Uniqueness of empty set:** If \(\emptyset_1\) and \(\emptyset_2\) both have no elements, then for any \(x\), \(x \in \emptyset_1 \Leftrightarrow x \in \emptyset_2\) (both false), so \(\emptyset_1 = \emptyset_2\).

### Worked Example 1
Let \(U = \{1,2,\ldots,10\}\), \(A = \{x \in U \mid x \text{ is even}\}\). Then \(A = \{2,4,6,8,10\}\) and \(|A| = 5\).

### Worked Example 2
Write \(\{x \in \mathbb{Z} \mid |x| \le 2\}\) in roster form: \(\{-2,-1,0,1,2\}\), cardinality 5.

### GATE Connection
GATE often tests **set-builder translation** from English ("all even integers between 1 and 20") and **cardinality of a described set** without listing every element.

### Common Trap
Using \(\in\) when you mean \(\subseteq\). Example: \(\{1\} \subseteq \{1,2\}\) is true, but \(\{1\} \in \{1,2\}\) is false (unless the set contains the set as an element).

### Concept Connections
Sets are the foundation for **relations** (subsets of \(A \times B\)), **functions** (special relations), and **probability** sample spaces.

---

## 2. Subsets, Proper Subsets, and Power Sets

### Concept
\(A \subseteq B\) means every element of \(A\) is in \(B\): \(\forall x,\; x \in A \Rightarrow x \in B\).
**Proper subset** \(A \subset B\): \(A \subseteq B\) and \(A \neq B\).

The **power set** \(\mathcal{P}(A)\) (also written \(2^A\)) is the set of **all subsets** of \(A\).

### Intuition
Subsets are "choices" of elements from \(A\). For each element, include it or not — binary choice per element.

### Formal Definition
\(\mathcal{P}(A) = \{X \mid X \subseteq A\}\). If \(|A| = n\) (finite), then \(|\mathcal{P}(A)| = 2^n\).

### Important Properties
- \(A \subseteq A\) (every set is a subset of itself) — reflexivity of subset relation.
- \(\mathcal{P}(\emptyset) = \{\emptyset\}\), so \(|\mathcal{P}(\emptyset)| = 1\).
- \(\mathcal{P}(\{a\}) = \{\emptyset, \{a\}\}\) — two elements.
- If \(A \subseteq B\) then \(\mathcal{P}(A) \subseteq \mathcal{P}(B)\).

### Derivation/Proof (when useful)
**Proof that \(|\mathcal{P}(A)| = 2^n\):** List \(A = \{a_1,\ldots,a_n\}\). Each subset corresponds to an \(n\)-bit string where bit \(i\) is 1 iff \(a_i\) is included. There are \(2^n\) binary strings.

### Worked Example 1
\(A = \{1,2\}\). Then \(\mathcal{P}(A) = \{\emptyset, \{1\}, \{2\}, \{1,2\}\}\), count \(2^2 = 4\).

### Worked Example 2
How many **proper** subsets does a set of size 5 have? Total subsets \(2^5 = 32\); subtract 1 for the set itself: **31**. (Some texts also exclude \(\emptyset\); read the question.)

### GATE Connection
Classic question: "Number of subsets of \(\{1,\ldots,n\}\) that contain 7" → fix 7 in, choose freely from remaining \(n-1\) elements: \(2^{n-1}\).

### Common Trap
**General/common trap:** \(\mathcal{P}(\{ \emptyset \})\) has elements \(\emptyset\) and \(\{\emptyset\}\) — **two** elements, not one. Another trap: confusing \(|\mathcal{P}(A)|\) with \(|A|\).

### Concept Connections
Power set size links to **combinatorics** (binary choices) and **inclusion–exclusion** (counting union sizes).

---

## 3. Set Operations: Union, Intersection, Difference, Complement

### Concept
Given universe \(U\) and sets \(A, B \subseteq U\):

| Operation | Notation | Meaning |
|-----------|----------|---------|
| Union | \(A \cup B\) | \(\{x \mid x \in A \text{ or } x \in B\}\) |
| Intersection | \(A \cap B\) | \(\{x \mid x \in A \text{ and } x \in B\}\) |
| Difference | \(A - B\) | \(\{x \mid x \in A \text{ and } x \notin B\}\) |
| Complement | \(A^c\) or \(\overline{A}\) | \(\{x \in U \mid x \notin A\}\) |

**Disjoint:** \(A \cap B = \emptyset\).

### Intuition
Union = "either bucket"; intersection = "overlap"; difference = "in A but not B"; complement = "everything in universe outside A".

### Formal Definition
Operations satisfy **commutativity** of \(\cup, \cap\); **associativity**; **distributive laws**:
- \(A \cup (B \cap C) = (A \cup B) \cap (A \cup C)\)
- \(A \cap (B \cup C) = (A \cap B) \cup (A \cap C)\)

**Identity:** \(A \cup \emptyset = A\), \(A \cap U = A\). **Domination:** \(A \cup U = U\), \(A \cap \emptyset = \emptyset\).

### Important Properties
- \(A - B = A \cap B^c\)
- \(A \subseteq B \Leftrightarrow A \cap B = A \Leftrightarrow A \cup B = B\)
- \(|A \cup B| \leq |A| + |B|\) with equality iff disjoint

### Worked Example 1
\(U = \{1,\ldots,10\}\), \(A = \{1,2,3,4,5\}\), \(B = \{4,5,6,7\}\).
- \(A \cup B = \{1,2,3,4,5,6,7\}\), \(|A \cup B| = 7\)
- \(A \cap B = \{4,5\}\), \(|A \cap B| = 2\)
- \(A - B = \{1,2,3\}\)

### Worked Example 2
If \(|A|=20\), \(|B|=15\), \(|A \cap B|=5\), then \(|A \cup B| = 20+15-5 = 30\).

### GATE Connection
Set identity questions often rewrite \(A \cap (B \cup C)\) or ask which Venn region a expression describes.

### Common Trap
**General/common trap:** \(A - B \neq B - A\) in general. Also, complement depends on **declared universe** \(U\).

### Concept Connections
Set operations mirror **logical connectives** (∨, ∧, ¬) — De Morgan bridges the two worlds.

---

## 4. De Morgan's Laws (Sets and Logic)

### Concept
For subsets of universe \(U\):
- \((A \cup B)^c = A^c \cap B^c\)
- \((A \cap B)^c = A^c \cup B^c\)

Generalized: \(\left(\bigcup_i A_i\right)^c = \bigcap_i A_i^c\) and dual.

### Intuition
"Not in the union" means outside **every** piece — intersection of complements. "Not in the intersection" means missing **at least one** piece — union of complements.

### Formal Definition
Complement is relative to \(U\). De Morgan follows from logical equivalences \(\neg(P \lor Q) \equiv \neg P \land \neg Q\).

### Important Properties
- Dual laws help simplify nested complements: \(((A^c)^c = A)\)
- Useful for proving set equalities: show \(x \in LHS \Leftrightarrow x \in RHS\)

### Derivation/Proof (when useful)
**Proof of \((A \cup B)^c = A^c \cap B^c\):**
\(x \in (A \cup B)^c \Leftrightarrow x \notin A \cup B \Leftrightarrow x \notin A \text{ and } x \notin B \Leftrightarrow x \in A^c \cap B^c\).

### Worked Example 1
Simplify \((A \cup B)^c \cap (A \cup C)\). Using De Morgan: \((A^c \cap B^c) \cap (A \cup C)\). No single name — distribute if needed for counting regions.

### Worked Example 2
Prove \(A - (B \cup C) = (A - B) \cap (A - C)\).
\(x \in A - (B \cup C) \Leftrightarrow x \in A \land x \notin B \cup C \Leftrightarrow x \in A \land x \notin B \land x \notin C \Leftrightarrow x \in (A-B) \cap (A-C)\).

### GATE Connection
GATE loves "which is equal to" with complements and unions — apply De Morgan before brute Venn shading.

### Common Trap
Forgetting that complement is w.r.t. \(U\). If universe shrinks, complements change.

### Concept Connections
Same laws in **propositional logic** and **Boolean algebra** — CS students see this in digital logic too.

---

## 5. Cardinality and the Inclusion–Exclusion Principle

### Concept
For finite sets, **inclusion–exclusion (I–E)** counts elements in a union without double-counting overlap.

**Two sets:**
\[|A \cup B| = |A| + |B| - |A \cap B|\]

**Three sets:**
\[|A \cup B \cup C| = |A|+|B|+|C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|\]

### Intuition
Add each set, subtract pairwise overlaps (counted twice), add back triple overlap (subtracted once too many).

### Formal Definition
For \(n\) sets \(A_1,\ldots,A_n\):
\[\left|\bigcup_{i=1}^n A_i\right| = \sum |A_i| - \sum |A_i \cap A_j| + \cdots + (-1)^{n+1}|A_1 \cap \cdots \cap A_n|\]

### Important Properties
If pairwise disjoint: \(|A_1 \cup \cdots \cup A_n| = \sum |A_i|\).
**Complement counting:** \(|A^c| = |U| - |A|\).

### Derivation/Proof (when useful)
Two-set case: partition \(A \cup B\) into three disjoint regions: \(A-B\), \(B-A\), \(A \cap B\). Sizes: \(|A-B|+|A \cap B|=|A|\), \(|B-A|+|A \cap B|=|B|\), sum gives formula.

### Worked Example 1
In a class of 100 students: 60 know Java, 45 know Python, 25 know both. How many know at least one?
\(|J \cup P| = 60 + 45 - 25 = 80\).

### Worked Example 2
How many integers from 1 to 1000 are divisible by 2, 3, or 5?
Let \(A_2, A_3, A_5\) be divisible sets.
\(|A_2|=500\), \(|A_3|=333\), \(|A_5|=200\), \(|A_6|=166\), \(|A_{10}|=100\), \(|A_{15}|=66\), \(|A_{30}|=33\).
I–E: \(500+333+200-166-100-66+33 = 734\).

### GATE Connection
Divisibility counting, survey problems, and "at least one property" are standard GATE patterns.

### Common Trap
**General/common trap:** Using two-set formula for three sets without the triple intersection term. Sign alternation errors in general I–E.

### Concept Connections
I–E is the discrete version of **probability** \(P(A \cup B) = P(A)+P(B)-P(A \cap B)\) for uniform finite spaces.

---

## 6. Cartesian Product

### Concept
For sets \(A\) and \(B\), the **Cartesian product** is:
\[A \times B = \{(a,b) \mid a \in A,\; b \in B\}\]
Ordered pairs — **order matters**: \((a,b) \neq (b,a)\) unless \(a=b\) and sets coincide appropriately.

### Intuition
Rows × columns grid: every choice of first component paired with every choice of second.

### Formal Definition
If \(|A|=m\), \(|B|=n\) (finite), then \(|A \times B| = m \cdot n\).
Generally \(|A_1 \times \cdots \times A_k| = \prod |A_i|\).

### Important Properties
- \(A \times B \neq B \times A\) in general (unless \(A=B\) or one is empty)
- \(A \times (B \cup C) = (A \times B) \cup (A \times C)\) — but **not** distributive over intersection on both sides without care
- A **relation** from \(A\) to \(B\) is a subset of \(A \times B\)
- A **function** \(A \to B\) picks exactly one \(b\) for each \(a\)

### Worked Example 1
\(A=\{0,1\}\), \(B=\{a,b,c\}\). Then \(|A \times B| = 6\). List: all pairs \((0,a),(0,b),(0,c),(1,a),(1,b),(1,c)\).

### Worked Example 2
How many binary strings of length 8? Model as \(\{0,1\}^8\), count \(2^8 = 256\).

### GATE Connection
Counting functions, relations, and strings often reduce to counting elements in products or subsets of products.

### Common Trap
Confusing \(A \times B\) (set of pairs) with a single pair or with \(A \cap B\).

### Concept Connections
Direct link to **relations**, **functions**, and **combinatorics** (multiplication principle).

---

## 7. Symmetric Difference and Venn Diagrams

### Concept
**Symmetric difference:** \(A \triangle B = (A - B) \cup (B - A) = (A \cup B) - (A \cap B)\).
Elements in exactly one of \(A\) or \(B\).

**Venn diagram:** regions represent sets; overlaps = intersections; outside all circles = complement of union (within \(U\)).

### Intuition
Symmetric difference = "XOR" of membership — in A or B but not both.

### Formal Definition
\(\triangle\) is commutative and associative. \(A \triangle \emptyset = A\). \(A \triangle A = \emptyset\).

### Important Properties
- \(A \triangle B = B \triangle A\)
- \((A \triangle B) \triangle C = A \triangle (B \triangle C)\)
- \(|A \triangle B| = |A| + |B| - 2|A \cap B|\) for finite sets

### Worked Example 1
\(A=\{1,2,3,4\}\), \(B=\{3,4,5,6\}\). \(A \triangle B = \{1,2,5,6\}\).

### Worked Example 2
Draw three circles for \(A,B,C\). Region \(A \cap B \cap C^c\) = in A and B but not C. Translate set expressions to shaded regions in MCQs.

### GATE Connection
Venn-diagram MCQs: label 7 regions for three sets and assign counts or solve for unknown region sizes.

### Common Trap
Shading \(A \cup B\) when question asks for \(A \cap B\), or missing **outside** region as part of \(U\).

### Concept Connections
Symmetric difference appears in **error detection** (XOR) and **Boolean algebra**.

---

## 8. Counting Subsets with Constraints

### Concept
Count subsets of \(A\) satisfying properties: contain a fixed element, size \(k\), disjoint from \(B\), etc.

### Intuition
Fix forced choices, free choices on the rest; or use complement counting.

### Formal Definition
Number of \(k\)-subsets of an \(n\)-set: \(\binom{n}{k}\). Subsets containing fixed \(x\): \(2^{n-1}\). Subsets disjoint from \(B \subseteq A\): choose only from \(A - B\), so \(2^{|A|-|B|}\) if \(B \subseteq A\).

### Important Properties
- Subsets **not containing** any element of \(B\): power set of \(A - B\)
- Subsets **containing all** of \(S \subseteq A\): choose freely from \(A - S\): \(2^{|A|-|S|}\)

### Worked Example 1
How many subsets of \(\{1,\ldots,10\}\) contain 3 but not 7?
Fix 3 in, exclude 7: choose freely from remaining 8 elements: \(2^8 = 256\).

### Worked Example 2
How many subsets of size 3 from a 6-element set? \(\binom{6}{3} = 20\).

### GATE Connection
Combines set theory with **combinatorics** — very frequent multi-concept questions.

### Common Trap
Double-counting when constraints overlap; forgetting that \(\emptyset\) is a valid subset unless excluded.

### Concept Connections
Leads to **binomial coefficients** and **generating functions** in advanced combinatorics.

---

## Summary Checklist for GATE (Sets)
- Translate English ↔ set-builder notation
- Compute \(|A \cup B|\), three-set I–E, complement counts
- Power set size \(2^n\); proper subset counts
- De Morgan simplification
- Cartesian product size; link to relations/functions
- Venn region identification
- Subset counting with constraints

