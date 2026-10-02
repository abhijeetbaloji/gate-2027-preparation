# Combinatorics: Counting — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. Counting in GATE

## Discrete enumeration

### Concept

Count arrangements, selections, distributions under constraints.

### Intuition

Organize counting into steps; avoid double counting.

### GATE Connection

Permutations, combinations, IEP, pigeonhole — high frequency.

### Traps

Order matters vs does not — decide first.


## 2. Sum and product rules

## Fundamental principles

### Concept

**Sum:** disjoint alternatives add. **Product:** independent sequential choices multiply.

### Examples

3 shirts, 4 pants → 12 outfits (product).

### GATE Connection

First step in most problems.

### Traps

Using product when cases overlap — need sum or IEP.


## 3. Permutations P(n,r)

## Ordered selections

### Concept

Arrange r distinct positions from n objects without repetition: P(n,r)=n!/(n−r)!.

### Intuition

First slot n choices, second n−1, …

### Examples

P(5,3)=5·4·3=60.

### GATE Connection

Words, rankings, injective assignments.

### Traps

Dividing when order matters — use P not C.


## 4. Why C(n,r) = n!/(r!(n−r)!)

## Combinations as unordered selections

### Concept

**Combination** chooses r objects from n without regard to order.

### Intuition

Each r-set corresponds to r! orderings — divide permutations by r!.

### Definition

C(n,r) = n choose r = |{S⊆[n]: |S|=r}|.

### Derivation

Step 1 — Ordered selection: choose and arrange r from n → **P(n,r) = n!/(n−r)!**.

Step 2 — Each unordered r-set appears exactly **r!** times in the ordered list (all permutations of the set).

Step 3 — Therefore **C(n,r) = P(n,r)/r! = n!/(r!(n−r)!)**.

Step 4 — Sanity check n=5,r=2: P=20, each pair counted twice → C=10.

Step 5 — **Symmetry:** choosing r to keep equals choosing n−r to discard → C(n,r)=C(n,n−r).

### Examples

C(10,3)=10·9·8/(3·2·1)=120.

### GATE Connection

Binomial coefficients in probability and algebra.

### Traps

Using C when order matters; forgetting r! divisor.


## 5. Multiset permutations

## Identical objects

### Concept

n objects with multiplicities n₁,…,n_k: arrangements = n!/(n₁!…n_k!).

### Examples

MISSISSIPPI: 11!/(4!4!2!).

### GATE Connection

Letter rearrangement with repeats.

### Traps

Treating identical letters as distinct.


## 6. Combinations with repetition

## Stars and bars

### Concept

Choose r from n types, repetition OK, order irrelevant: **C(n+r−1,r)**.

### Derivation

r stars and n−1 bars → C(n+r−1, n−1).

### Examples

10 identical balls into 3 boxes: C(12,2)=66.

### GATE Connection

Distributions of identical objects.

### Traps

Using C(n,r) when repetition allowed.


## 7. Inclusion–Exclusion Principle

## Correct overcounting

### Concept

For finite sets: |A∪B|=|A|+|B|−|A∩B|. Three sets add triple intersection back.

### Intuition

Elements in both sets were counted twice — subtract overlap once.

### Derivation

Two sets: partition A into (A\B) and (A∩B); partition B into (B\A) and (A∩B).
Summing |A|+|B| counts (A∩B) twice → subtract |A∩B| once.

Three sets: add singles, subtract pairwise intersections, add |A∩B∩C|.

General: alternate sum over nonempty intersections of subfamilies.

Onto functions: |A_i|=maps missing i → IEP gives surjection count.

### Examples

|A|=40,|B|=35,|A∩B|=10 → |A∪B|=65.

### GATE Connection

At least one of properties; surjections; divisibility in [1,n].

### Traps

For three sets, forgetting to add triple intersection.


## 8. Pigeonhole principle

## Existence by counting

### Concept

If n+1 objects placed into n boxes, some box has ≥2 objects. General: N items, k holes ⇒ some hole has ≥⌈N/k⌉.

### Intuition

Too many pigeons force a crowded hole.

### Examples

13 birthdays in 12 months ⇒ two share a month.

### GATE Connection

Prove existence of duplicate remainder, same birthday, etc.

### Traps

Applying when objects/boxes not clearly defined.


## 9. Circular permutations

## Rotations equivalent

### Concept

n distinct around circle: (n−1)! (fix one object). Necklace with reflection: divide by 2 carefully.

### Examples

4 beads on bracelet distinct: (4−1)!/2 for reflection symmetry sometimes.

### GATE Connection

Seating around round table.

### Traps

Using n! instead of (n−1)!.


## 10. Derangements and advanced (awareness)

## Beyond basics

### Concept

Derangement !n counts permutations with no fixed point; GATE may mention formula !n = n!Σ(−1)^i/i!.

### GATE Connection

Usually smaller n enumerated.

### Traps

Over-memorizing — derive from IEP if needed.


---

Master `FORMULAS.md` for quick lookup during revision.
