# Partial Orders and Lattices — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. Partial orders in GATE

## Posets

### Concept

A **partial order (PO)** on P is a relation ≤ that is **reflexive, antisymmetric, and transitive**.

### Intuition

Some elements compare; others may be incomparable (neither ≤ the other).

### Definition

(P,≤) is a **poset**. **Total order** if every pair is comparable.

### Examples

Divisibility on {1,2,3,6}: 2 and 3 incomparable.

### GATE Connection

Hasse diagrams, extrema, lattice operations.

### Traps

Antisymmetric ≠ asymmetric — PO allows (a,a).


## 2. Hasse diagrams

## Cover relations visually

### Concept

Draw element a below b iff a<b and no c with a<c<b (**cover**). Omit loops and transitive edges.

### Intuition

Transitive shortcuts are implied upward.

### Examples

Power set of {a,b}: ∅ bottom, {a},{b} middle, {a,b} top.

### GATE Connection

Read comparability and extrema from picture.

### Traps

Drawing all transitive edges — clutters diagram.


## 3. Minimal, maximal, least, greatest

## Four extrema types

### Concept

**Minimal:** no element strictly below. **Maximal:** none strictly above. **Least (minimum):** ≤ all. **Greatest (maximum):** all ≤ it.

### Intuition

Minimals are 'bottom layer'; minimum is unique lowest if it exists.

### Examples

On {1,2,3,6}| divides: minimum 1, maximum 6; minimals={1}, maximals={6}.

### GATE Connection

MSQ: which elements are maximal?

### Traps

Multiple maximals ≠ maximum element exists.


## 4. LUB and GLB

## Join and meet

### Concept

**Join a∨b** = least upper bound (LUB). **Meet a∧b** = greatest lower bound (GLB).

### Intuition

Join is smallest common upper; meet is largest common lower.

### Definition

**Lattice:** every pair has join and meet. **Complete lattice:** every subset has LUB/GLB.

### Examples

On divisibility poset {1,2,3,6}: 2∨3=6, 2∧3=1.

### GATE Connection

Verify lattice laws or compute join/meet.

### Traps

Subset closed under meet may fail join — not sublattice.


## 5. Lattice identities

## Algebraic laws

### Concept

In a lattice: a≤b ⇔ a∧b=a ⇔ a∨b=b. Also commutativity, associativity, absorption: a∧(a∨b)=a.

### Derivation

From order definition of ∧,∨.

### GATE Connection

Proof-style MCQ on equivalences.

### Traps

Assuming distributivity — lattices need not distribute.


## 6. Chains and antichains

## Totally ordered subsets

### Concept

**Chain:** totally ordered subset. **Antichain:** no two distinct elements comparable.

### Intuition

Chain is a line; antichain is an incomparable set.

### Examples

In divisibility on {1,…,12}, {2,4,8} is a chain; {2,3,5} is an antichain.

### GATE Connection

Dilworth-style intuition; count comparable pairs in chain length n: n(n+1)/2.

### Traps

Single element sets are both chain and antichain.


## 7. Product and subposets

## Building new posets

### Concept

Product order: (a,b)≤(c,d) iff a≤c and b≤d. Subposet inherits order.

### Examples

2×2 chain product gives 4-element grid poset.

### GATE Connection

Recognize product structure in Hasse diagrams.

### Traps

Cartesian product cardinality multiplies; cover edges may differ.


## 8. Special elements ⊤ and ⊥

## Top and bottom

### Concept

**Bottom ⊥** ≤ every element; **top ⊤** ≥ every element — unique if they exist.

### Examples

In (P(S),⊆), ∅ is bottom, S is top.

### GATE Connection

Identify in power set and divisibility lattices.

### Traps

Finite PO may lack top/bottom if bounds not in set.


## 9. Sublattices

## Closed under both operations

### Concept

S ⊆ L is **sublattice** if closed under ∧ and ∨ (same as in L).

### Examples

{1,2,6} in divisibility on {1,2,3,6} — check joins/meets stay inside.

### GATE Connection

Verify closure on candidate subsets.

### Traps

Subset that is subposet but not sublattice — missing join of two elements.


## 10. GATE problem patterns

## What to practice

### Concept

Draw Hasse from relation; list maximals; test lattice; compute join/meet.

### GATE Connection

Divisibility and subset lattices dominate.

### Traps

Confuse 'divides' direction — smaller divides larger below in Hasse.


---

Link back to `03-RELATIONS` for PO definition.
