# Functions — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. What is a function in GATE?

## Functions as relations with unique outputs

### Concept

A **function** f: A → B assigns **exactly one** element of B to each element of A. Equivalently, f ⊆ A×B is a relation where every a ∈ A appears in exactly one pair (a, b).

### Intuition

Think of a vending machine: one button (input) cannot dispense two different snacks (outputs) on a single press.

### Definition

**Domain** A, **codomain** B, **image/range** {f(a) | a ∈ A} ⊆ B. Write f(a) = b or (a,b) ∈ f.

### GATE Connection

GATE counts functions, tests injectivity/surjectivity, compositions, inverses, and floor/ceiling.

### Traps

Confusing codomain with range — surjective means range **equals** codomain.


## 2. Injective, surjective, bijective

## Three classifications

### Concept

**Injective (1-1):** f(a₁)=f(a₂) ⇒ a₁=a₂. **Surjective (onto):** ∀b ∈ B ∃a ∈ A: f(a)=b. **Bijective:** both.

### Intuition

Injective: no two inputs share an output. Surjective: every output is hit. Bijective: perfect pairing.

### Properties

For **finite** sets: |A|≤|B| needed for injection; |A|≥|B| for surjection; |A|=|B| for bijection.

### Derivation

Pigeonhole: if |A|>|B|, cannot inject A→B. If |A|<|B|, cannot surject A→B (finite).

### Examples

f:ℤ→ℤ, f(n)=n²: not injective (f(2)=f(−2)); not surjective (no negative in range).

### GATE Connection

MSQs on definitions; disprove injectivity with one counterexample pair.

### Traps

On infinite sets, injective does not imply surjective or vice versa.


## 3. Counting all functions

## Product rule on the domain

### Concept

For finite A, B with |A|=m, |B|=n, total functions A→B: **n^m**.

### Intuition

Each of m inputs independently chooses among n outputs.

### Derivation

m independent choices → multiply n choices m times.

### Examples

|A|=3, |B|=2 → 2³ = **8** functions.

### GATE Connection

Most common counting formula in this topic.

### Traps

Using m^n instead of n^m — outputs are codomain, inputs are domain.


## 4. Counting injections and bijections

## Permutations of codomain elements

### Concept

Injections exist only if m≤n; count = **P(n,m) = n!/(n−m)!**. Bijections require m=n; count = **m! = n!**.

### Intuition

Injective: assign distinct outputs to inputs — first input n choices, second n−1, etc.

### Examples

|A|=4, |B|=6 → injections = 6·5·4·3 = **360**.

### GATE Connection

Often combined with 'how many one-to-one assignments'.

### Traps

Attempting injections when |A|>|B| — answer is **0**.


## 5. Counting surjections (onto functions)

## Inclusion–exclusion on missing outputs

### Concept

Onto functions from m-element domain to n-element codomain (m≥n): **Σ_{i=0}^{n} (−1)^i C(n,i)(n−i)^m**.

### Intuition

Start with all n^m maps; subtract maps missing at least one output; add back double exclusions.

### Derivation

Let A_i = maps missing output i. |∪A_i| via IEP → standard surjection formula.

### Examples

m=3, n=2: 2³ − 2·1³ = **6** onto maps.

### GATE Connection

Small m,n — compute directly; remember 2^m − 2 for n=2.

### Traps

Using permutation formula instead of IEP for onto maps.


## 6. Composition and inverse

## Order matters

### Concept

(g∘f)(a) = g(f(a)). **Inverse f⁻¹** exists iff f is bijective.

### Intuition

Composition: apply f first, then g. Inverse undoes f.

### Properties

(g∘f)⁻¹ = f⁻¹∘g⁻¹ when inverses exist. Injective ∘ injective = injective; surjective ∘ surjective = surjective.

### Examples

f(x)=x+1, g(x)=2x on ℝ. g∘f(x)=2x+2; f∘g(x)=2x+1.

### GATE Connection

Verify bijection by constructing inverse or checking both directions.

### Traps

Assuming (f∘g) = (g∘f) — composition is not commutative.


## 7. Finite self-maps

## Injective iff surjective on finite equal sets

### Concept

If f: A→A and |A| is finite, then f injective ⇔ f surjective ⇔ f bijective.

### Intuition

Cannot embed a finite set into a proper subset — pigeonhole on equal cardinalities.

### Derivation

If injective, |image|=|A| ⊆ codomain A ⇒ image=A ⇒ surjective.

### Examples

Any permutation of {1,…,n} is bijective.

### GATE Connection

Quick elimination in MCQs about functions on finite sets.

### Traps

Extending the equivalence to infinite sets — false (e.g. ℤ→ℤ, n↦2n).


## 8. Floor and ceiling

## Integer bounding functions

### Concept

⌊x⌋ = greatest integer ≤ x; ⌈x⌉ = smallest integer ≥ x.

### Intuition

Floor chops toward −∞; ceiling toward +∞.

### Properties

⌊x⌋ ≤ x < ⌊x⌋+1; ⌈x⌉−1 < x ≤ ⌈x⌉; ⌊−x⌋ = −⌈x⌉.

### Examples

⌊3.7⌋=3, ⌈3.7⌉=4, ⌊−2.3⌋=−3, ⌈−2.3⌉=−2.

### GATE Connection

Evaluate nested floor/ceiling; count integers in intervals.

### Traps

Floor of negative numbers — not truncation toward zero.


## 9. Modular arithmetic as functions

## Residue maps

### Concept

f(n)=n mod k maps ℤ to {0,1,…,k−1}. Not injective on ℤ; image size k.

### Intuition

Wrap numbers on a clock.

### Examples

n mod 3 has three outputs; preimage of 0 is multiples of 3.

### GATE Connection

Connects to groups ℤ_k later; counting residues in ranges.

### Traps

Confusing mod with division — remainder is in {0,…,k−1}.


## 10. Summary checklist

## Exam workflow

### Concept

1) Classify map type. 2) Check cardinalities. 3) Pick counting formula. 4) Verify with small example.

### GATE Connection

Cross-link: bijections ↔ permutations ↔ counting arrangements.

### Traps

Always state whether sets are finite and whether function is total.


---

See `FORMULAS.md`, `SHORTCUTS.md`, `PRACTICE.md`, `MISTAKES.md`.
