# Relations — Detailed Learning Notes (GATE CS)

Relations generalize comparisons (≤, =, divides). A relation on A is a subset of A×A. GATE tests properties, equivalence classes, partial orders, composition, closures, and counting.

---

## 1. Definition and Representations

### Concept
A **binary relation R** from set A to B is any subset of A×B. If A=B, R is a relation **on** A. Write aRb or (a,b)∈R.

**Representations:** set of ordered pairs; **directed graph** (vertices = elements, edge a→b if (a,b)∈R); **matrix** (M[i,j]=1 if related).

### Intuition
"Who is related to whom" — like a Facebook "follows" graph or "≤" on integers.

### Formal Definition
R ⊆ A×B. **Domain:** {a | ∃b (a,b)∈R}. **Range:** {b | ∃a (a,b)∈R}. **Inverse** R⁻¹ = {(b,a) | (a,b)∈R}.

### Important Properties
- Empty relation ∅ is always a relation
- Universal relation A×A relates every pair
- Identity relation I_A = {(a,a) | a∈A}

### Worked Example 1
A={1,2,3}, R={(1,1),(1,2),(2,3)}. Draw edges 1→1, 1→2, 2→3.

### Worked Example 2
"≤" on {1,2,3}: pairs (1,1),(1,2),(1,3),(2,2),(2,3),(3,3) — 6 pairs.

### GATE Connection
Given a digraph, identify properties or number of relations with given properties.

### Common Trap
Confusing relation **set** with **number** of relations on finite A: there are 2^(n²) relations on n-element set.

### Concept Connections
Functions are relations with unique image; equivalence relations partition sets; partial orders support lattices.

---

## 2. Reflexive, Symmetric, Antisymmetric, Transitive

### Concept
Let R be a relation on A.

| Property | Definition |
|----------|------------|
| **Reflexive** | ∀a∈A, (a,a)∈R |
| **Irreflexive** | ∀a∈A, (a,a)∉R |
| **Symmetric** | (a,b)∈R ⇒ (b,a)∈R |
| **Antisymmetric** | (a,b)∈R ∧ (b,a)∈R ⇒ a=b |
| **Transitive** | (a,b)∈R ∧ (b,c)∈R ⇒ (a,c)∈R |

### Intuition
Reflexive: every node has self-loop. Symmetric: bidirectional edges. Antisymmetric: no mutual edges between distinct elements. Transitive: shortcuts exist — edge chains collapse to direct edges.

### Formal Definition
As above. **Partial order** = reflexive + antisymmetric + transitive. **Equivalence** = reflexive + symmetric + transitive.

### Important Properties
- Symmetric + antisymmetric + reflexive on finite A ⇒ often identity-like on comparable pairs
- "≤" on ℝ: reflexive, antisymmetric, transitive; not symmetric
- "≠" is symmetric and irreflexive but **not** transitive on {1,2,3}: 1≠2, 2≠3 but 1=3 fails

### Derivation/Proof (when useful)
To **disprove** reflexivity: find one a with (a,a)∉R. To disprove transitivity: find (a,b),(b,c)∈R with (a,c)∉R.

### Worked Example 1
R on ℤ: aRb iff |a-b|≤1. Reflexive yes. Symmetric yes. Transitive? 0R1 and 1R2 but 0R2? |0-2|=2>1 — **not transitive**.

### Worked Example 2
Divisibility on {1,2,4,8}: 2|4, 4|8, 2|8 — transitive. Antisymmetric: if a|b and b|a then a=b (positive integers).

### GATE Connection
Table/digraph → tick properties; minimal edits to make relation transitive/reflexive.

### Common Trap
**General/common trap:** Symmetric ≠ transitive. Antisymmetric allows (a,a) loops; irreflexive forbids them.

### Concept Connections
Logic quantifiers formalize properties: reflexive ≡ ∀x R(x,x).

---

