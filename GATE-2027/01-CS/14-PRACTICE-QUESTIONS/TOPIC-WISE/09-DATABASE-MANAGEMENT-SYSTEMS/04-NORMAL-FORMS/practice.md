# Normal Forms — Practice Questions

Original practice for GATE CS. These questions are not from any GATE paper. Attempt the questions before reading the solutions.

Attributes are atomic unless a question says otherwise, so every relation below is in 1NF. A functional dependency X → A is nontrivial when A is not in X. An attribute is prime when it belongs to at least one candidate key. The canonical cover is a minimal cover: single attribute on the right, no extraneous attribute on the left, and no redundant dependency.

## Level 1 — Conceptual

## Q1 — MCQ

A relation is in 1NF when

A. every attribute value is atomic
B. every non-prime attribute depends on the whole of every candidate key
C. it has no transitive dependency
D. every determinant is a superkey

---

## Q2 — MCQ

2NF forbids which situation?

A. A non-prime attribute functionally dependent on a proper subset of a candidate key
B. Any functional dependency whose right side is prime
C. Two candidate keys in the same relation
D. A dependency of a prime attribute on a proper subset of a candidate key

---

## Q3 — MCQ

A relation is in BCNF when, for every nontrivial functional dependency X → A that holds,

A. A is prime, even if X is not a superkey
B. X is a superkey
C. X contains exactly one attribute
D. the dependency is preserved by every decomposition

---

## Q4 — MSQ

Which inferences are valid? Select all that apply.

A. From A → B and A → C, infer A → BC
B. From A → B and B → C, infer A → C
C. From AB → C, infer A → C
D. From A → B, infer AC → B

---

## Level 2 — Standard GATE Style

## Q5 — MCQ

R(A, B, C, D) has F = {A → B, B → C, A → D}. What is the highest normal form of R?

A. 1NF but not 2NF
B. 2NF but not 3NF
C. 3NF but not BCNF
D. BCNF

---

## Q6 — MCQ

R(O, I, P, C, Y) has F = {OI → P, O → C, C → Y}. What is the highest normal form of R?

A. 1NF but not 2NF
B. 2NF but not 3NF
C. 3NF but not BCNF
D. BCNF

---

## Q7 — NAT

R(V, W, X) has F = {VW → X, X → W}. How many candidate keys does R have? ______

---

## Q8 — MCQ

R(J, K, L, M, N) has F = {J → K, KL → M, M → N, N → K}. The only candidate key is JL. Which dependency violates 2NF?

A. KL → M
B. M → N
C. J → K
D. N → K

---

## Q9 — NAT

F = {P → Q, Q → R, P → R, PS → Q} on attributes P, Q, R, S. How many dependencies are in a canonical cover of F? ______

---

## Q10 — MSQ

Which statements are true? Select all that apply.

A. A decomposition into two schemas is lossless if the intersection of the schemas is a superkey of at least one of them
B. BCNF decomposition by splitting on a violating dependency is lossless
C. Every BCNF decomposition obtained that way is dependency preserving
D. 3NF synthesis produces a decomposition that is both lossless and dependency preserving

---

## Level 3 — Multi-Step

## Q11 — NAT

R(A, B, C, D, E) has F = {A → B, C → D}, already a canonical cover. The only candidate key is ACE. How many schemas does 3NF synthesis emit? ______

---

## Q12 — MCQ

R(A, B, C, D) has F = {A → B, B → C, C → D} and is decomposed into AB, BC, and CD. Which description is correct?

A. The decomposition is lossy, and it does not preserve B → C
B. The decomposition is lossless, but it does not preserve B → C
C. The decomposition is lossless and dependency preserving, and each schema is in BCNF
D. The decomposition preserves every dependency, but the join of AB and CD is lossy, so the whole decomposition is lossy

---

## Q13 — NAT

R(W, X, Y, Z) has F = {W → X, X → Y, Y → W, WZ → Y}. How many candidate keys does R have? ______

---

## Q14 — MSQ

For the relation in Q13, which dependencies belong to a canonical cover of F? Select all that apply.

A. W → X
B. WZ → Y
C. X → Y
D. Y → W

---

## Level 4 — Tricky / Trap-Based

