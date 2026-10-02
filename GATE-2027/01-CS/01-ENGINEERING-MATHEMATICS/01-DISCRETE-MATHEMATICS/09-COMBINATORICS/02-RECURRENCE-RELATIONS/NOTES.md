# Recurrence Relations — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---


## 1. Recurrences in GATE

## Discrete dynamical equations

### Concept

**Recurrence** defines sequence {a_n} by relation among terms, e.g. a_n = c₁a_{n−1}+c₂a_{n−2}.

### Intuition

Each term built from previous ones — like Fibonacci.

### GATE Connection

Solve linear recurrences; find closed form; asymptotic order.

### Traps

Need base cases — relation alone underdetermines sequence.


## 2. Linear homogeneous recurrences

## Constant coefficients

### Concept

a_n + c₁a_{n−1}+…+c_ka_{n−k}=0. Characteristic polynomial r^k+c₁r^{k−1}+…+c_k=0.

### Derivation

Try a_n=r^n → characteristic equation; roots give basis.

### Examples

Fibonacci: a_n=a_{n−1}+a_{n−2} → roots φ,ψ.

### GATE Connection

Distinct real roots → C₁r₁^n+C₂r₂^n.

### Traps

Repeated roots need n^j r^n terms.


## 3. Nonhomogeneous terms

## Forcing functions

### Concept

a_n = c₁a_{n−1}+f(n). Solve homogeneous part + particular solution.

### Examples

a_n=2a_{n−1}+1 — particular constant.

### GATE Connection

Guess particular based on f(n) form.

### Traps

Particular must satisfy full recurrence.


## 4. Initial conditions

## Unique solution

### Concept

k initial values needed for order-k recurrence.

### GATE Connection

Plug into general solution for constants.

### Traps

Using wrong number of constants.


## 5. Master theorem style (divide and conquer)

## Algorithm recurrences

### Concept

T(n)=aT(n/b)+f(n) — know standard cases for O(n^log_b a) vs f(n).

### GATE Connection

Connects to algorithms subject.

### Traps

Regularity condition in case 3 — GATE usually states answer.


## 6. Generating function link

## Algebraic encoding

### Concept

G(x)=Σ a_n x^n turns recurrence into equation in x.

### GATE Connection

See `03-GENERATING-FUNCTIONS`.

### Traps

Sign errors in shifting indices.


## 7. Asymptotic growth

## Dominant root

### Concept

Closed form dominated by largest root magnitude; multiplicity affects polynomial factor.

### Examples

Fibonacci ~ φ^n/√5.

### GATE Connection

Compare growth rates.

### Traps

Ignoring multiplicity when roots equal.


## 8. Systems and substitutions

## Transform recurrences

### Concept

Substitute b_n=n!a_n or b_n=a_n+c to simplify.

### GATE Connection

Telescoping style tricks.

### Traps

Substitution must be invertible.


## 9. Tower and nonlinear (awareness)

## Harder forms

### Concept

a_n=a_{n−1}^2 etc. rarely closed form — small n computed.

### GATE Connection

Enumerate if n small.

### Traps

Assuming linear method works.


## 10. Summary

## Workflow

### Concept

Homogeneous solution + particular + fit ICs.

### GATE Connection

Characteristic equation is default tool.

### Traps

Check distinct vs repeated roots.
