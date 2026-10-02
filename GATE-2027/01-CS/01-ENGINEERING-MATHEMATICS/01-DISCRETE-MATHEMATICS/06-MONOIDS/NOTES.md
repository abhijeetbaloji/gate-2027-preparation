# Monoids — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. Monoids in GATE

## Algebra with identity

### Concept

**Monoid (M,·,e):** set M, binary operation ·, **associative**, identity e with e·a=a·e=a.

### Intuition

You can multiply (or combine) things and there's a 'do nothing' element.

### GATE Connection

Verify axioms on small sets; distinguish semigroup vs monoid.

### Traps

Identity must be **two-sided** — rare trick questions with one-sided identity.


## 2. Semigroups

## Associativity alone

### Concept

**Semigroup:** (S,·) associative. Monoid adds identity.

### Examples

(ℕ,+) semigroup and monoid with 0.

### Traps

(ℤ,−) not a semigroup — not associative.


## 3. Closure

## Operation stays in M

### Concept

∀a,b∈M: a·b∈M.

### Examples

2×2 matrices under × — closed.

### GATE Connection

First check when testing algebraic structure.

### Traps

Operations on subset may leave set — not closed.


## 4. Commutative monoids

## ab = ba

### Concept

**Commutative monoid** if operation commutative.

### Examples

(ℕ,+), (ℕ,×), (P(A),∪) with ∅.

### Traps

Matrix multiplication monoid not commutative.


## 5. String monoid

## Free monoid

### Concept

Σ* strings over alphabet Σ with concatenation; identity ε.

### Intuition

Concatenation order matters.

### GATE Connection

Classic CS example linking to formal languages.

### Traps

Empty string is identity, not a letter.


## 6. Power set monoids

## Two standard examples

### Concept

(P(A),∪,∅) and (P(A),∩,A) both monoids.

### Examples

A={a,b}: ∪ identity ∅; ∩ identity {a,b}.

### GATE Connection

Pick correct identity for operation.

### Traps

Swapping identities between ∪ and ∩.


## 7. Submonoid

## Substructure

### Concept

N ⊆ M submonoid if closed under · and contains e.

### Examples

Even naturals under + — submonoid of (ℕ,+).

### GATE Connection

Verify closure + identity in subset.

### Traps

Subset closed under operation but missing identity of M.


## 8. Homomorphisms

## Structure-preserving maps

### Concept

f: M→M' monoid homomorphism if f(a·b)=f(a)·f'(b) and f(e)=e'.

### GATE Connection

Rare direct questions; understand for consistency.

### Traps

Forgetting f(e)=e' requirement.


## 9. Finite monoids

## Orders of elements

### Concept

In finite monoid, each element has finite **order** (smallest k>0 with a^k=e if exists).

### GATE Connection

Leads into groups when inverses exist.

### Traps

Not every monoid element has inverse — that's group level.


## 10. Summary

## Checklist

### Concept

Check closure → associativity → identity. Name the identity explicitly.

### GATE Connection

Often paired with groups in same MSQ.

### Traps

Calling structure group without verifying inverses.