## Q15 — MCQ

R(V, W, X) has F = {VW → X, X → W}. It is decomposed into VX and WX. Which description is correct?

A. Lossless and dependency preserving
B. Lossy, but dependency preserving
C. Lossless, but not dependency preserving
D. Lossy, and not dependency preserving

---

## Q16 — MCQ

What is the highest normal form of the relation in Q15?

A. 1NF but not 2NF
B. 2NF but not 3NF
C. 3NF but not BCNF
D. BCNF

---

## Q17 — MSQ

R(A, B, C) has F = {A → B, B → A}. Which statements are true? Select all that apply.

A. The candidate keys are AC and BC
B. R is in 3NF
C. R is in BCNF
D. The decomposition into AB and AC is lossless and preserves both dependencies

---

## Level 5 — Challenge

## Q18 — NAT

F = {A → B, A → C, B → C, AC → D, D → A} on R(A, B, C, D). How many dependencies are in a canonical cover of F? ______

---

## Q19 — MCQ

What is the highest normal form of the relation in Q18?

A. 1NF but not 2NF
B. 2NF but not 3NF
C. 3NF but not BCNF
D. BCNF

---

## Q20 — MSQ

Again let R(V, W, X) have F = {VW → X, X → W}. Which statements are true? Select all that apply.

A. R is in 3NF and is not in BCNF
B. The decomposition into VX and WX is lossless
C. The decomposition into VX and WX preserves VW → X
D. The decomposition into VW and WX is lossless

---

## Answer Key

| Q | Type | Answer |
|---|------|--------|
| 1 | MCQ | A |
| 2 | MCQ | A |
| 3 | MCQ | B |
| 4 | MSQ | A, B, D |
| 5 | MCQ | B |
| 6 | MCQ | A |
| 7 | NAT | 2 |
| 8 | MCQ | C |
| 9 | NAT | 2 |
| 10 | MSQ | A, B, D |
| 11 | NAT | 3 |
| 12 | MCQ | C |
| 13 | NAT | 3 |
| 14 | MSQ | A, C, D |
| 15 | MCQ | C |
| 16 | MCQ | C |
| 17 | MSQ | A, B, D |
| 18 | NAT | 4 |
| 19 | MCQ | B |
| 20 | MSQ | A, B |

## Detailed Solutions

### Q1

Answer: A

1NF requires atomic attribute values: no repeating groups and no multivalued cells. B is the extra demand of 2NF. C is the idea behind 3NF. D is BCNF. A relation can be in 1NF and still have partial and transitive dependencies.

### Q2

Answer: A

2NF allows a non-prime attribute to depend on a candidate key, but not on a proper piece of one. That partial dependency is A.

B is not a violation. Prime attributes on the right side are how 3NF still permits some non-superkey determinants. C is harmless; several minimal keys are normal. D is too strong. A prime attribute may depend on part of a key without leaving 2NF. The classic separation is that 2NF talks about non-prime attributes. The dependency in D can still destroy BCNF, but it is not what 2NF forbids.

### Q3

Answer: B

BCNF ignores the prime-attribute escape used by 3NF. Every nontrivial left side must be a superkey. A is the reason a 3NF relation can fail BCNF. C is not required; a composite key is a legal determinant. D confuses a normal form of one schema with a property of a decomposition.

### Q4

Answer: A, B, D

A is the union rule. B is transitivity. D is augmentation, followed by the fact that C → C is trivial, so AC → BC and therefore AC → B.

C is false. AB → C does not imply A → C. A counter-model is the key AB of a relation in which A alone does not determine C. Augmentation adds attributes to the left side; it does not delete them.

### Q5

Answer: B

A⁺ = {A, B, C, D}, so A is a candidate key. No other attribute determines A, so it is the only one. The key is a single attribute, and a single-attribute key has no proper nonempty subset. There is no partial dependency, and R is in 2NF.

B → C holds, B is not a superkey (B⁺ = {B, C}), and C is not prime. R is not in 3NF, and therefore not in BCNF. The highest form is 2NF.

A would require a partial dependency, which a single-attribute key cannot have. C would be right only if every violating right side were prime. D fails because of B → C.

### Q6

Answer: A

