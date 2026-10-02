# Bayes Theorem — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** P(A)=0.3,P(B|A)=0.8,P(B|A^c)=0.2. P(A|B)?

**2.** 2% defect,95% detect,4% false pos. P(D|+)?

**3.** 60% F1(1% def),40% F2(2% def). P(F1|def)?

**4.** Prior 0.01,like 0.9,marginal 0.05. Posterior?

**5.** P(A|B) vs P(B|A)?

---

## Level 2 — Standard GATE

**6.** Disease 1%, test 99% sensitive, 5% false positive. P(disease|positive)?

**7.** Three suppliers: S1(50%,2% def), S2(30%,3%), S3(20%,5%). P(S2|defective item)?

**8.** P(H)=0.6. P(E|H)=0.8,P(E|¬H)=0.3. P(H|E)?

**9.** Spam filter: P(spam)=0.4, P(word|spam)=0.5, P(word|¬spam)=0.1. P(spam|word)?

**10.** Prior P(θ)=0.2, likelihood P(D|θ)=0.9, P(D|¬θ)=0.1. P(θ|D)?

---

## Level 3 — Multi-Step

**11.** Two boxes: Box1 has 3W,1B; Box2 has 1W,3B. Pick box uniformly, draw white. P(Box1|white)?

**12.** Manufacturing: 70% auto (1% def), 30% manual (4% def). Item defective. P(auto)?

**13.** Email: 30% spam. Keyword in 60% spam, 10% ham. Email has keyword. P(spam)?

**14.** Three hypotheses H₁,H₂,H₃ with priors 0.5,0.3,0.2. Likelihoods given data: 0.8,0.5,0.2. Find posterior for H₁.

**15.** Sequential: test 1 positive (sens 0.95, fpr 0.1). Update prior 0.02. Posterior after test 1?

---

## Level 4 — Trap Questions

**16.** P(A|B)=P(B|A) always:
(a) true  (b) false

**17.** High test accuracy guarantees high P(disease|+):
(a) true  (b) false

**18.** Base rate neglect means ignoring:
(a) prior  (b) likelihood  (c) marginal  (d) posterior

**19.** P(A|B)P(B)=P(B|A)P(A) is:
(a) Bayes  (b) always true  (c) both  (d) neither

**20.** If prior is uniform over two hypotheses, posterior depends only on:
(a) likelihoods  (b) priors  (c) marginal  (d) (a) relative likelihoods

---

## Level 5 — Challenge

**21.** Rare disease 0.1%, test 99% sens, 1% fpr. P(disease|+)? Interpret paradox.

**22.** Naive Bayes: two independent words w₁,w₂. P(spam|w₁,w₂) from P(spam), P(wᵢ|spam), P(wᵢ|ham)?

**23.** Three tests independent given disease status. All positive. Prior 0.05, each test sens 0.9, fpr 0.05. Posterior?

**24.** Prove: P(A|B)≥P(A) iff P(B|A)≥P(B).

**25.** A and B independent. Can P(A|B∪C) be computed from Bayes without more info?

---

## Answers (Full Reasoning)

**A1.** P(B)=0.3·0.8+0.7·0.2=0.38. P(A|B)=0.24/0.38 ≈ **0.632**.

**A2.** P(+)=0.02·0.95+0.98·0.04=0.0582. P(D|+)=0.019/0.0582 ≈ **0.326**. Low prior (2%) keeps posterior modest despite 95% sensitivity — classic base-rate effect.

**A3.** P(def)=0.006+0.008=0.014. P(F1|def)=0.006/0.014 ≈ **0.429**.

**A4.** Posterior = 0.01·0.9/0.05 = **0.18**.

**A5.** **Different** — reverse conditioning; related by Bayes.

**A6.** P(+)=0.01·0.99+0.99·0.05=0.0594. P(D|+)=0.0099/0.0594 ≈ **0.167**.

**A7.** P(def)=0.01+0.009+0.01=0.029. P(S2|def)=0.009/0.029 ≈ **0.31**.

**A8.** P(E)=0.48+0.14=0.62. P(H|E)=0.48/0.62 ≈ **0.774**.

**A9.** P(word)=0.2+0.06=0.26. P(spam|word)=0.2/0.26 ≈ **0.769**.

**A10.** P(D)=0.18+0.08=0.26. P(θ|D)=0.18/0.26 ≈ **0.692**.

**A11.** P(W)=0.5·0.75+0.5·0.25=0.5. P(Box1|W)=0.375/0.5=**0.75**.

**A12.** P(def)=0.007+0.012=0.019. P(auto|def)=0.007/0.019 ≈ **0.368**.

**A13.** P(K)=0.18+0.07=0.25. P(spam|K)=0.18/0.25=**0.72**.

**A14.** P(D)=0.4+0.15+0.04=0.59. P(H₁|D)=0.4/0.59 ≈ **0.678**.

**A15.** P(+)=0.02·0.95+0.98·0.1=0.117. Posterior=0.019/0.117≈**0.162**.

**A16.** **(b) false** — unless P(A)=P(B).

**A17.** **(b) false** — low base rate yields low posterior even with good test.

**A18.** **(a) prior** — base rate neglect.

**A19.** **(c) both** — product rule + Bayes rearrangement.

**A20.** **(d) relative likelihoods** — posterior ∝ prior×likelihood.

**A21.** P(+)=0.001·0.99+0.999·0.01≈0.01098. P(D|+)≈0.00099/0.01098≈**0.09** (~9% despite 99% test). Base rate paradox.

**A22.** P(spam|w₁,w₂) ∝ P(spam)·P(w₁|spam)·P(w₂|spam); normalize with ham product.

**A23.** Likelihood ratio ≈ (0.9/0.05)³=5832. Posterior ≈ 0.05·5832/(0.05·5832+0.95) ≈ **0.997**.

**A24.** P(A|B)≥P(A) ⇔ P(A∩B)≥P(A)P(B) ⇔ P(B|A)≥P(B) — equivalent.

**A25.** **Need more information** — independence of A with B∪C not given.
