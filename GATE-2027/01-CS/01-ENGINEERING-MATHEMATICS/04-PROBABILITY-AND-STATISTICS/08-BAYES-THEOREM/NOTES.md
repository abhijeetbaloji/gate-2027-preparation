# Bayes' Theorem — Learning Notes

These notes are written for **first-time learning** or relearning. For a compressed sheet, use `REVISION.md` after you have studied this file.

---

## 1. What does Bayes do in GATE?

**Conditional probability** (`07-CONDITIONAL-PROBABILITY/NOTES.md`) gives P(A|B) from P(A∩B)/P(B). Often we know the **reverse** — P(B|A) (likelihood) — and want P(A|B) (posterior).

**Bayes' theorem inverts conditioning.** It is the capstone of the probability arc for GATE CS.

---

## 2. Bayes' formula

**P(A|B) = P(B|A) · P(A) / P(B)**

| Term | Name | Meaning |
|------|------|---------|
| P(A) | Prior | Belief before evidence B |
| P(B|A) | Likelihood | Probability of evidence if A true |
| P(B) | Evidence / marginal | Overall probability of observing B |
| P(A|B) | Posterior | Updated belief after seeing B |

---

## 3. Derivation

From definition: P(A|B) = P(A∩B)/P(B) and P(B|A) = P(A∩B)/P(A).

So P(A∩B) = P(B|A)P(A). Substitute:

**P(A|B) = P(B|A)P(A) / P(B)**. ∎

---

## 4. The denominator — law of total probability

P(B) is often computed via **partition** {A₁, …, A_k}:

**P(B) = Σᵢ P(B|A_i) · P(A_i)**

### Derivation of denominator

B = ∪ᵢ (B ∩ A_i), disjoint ⇒ P(B) = Σ P(B∩A_i) = Σ P(B|A_i)P(A_i).

### Worked Example 1 — Two hypotheses

P(A)=0.3, P(B|A)=0.8, P(B|Aᶜ)=0.2.

P(B) = 0.3·0.8 + 0.7·0.2 = 0.24 + 0.14 = **0.38**.

P(A|B) = 0.24/0.38 ≈ **0.632**.

---

## 5. Two-hypothesis form (medical test template)

**P(H|D) = P(D|H)P(H) / [P(D|H)P(H) + P(D|¬H)P(¬H)]**

- H = hypothesis (e.g. disease)
- D = positive test result
- P(D|¬H) = false positive rate

### Worked Example 2 — Medical test (base-rate neglect)

- 2% have disease: P(H) = 0.02
- Sensitivity P(D|H) = 0.95
- False positive P(D|¬H) = 0.04

P(D) = 0.02·0.95 + 0.98·0.04 = 0.019 + 0.0392 = **0.0582**

P(H|D) = 0.019/0.0582 ≈ **0.033** (about 3.3%, not 95%!)

### Why posterior is low

Disease is **rare** (low prior). Most positives come from false positives in the large healthy group.

---

## 6. Multi-category form (factories)

**P(F_i|defect) = P(defect|F_i)P(F_i) / Σⱼ P(defect|F_j)P(F_j)**

### Worked Example 3 — Two factories

- 60% from F1, defect rate 1%
- 40% from F2, defect rate 2%

P(defect) = 0.6·0.01 + 0.4·0.02 = 0.006 + 0.008 = **0.014**

P(F1|defect) = 0.006/0.014 ≈ **0.429**

---

## 7. Tree and table methods

**Tree:** multiply along paths for joint; sum paths for marginal P(B).

**Table:** rows = hypotheses, columns = evidence; fill joint P(H∩D) = P(D|H)P(H); normalize column for posterior.

Both prevent algebra errors under time pressure.

---

## 8. Odds form (optional)

Posterior odds = Prior odds × Likelihood ratio.

P(H|D)/P(¬H|D) = [P(H)/P(¬H)] · [P(D|H)/P(D|¬H)]

Useful for quick checks; GATE usually uses probability form.

---

## 9. GATE Connection

- Medical testing: sensitivity ≠ P(disease|positive).
- Factory/machine defect source identification.
- Spam filtering: P(spam|keywords).
- Always compute **P(B)** via total probability first.
- Classic trap: **base-rate neglect** and **prosecutor fallacy** P(A|B) vs P(B|A).

---

## 10. Common traps

1. Using P(B|A) as answer when question asks P(A|B).
2. Forgetting denominator P(B) — posterior won't sum correctly.
3. Ignoring low prior in medical tests.
4. Confusing sensitivity with PPV (positive predictive value).
5. Not using partition when multiple causes exist.

---

## 11. Summary checklist

- [ ] P(A|B) = P(B|A)P(A) / P(B).
- [ ] P(B) = Σ P(B|A_i)P(A_i) over partition.
- [ ] Draw tree or table for multi-step.
- [ ] Medical: rare disease ⇒ low posterior even with good test.
- [ ] Factory: defect given source uses Bayes with total P(defect).