OI⁺ contains P, then C by O → C, then Y by C → Y, so OI is a key. O alone yields {O, C, Y}, which misses I and P, so O is not a key. I alone determines nothing further. The only candidate key is OI. The prime attributes are O and I. P, C, and Y are non-prime.

O → C uses a proper subset of the candidate key and determines a non-prime attribute. That is a partial dependency, so R is not in 2NF. It is in 1NF by the atomic-attribute assumption. C → Y is a further problem, but the partial dependency is already enough to stop the climb at 1NF.

### Q7

Answer: 2

VW⁺ = {V, W, X} because VW → X. VX⁺ = {V, X, W} because X → W and then VW → X is already satisfied. So VW and VX are both keys.

V⁺ = {V}, W⁺ = {W}, and X⁺ = {X, W}. None of those is a key, and WX⁺ = {W, X} misses V. There is no third candidate key. The count is 2.

### Q8

Answer: C

The only candidate key is JL, which can be checked by closure: J → K, then KL → M, M → N, and N → K, so JL⁺ is the whole schema. No proper subset of JL works, because L alone determines nothing new and J alone misses L.

Prime attributes are only J and L. K is non-prime. J is a proper subset of the candidate key JL, and J → K, so this dependency violates 2NF.

KL is not a subset of JL, because K is not in the key. KL → M is a bad BCNF dependency, but it is not a partial dependency of a candidate key. M → N and N → K likewise have left sides that are not proper subsets of JL. They violate higher normal forms without being the 2NF violation.

### Q9

Answer: 2

Split nothing further; every right side is already a single attribute.

On PS → Q, S is extraneous: P → Q already, so P⁺ contains Q without using S. The dependency simplifies to P → Q, which is already present.

P → R is redundant. From P → Q and Q → R, P⁺ contains R even if P → R is deleted.

P → Q is not redundant: without it, P⁺ does not contain Q. Q → R is not redundant: without it, Q⁺ = {Q}.

A canonical cover is {P → Q, Q → R}. It contains 2 dependencies.

### Q10

Answer: A, B, D

If R is split into R1 and R2 and R1 ∩ R2 is a superkey of R1 or of R2, the join is lossless. That is the binary chase condition, so A holds. The BCNF algorithm always splits off a violating dependency X → A as a schema XA whose key is X, and the remaining schema still contains X, so the intersection X is a key of XA. Each split is lossless, and a sequence of lossless splits is lossless. B holds. 3NF synthesis builds one schema per left side of the canonical cover and adds a candidate key if none of those schemas contains one. The result preserves every dependency of the cover and is lossless. D holds.

C is false. Lossless BCNF decompositions need not preserve dependencies. Q15 is a concrete case.

### Q11

Answer: 3

Synthesis makes a schema for each dependency in the cover: AB from A → B, and CD from C → D. The candidate key is ACE. Neither AB nor CD contains A, C, and E together, so the algorithm adds a schema ACE.

The three schemas are AB, CD, and ACE. Omitting ACE leaves a lossy join, because nothing connects E to the rest and nothing connects the AB group to the CD group. ABCD would not be in 3NF anyway: inside ABCD the key would be AC, and A → B would still have a non-superkey left side and a non-prime right side.

### Q12

Answer: C

Join AB and BC first. Their intersection is B, and B → C, so B is a key of BC. The join to ABC is lossless. Then join CD. The intersection is C, and C → D, so C is a key of CD. The full decomposition is lossless.

Each dependency sits inside one schema: A → B in AB, B → C in BC, and C → D in CD. The decomposition is dependency preserving.

Each piece is in BCNF. In AB the nontrivial dependency is A → B and A is a key of AB. In BC, B is a key. In CD, C is a key.

A and B deny a dependency that is stored entirely inside BC. D claims the AB–CD join is the decomposition. That pairwise join would be lossy, because AB ∩ CD is empty, but the actual decomposition also contains BC, and the three-way join is lossless.

### Q13

Answer: 3

W, X, and Y determine each other: W → X → Y → W. None of them determines Z, because Z never appears on a right side. Adding Z produces a key.

- WZ⁺ contains X and Y, hence the whole schema.
- XZ⁺ contains Y and then W.
- YZ⁺ contains W and then X.

