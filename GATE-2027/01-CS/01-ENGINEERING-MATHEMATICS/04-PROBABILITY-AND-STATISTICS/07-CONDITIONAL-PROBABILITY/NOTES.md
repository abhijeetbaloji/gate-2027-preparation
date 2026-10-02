# Conditional Probability — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What is conditioning in GATE?

**Conditional probability** answers: "Given that B occurred, what is the probability of A?" The sample space **shrinks** to outcomes consistent with B.

This topic leads directly to:
- **Multiplication rule** and joint probabilities
- **Law of total probability**
- **Bayes' theorem** (`08-BAYES-THEOREM/NOTES.md`)

---

## 2. Definition

**P(A|B) = P(A ∩ B) / P(B)**, provided **P(B) > 0**.

### Interpretation

Among all outcomes where B is true, the fraction that also satisfies A.

### Why divide by P(B)

Restricting to B re-normalizes probabilities so they sum to 1 within B.

### Worked Example 1

P(A)=0.4, P(B)=0.5, P(A∩B)=0.2.

P(A|B) = 0.2/0.5 = **0.4**.

P(B|A) = 0.2/0.4 = **0.5** — note P(A|B) ≠ P(B|A) in general.

---

## 3. Multiplication rule

From definition: **P(A ∩ B) = P(B) · P(A|B) = P(A) · P(B|A)**.

**Chain rule:** P(A₁∩A₂∩…∩A_n) = P(A₁)·P(A₂|A₁)·P(A₃|A₁∩A₂)···

### Worked Example 2 — Cards without replacement

P(1st ace) = 4/52. P(2nd ace | 1st ace) = **3/51**.

P(both aces) = (4/52)(3/51).

### Worked Example 3 — Two coins, given at least one H

Sample space restricted to {HH, HT, TH} (equally likely, 3 outcomes).

P(HH | ≥1H) = **1/3** (not 1/2 — classic trap).

---

## 4. Independence

A and B are **independent** iff:

**P(A∩B) = P(A)P(B)**

Equivalently (when P(B)>0): **P(A|B) = P(A)** — knowing B does not change P(A).

### Worked Example 4

Fair coin tosses: P(HH) = 1/4 = P(H)P(H) ⇒ independent tosses.

Drawing two cards **with replacement** ⇒ independent draws.

**Without replacement** ⇒ **not** independent.

---

## 5. Law of total probability

If {B₁, B₂, …, B_k} **partition** Ω (disjoint, union = all):

**P(A) = Σᵢ P(A|B_i) · P(B_i)**

### Derivation

A = ∪ᵢ (A ∩ B_i), disjoint union ⇒ P(A) = Σ P(A∩B_i) = Σ P(A|B_i)P(B_i).

### Worked Example 5

P(B₁)=0.6, P(A|B₁)=0.1; P(B₂)=0.4, P(A|B₂)=0.3.

P(A) = 0.6·0.1 + 0.4·0.3 = 0.06 + 0.12 = **0.18**.

---

## 6. Tree diagrams

Sequential conditioning is easiest on a tree:
- First branch: P(B_i)
- Second branch from B_i: P(A|B_i)
- Path probability = product along path

---

## 7. Conditional probability and RVs

P(X = k | Y = m) = P(X=k, Y=m) / P(Y=m).

Links to **joint PMF** in `01-RANDOM-VARIABLES/NOTES.md`.

---

## 8. Memoryless property (preview)

Exponential distribution: P(X > s+t | X > s) = P(X > t).

A conditional probability identity — see `03-EXPONENTIAL/NOTES.md`.

---

## 9. GATE Connection

- P(A|B) vs P(B|A) — **not equal** in general (prosecutor fallacy).
- Without replacement: update probabilities each draw.
- Total probability for mixture problems (factories, tests).
- Prerequisite for **Bayes' theorem**.
- "At least one" conditioning changes sample space.

---

## 10. Common traps

1. P(A|B) ≠ P(B|A).
2. Forgetting to restrict sample space when conditioning.
3. Treating "without replacement" as independent.
4. "At least one H" — three outcomes, not four.
5. Dividing by P(B) when P(B)=0 (undefined).

---

## 11. Summary checklist

- [ ] P(A|B) = P(A∩B)/P(B).
- [ ] Multiplication: P(A∩B) = P(B)P(A|B).
- [ ] Independence: P(A∩B) = P(A)P(B).
- [ ] Total probability: P(A) = Σ P(A|B_i)P(B_i).
- [ ] Draw tree for multi-step problems.