## 3. Equivalence Relations and Partitions

### Concept
R is an **equivalence relation** if reflexive, symmetric, and transitive.

**Equivalence class** of a: [a] = {b∈A | aRb}. **Partition** of A: disjoint nonempty subsets whose union is A.

### Intuition
Equivalence = "same bucket" relation: modular congruence, same birth month, graph connectivity.

### Formal Definition
Theorem: equivalence relations ↔ partitions (one-to-one correspondence). **[a]∩[b] = ∅ or [a]=[b]**. A = ⋃ [a_i].

### Important Properties
- Refinement: finer equivalence = more classes, smaller classes
- Number of equivalence relations on n-element set = **Bell number** B_n (GATE may ask small n)

### Worked Example 1
On {1,2,3,4}, aRb iff a≡b (mod 2). Classes: {1,3}, {2,4}.

### Worked Example 2
How many equivalence relations on 3-element set? B_3 = **5** (partitions: 1+1+1, 2+1, 3).

### GATE Connection
Count classes, size of [a], verify partition from given classes.

### Common Trap
Classes must **cover** A and be **disjoint**. Missing an element invalidates partition.

### Concept Connections
Congruence mod n in **groups**; kernel of homomorphism is equivalence.

---

## 4. Partial Orders

### Concept
**Partial order (poset)** (A,≤): reflexive, antisymmetric, transitive. Not every pair comparable — "partial".

**Comparable:** a≤b or b≤a. **Total order:** all pairs comparable.

**Hasse diagram:** draw a→b if a covers b (no c with a<c<b); omit loops and transitive edges.

### Intuition
Hierarchy: divisibility, subsets by inclusion, subtasks in project — not all siblings comparable.

### Formal Definition
a **covers** b if b<a and no c with b<c<a. **Immediate predecessor/successor** in finite posets.

### Important Properties
- Minimal element: no element strictly below it (can be several)
- Minimum: unique least element ≤ all (if exists)
- Maximal / maximum dual definitions

### Worked Example 1
Divisibility on {1,2,3,6,12}. Hasse: 1 below 2,3; 2,3 below 6; 6 below 12.

### Worked Example 2
( P({a,b}), ⊆ ). Bottom ∅, top {a,b}; {a} and {b} incomparable.

### GATE Connection
Hasse diagram reading; count minimal/maximal elements; identify chains.

### Common Trap
**General/common trap:** Minimal ≠ minimum (uniqueness). Maximal ≠ maximum.

### Concept Connections
Leads to **lattices** (topic 05) — join/meet existence.

---

## 5. Composition of Relations

### Concept
If R ⊆ A×B and S ⊆ B×C, **composition** S∘R (or R;S) = {(a,c) | ∃b∈B: (a,b)∈R ∧ (b,c)∈S}.

For relations on A: R² = R∘R, R^n = compose n times.

### Intuition
Two-hop paths: parent→child and child→grandchild gives parent→grandchild if transitive closure not yet added.

### Formal Definition
Matrix multiply: M_{R∘S} = M_R · M_S over Boolean semiring (OR of ANDs).

### Important Properties
Composition associative: (T∘S)∘R = T∘(S∘R). Identity I satisfies I∘R = R∘I = R.

### Worked Example 1
R={(1,2),(2,3)} on {1,2,3}. R² = {(1,3)}.

### Worked Example 2
Parent relation P. P² = grandparent. Transitive closure P⁺ = ancestor.

### GATE Connection
Compute R² from matrix or digraph; count pairs in composition.

### Common Trap
Order matters: R∘S ≠ S∘R in general.

### Concept Connections
Function composition is special case; **Warshall** computes transitive closure.

---

## 6. Closures: Reflexive, Symmetric, Transitive

### Concept
**Closure** of R with property P = smallest relation containing R that has property P.