No subset of these is a key, because dropping Z loses Z, and Z alone determines nothing. The three candidate keys are WZ, XZ, and YZ.

### Q14

Answer: A, C, D

WZ → Y is redundant. W → X and X → Y already give W → Y, so WZ → Y follows by augmentation and does not belong in a canonical cover.

The cycle W → X, X → Y, Y → W has no redundant member. Deleting W → X leaves W unable to reach X. Deleting X → Y leaves X unable to reach Y. Deleting Y → W leaves Y unable to reach W. A canonical cover is {W → X, X → Y, Y → W}.

### Q15

Answer: C

The schemas are VX and WX, and their intersection is X. X → W, so X is a superkey of WX. The binary test says the join is lossless.

VW → X is not preserved. The preservation test starts from VW and may apply only dependencies that lie inside one schema. WX contains X → W. VX contains no nontrivial dependency implied by F: V never appears on a right side, and X does not determine V. Closing VW under those local pieces never produces X. The dependency VW → X, which needs V, W, and X together, is lost.

A would be true of many 3NF syntheses and is the trap here. B and D contradict the intersection test.

### Q16

Answer: C

From Q7, the candidate keys are VW and VX. Every attribute is prime: V and W occur in VW, and X occurs in VX.

X → W has a left side that is not a superkey, because X⁺ = {X, W} misses V. BCNF fails. 3NF still holds, because the right side W is prime. VW → X has a superkey on the left, so it offends neither form. The keys are composite, but neither dependency is a non-prime partial dependency, so 2NF holds as well. The highest form is 3NF.

A and B are the usual misreading of X → W as a 2NF or 3NF violation. It would violate 3NF only if W were non-prime. D ignores that X is not a superkey.

### Q17

Answer: A, B, D

A⁺ = {A, B} and B⁺ = {A, B}. Neither contains C. AC⁺ and BC⁺ contain everything, and no smaller set does: C⁺ = {C}, and AB⁺ = {A, B}. The candidate keys are AC and BC, so A is true. Every attribute is prime.

A → B and B → A both fail BCNF, because A and B are not superkeys. Both satisfy 3NF, because B and A are prime. R is in 3NF and not in BCNF. B is true and C is false.

AB ∩ AC = A, and A → B, so A is a key of AB and the join is lossless. Both dependencies use only A and B, so both are enforced inside AB. AC has no nontrivial dependency. D is true. This relation can be decomposed into dependency-preserving BCNF schemas; Q15 is the contrasting case, where that is not possible.

### Q18

Answer: 4

C is extraneous on the left of AC → D. A⁺ already contains C because A → C, and once C is present AC → D yields D. So AC → D simplifies to A → D, which really does follow from the original set: A → AC and AC → D.

A → C is then redundant, because A → B and B → C remain. A → B is not redundant: without it, A does not determine B. B → C is not redundant. A → D is not redundant: without it, A determines only A, B, and C. D → A is not redundant.

A canonical cover is {A → B, B → C, A → D, D → A}. It has 4 dependencies.

### Q19

Answer: B

From the cover, A⁺ contains B, C, and D, so A is a key. D → A, so D is a key as well. B⁺ = {B, C} and C⁺ = {C}, so there is no other candidate key. The prime attributes are A and D. B and C are non-prime.

Both candidate keys are single attributes, so there is no partial dependency and the relation is in 2NF. B → C has a left side that is not a superkey and a right side that is not prime, so the relation is not in 3NF. The highest form is 2NF.

The tempting error is to treat B → C as a partial dependency. B is not a subset of a candidate key in the required sense: the keys are A and D, and B is not a proper subset of either. Partial dependency is a 2NF idea. This violation is a 3NF violation.

### Q20

Answer: A, B

A and B are Q16 and the lossless half of Q15.

C is false: VW → X is exactly the dependency the preservation test fails to recover from VX and WX.

D is false. VW ∩ WX = W, and W⁺ = {W}. W is not a superkey of VW or of WX. The chase cannot build a full all-distinguished row. The decomposition is an attractive attempt to keep VW → X inside VW and X → W inside WX, but the join loses information. Dependency preservation without a lossless join is not an acceptable decomposition.
