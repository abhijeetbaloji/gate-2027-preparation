# Generating Functions — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. Generating functions in GATE

## Formal power series

### Concept

**OGF** G(x)=Σ a_n x^n encodes sequence {a_n}.

### Intuition

Carry sequence as coefficients; algebra solves counting.

### GATE Connection

Count selections, compositions; solve recurrences.

### Traps

Convergence not central — formal series.


## 2. Building blocks

## Standard series

### Concept

1/(1−x)=Σ x^n. (1+x)^n binomial coefficients. 1/(1−x)^k for combinations with repetition.

### Examples

Σ C(n+k−1,k−1)x^n = 1/(1−x)^k.

### GATE Connection

Pick correct template.

### Traps

Off-by-one in exponent shifts.


## 3. Convolution

## Product of series

### Concept

(Σ a_n x^n)(Σ b_n x^n)=Σ c_n x^n with c_n=Σ_{k=0}^n a_k b_{n−k}.

### Intuition

Choose k from first structure, n−k from second.

### GATE Connection

Split counting into independent parts.

### Traps

Index reversal confusion.


## 4. Exponential generating functions

## EGF

### Concept

Â(x)=Σ a_n x^n/n! — useful for labeled structures.

### GATE Connection

Occasional advanced MCQ.

### Traps

Forgetting n! in denominator.


## 5. Recurrences via generating functions

## Shift identities

### Concept

a_n = a_{n−1}+a_{n−2} ⟺ G(x)(1−x−x²)=base terms.

### Derivation

Multiply recurrence by x^n and sum.

### GATE Connection

Fibonacci closed form route.

### Traps

Missing initial term contributions.


## 6. Partitions and compositions

## Integer partitions

### Concept

Product Π 1/(1−x^k) for partitions into parts k.

### GATE Connection

Coins/weights problems.

### Traps

Order matters in compositions not partitions.


## 7. Solving for coefficients

## Partial fractions

### Concept

Decompose rational G(x) to extract a_n.

### GATE Connection

After setting up equation.

### Traps

Algebra errors in decomposition.


## 8. Catalan numbers (awareness)

## Classic sequence

### Concept

C(x)=1/(1−xC(x)) → C_n = C(2n,n)/(n+1).

### GATE Connection

BST count, balanced parentheses.

### Traps

Memorize small values: 1,1,2,5,14.


## 9. Applications table

## When to use OGF

### Concept

Unlabeled counting with size parameter; distributing identical objects with generating series.

### GATE Connection

Link stars-and-bars to 1/(1−x)^k.

### Traps

Using OGF where EGF needed for labeled.


## 10. Summary

## Workflow

### Concept

Model → equation for G(x) → expand series → read coefficient.

### GATE Connection

Practice index shifting.

### Traps

Sign in (1−x) factors.
