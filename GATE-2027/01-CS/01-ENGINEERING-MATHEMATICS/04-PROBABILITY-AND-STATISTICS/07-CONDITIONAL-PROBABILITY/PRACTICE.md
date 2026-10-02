# Conditional Probability — GATE-STYLE PRACTICE

**These are practice questions only — not GATE PYQs.**

---

## Level 1 — Concept Check

**1.** P(A)=0.4,P(B)=0.5,P(A∩B)=0.2. P(A|B)?

**2.** P(HH|≥1H) two coins?

**3.** P(A|B)=P(A). Independent?

**4.** Two aces without replacement?

**5.** P(D)=0.01,P(+|D)=0.99. P(D|+)=?

---

## Level 2 — Standard GATE

**6.** P(A)=0.6,P(B)=0.5,P(A∪B)=0.8. Find P(A|B) and P(B|A).

**7.** Deck: P(King|Red card)?

**8.** Two dice. P(sum=7 | first die is 4)?

**9.** P(A|B)=0.7, P(B)=0.4. Find P(A∩B).

**10.** Events mutually exclusive with P(A)=0.3,P(B)=0.4. P(A|B)?

---

## Level 3 — Multi-Step

**11.** Box: 3 red, 2 blue. Draw 2 without replacement. P(both red | first red)?

**12.** P(Rain)=0.3, P(Wet|Rain)=0.9, P(Wet|¬Rain)=0.1. Find P(Rain|Wet).

**13.** Three cards drawn without replacement from standard deck. P(all hearts | first is heart)?

**14.** Factory: Machine A 60% output, 2% defect; B 40%, 3% defect. P(defect|from A)?

**15.** P(A)=0.5,P(B)=0.6,P(C)=0.4,P(A∩B)=0.3,P(A∩C)=0.2,P(B∩C)=0.25,P(A∩B∩C)=0.1. Find P(A|B∩C).

---

## Level 4 — Trap Questions

**16.** P(A|B)=P(B|A) implies A and B are independent:
(a) true  (b) false

**17.** If P(A|B)=1, then B⊆A:
(a) always  (b) only if P(B)>0  (c) false

**18.** P(A|B)+P(A^c|B) equals:
(a) 1  (b) P(A)  (c) P(B)  (d) 0

**19.** For mutually exclusive A,B with P(B)>0:
(a) P(A|B)=0  (b) P(A|B)=P(A)  (c) undefined

**20.** P(A∩B)=P(A)P(B) is equivalent to:
(a) P(A|B)=P(A)  (b) P(B|A)=P(B)  (c) both  (d) neither

---

## Level 5 — Challenge

**21.** Monty Hall: 3 doors, switch vs stay — P(win|switch)?

**22.** Family with 2 children. Given at least one boy, P(both boys)? (Assume equally likely.)

**23.** Urn: 5 white, 3 black. Add 2 white, draw 1. P(white | added white)? Compare to P(white) before.

**24.** Prove P(A|B)P(B)+P(A|B^c)P(B^c)=P(A) (law of total probability).

**25.** P(A|B∪C) in terms of P(A|B), P(A|C) — can you simplify without extra info?

---

## Answers (Full Reasoning)

**A1.** P(A|B)=0.2/0.5 = **0.4**.

**A2.** Outcomes with ≥1H: HH,HT,TH. Only HH has HH → **1/3**.

**A3.** **Yes** — P(A|B)=P(A) is definition of independence (when P(B)>0).

**A4.** (4/52)(3/51) = **1/221** for first two aces (ordered) or C(4,2)/C(52,2) for unordered pair.

**A5.** **Cannot determine** without P(+) — needs Bayes/total probability.

**A6.** P(A∩B)=0.8−0.6−0.5+... = 0.1. P(A|B)=0.1/0.5=**0.2**. P(B|A)=0.1/0.6≈**0.167**.

**A7.** 2 Kings in 26 red → **2/26 = 1/13**.

**A8.** Given first=4, second must be 3 → **1/6**.

**A9.** P(A∩B)=0.7·0.4 = **0.28**.

**A10.** **0** — cannot occur together.

**A11.** After first red, 2 red left of 4: P(second red|first red)=**1/2**.

**A12.** P(Wet)=0.3·0.9+0.7·0.1=0.34. P(Rain|Wet)=0.27/0.34≈**0.794**.

**A13.** Given first heart, 12 hearts left in 51 cards; need 2 more hearts: C(12,2)/C(51,2)≈**0.055**.

**A14.** **2%** by statement (defect rate from A).

**A15.** P(A|B∩C)=P(A∩B∩C)/P(B∩C)=0.1/0.25=**0.4**.

**A16.** **(b) false** — symmetry of conditioning ≠ independence (e.g. P(A)=P(B)).

**A17.** **(b)** — if P(B)>0 and P(A|B)=1, then B⊆A.

**A18.** **(a) 1** — partition of sample space given B.

**A19.** **(a) P(A|B)=0** when mutually exclusive and P(B)>0.

**A20.** **(c) both** — equivalent definitions of independence.

**A21.** Switch wins with prob **2/3** (standard Monty Hall).

**A22.** BB,BG,GB,GG equally likely given ≥1 boy excludes GG. BB probability = **1/3**.

**A23.** After adding: 7W,3B. P(W)=**7/10**. Before: 5/8=0.625. Conditioning on "added white" is certain → P(W|added)=**7/10**.

**A24.** Expand: P(A∩B)+P(A∩B^c)=P(A) — partition law.

**A25.** **Cannot simplify** in general without knowing overlap structure of B and C.