- **Reflexive closure:** R ∪ I_A
- **Symmetric closure:** R ∪ R⁻¹
- **Transitive closure:** smallest transitive superset; R⁺ = ⋃_{n≥1} R^n; reflexive-transitive R* = R⁺ ∪ I

### Intuition
Add minimum edges to satisfy a property — like adding self-loops or shortcut edges.

### Formal Definition
Transitive closure on finite A with |A|=n: at most n-1 hops needed in path (or use Warshall O(n³)).

### Important Properties
If R already transitive, closure = R. Symmetric closure of ≤ is not transitive in general.

### Worked Example 1
R={(1,2),(2,3)}. Reflexive closure adds (1,1),(2,2),(3,3). Transitive closure adds (1,3).

### Worked Example 2
Reachability in directed graph = reflexive-transitive closure of edge relation.

### GATE Connection
"Minimum edges to add" problems; closure size counting.

### Common Trap
Reflexive-transitive closure ≠ transitive closure unless you add I explicitly.

### Concept Connections
**Graph connectivity**; **regular expressions** and automata (Kleene star analogy).

---

## 7. Counting Relations

### Concept
On set A with |A|=n:
- Total relations: **2^(n²)** (each pair in/out)
- Reflexive relations: **2^(n²−n)** (diagonal forced in)
- Irreflexive: **2^(n²−n)** (diagonal forced out)
- Symmetric: choose upper triangle + diagonal freely: **2^(n(n+1)/2)**
- Antisymmetric: off-diagonal pairs independent in one direction: **2^(n(n+1)/2)** (same count as symmetric!)
- Partial orders: no simple 2^k formula for general n — GATE uses small n or known facts

### Intuition
Independent binary choices on allowed positions in matrix subject to constraints.

### Formal Definition
Reflexive + symmetric + transitive = equivalence: count = Bell(n). Reflexive + antisymmetric + transitive = partial orders — enumerate for n≤4 in GATE.

### Worked Example 1
n=2: 2^4=16 total relations. Reflexive: 2^2=4.

### Worked Example 2
n=3 symmetric relations: 2^(3·4/2)=2^6=64.

### GATE Connection
"How many relations on 3 elements are both reflexive and symmetric?" → 2^(9−3)=2^6=64? Wait reflexive+symmetric on n=3: diagonal fixed in, upper triangle 3 pairs optional each way but symmetric fixes pairs — formula 2^(n(n-1)/2) for reflexive symmetric? Reflexive symmetric: diagonal in, upper triangle free: 2^(n(n-1)/2) = 2^3=8 for n=3.

### Common Trap
Mixing formulas for symmetric vs antisymmetric — same count but different meaning.

### Concept Connections
**Combinatorics**; **Bell numbers**; **OEIS** patterns for small n.

---

## 8. Relation Matrices and Warshall's Algorithm

### Concept
Adjacency matrix M_R[i,j]=1 iff (i,j)∈R. Transitive closure: Warshall triple loop OR compute R∪R²∪… until stable.

### Intuition
If i→k and k→j, add i→j for transitive closure.

### Formal Definition
Warshall: for k,i,j: M[i,j] |= M[i,k] & M[k,j].

### Worked Example 1
Apply Warshall on 3-node graph; verify reachability matrix.

### Worked Example 2
Boolean matrix power: (M∨M²∨M³) for n=3 gives transitive closure (with reflexive if add I).

### GATE Connection
One-step Warshall update or "entry (i,j) after considering node k".

### Common Trap
Off-by-one in indexing; forgetting reflexive diagonal if asked for R*.

### Concept Connections
**Floyd-Warshall** shortest paths variant; **graph algorithms**.

---

## Summary Checklist
- Verify four properties from matrix/digraph
- Equivalence → partition; count classes
- Poset → Hasse; minimal vs minimum
- Compose relations; compute closures
- Count relations: 2^(n²), symmetric 2^(n(n+1)/2), reflexive 2^(n²−n)
- Bell numbers for equivalences on small sets

