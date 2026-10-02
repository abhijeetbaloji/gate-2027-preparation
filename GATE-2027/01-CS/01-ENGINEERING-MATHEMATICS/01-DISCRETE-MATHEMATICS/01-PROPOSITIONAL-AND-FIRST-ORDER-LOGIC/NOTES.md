# Propositional and First-Order Logic

---

## 1. Propositions and Logical Connectives

### Concept
Propositional logic studies statements that are either **true (T)** or **false (F)** — no in-between. We combine them with connectives to build compound formulas.

### Intuition
Think of propositions as light switches (on/off). Connectives are wiring rules: AND needs both on, OR needs at least one on, NOT flips the switch.

### Formal Definition
- A **proposition** (or **atomic formula**) is a declarative statement with a definite truth value.
- **Propositional variables**: P, Q, R, …
- **Connectives**: ¬ (NOT), ∧ (AND), ∨ (OR), → (IMPLIES), ↔ (IFF)
- **Precedence** (highest to lowest): ¬ > ∧ > ∨ > → > ↔. Use parentheses when unsure.

### Important Properties
| Connective | True when | False when |
|------------|-----------|------------|
| ¬P | P is F | P is T |
| P∧Q | both T | at least one F |
| P∨Q | at least one T | both F |
| P→Q | P is F **or** Q is T | P is T and Q is F |
| P↔Q | same truth value | different truth values |

### Worked Example 1
**P** = "It rains", **Q** = "I carry an umbrella."
- P→Q is F only when it rains but I don't carry an umbrella.
- If it doesn't rain (P=F), P→Q is T regardless of Q.

### Worked Example 2
Evaluate (P→Q)∧(¬P∨R) when P=T, Q=F, R=T.
- P→Q = F; ¬P∨R = F∨T = T; result = F∧T = **F**.

### GATE Connection
Truth tables with 2–4 variables appear in almost every GATE CS paper. Know connective semantics cold.

### Common Trap
Treating P→Q as "P causes Q." It is a **truth-functional** statement: false only at (T,F).

### Concept Connections
Connectives link to **digital circuits** (AND/OR/NOT gates) and **Boolean algebra** in Digital Logic.

---

## 2. Implication — Deep Dive

### Concept
Implication P→Q is the most misunderstood connective in GATE. Master it completely.

### Intuition
"If P then Q" promises: whenever P holds, Q must hold. It says nothing when P is false.

### Formal Definition
Truth table for P→Q:

| P | Q | P→Q |
|---|---|-----|
| T | T | T |
| T | F | F |
| F | T | T |
| F | F | T |

**Equivalent form**: P→Q ≡ ¬P∨Q

### Important Properties — Related conditionals
Given P→Q:
| Name | Form | Equivalent to P→Q? |
|------|------|---------------------|
| **Converse** | Q→P | No |
| **Inverse** | ¬P→¬Q | No (but ≡ converse) |
| **Contrapositive** | ¬Q→¬P | **Yes** |

### Derivation/Proof
**Contrapositive equivalence**: P→Q ≡ ¬Q→¬P
- P→Q ≡ ¬P∨Q
- ¬Q→¬P ≡ ¬(¬Q)∨¬P ≡ Q∨¬P ≡ ¬P∨Q ✓

**Negation of implication**: ¬(P→Q) ≡ P∧¬Q (NOT ¬P∨¬Q!)

### Worked Example 1
"If n is even, then n² is even." (P→Q)
- Converse: "If n² is even, then n is even." — **False** (n=2 works, but n² even doesn't force n even? Actually n² even ⇒ n even. This converse happens to be true.)
- Better: "If I study, I pass." Converse "If I pass, I studied" — false.

### Worked Example 2
Simplify ¬(P→(Q→R)).
- ¬(P→(Q→R)) ≡ P∧¬(Q→R) ≡ P∧(Q∧¬R) ≡ **P∧Q∧¬R**

### GATE Connection
Questions ask: which is equivalent to given formula? Contrapositive and ¬(P→Q) ≡ P∧¬Q are favourites.

### Common Trap
Confusing converse with contrapositive. Only contrapositive is equivalent.

### Concept Connections
Implication underpins **program correctness** (precondition → postcondition) and **Hoare logic**.

---

## 3. Logical Equivalence, Tautology, Contradiction, Contingency

### Concept
Two formulas are **logically equivalent** if they have identical truth tables. A **tautology** is always T; **contradiction** always F; **contingency** otherwise.

### Intuition
Tautology = always-on circuit. Contradiction = short circuit. Contingency = depends on inputs.

### Formal Definition
- α ≡ β iff for every assignment, α and β have the same truth value.
- α is a **tautology** iff every row of its truth table is T.
- α is **satisfiable** iff at least one row is T.
- α is **valid** (in formula sense) = tautology.

### Important Properties — Key equivalences
| Law | Form |
|-----|------|
| De Morgan | ¬(P∧Q) ≡ ¬P∨¬Q; ¬(P∨Q) ≡ ¬P∧¬Q |
| Double negation | ¬¬P ≡ P |
| Commutative | P∧Q ≡ Q∧P; P∨Q ≡ Q∨P |
| Associative | (P∧Q)∧R ≡ P∧(Q∧R) |
| Distributive | P∧(Q∨R) ≡ (P∧Q)∨(P∧R) |
| Absorption | P∨(P∧Q) ≡ P |
| Identity | P∨F ≡ P; P∧T ≡ P |
| Domination | P∨T ≡ T; P∧F ≡ F |

### Worked Example 1
Show (P→Q)∨(Q→P) is a tautology.
- Only risky row: P=T,Q=F → (F)∨(T) = T ✓
- P=T,Q=T → T∨T = T; P=F,Q=F → T∨T = T; P=F,Q=T → T∨T = T. **Tautology.**

### Worked Example 2
Is P→(Q→P) a tautology?
- P→(Q→P) ≡ P→(¬Q∨P) ≡ ¬P∨¬Q∨P ≡ T∨¬Q ≡ **T**. Yes, tautology.

### GATE Connection
"Which of the following is a tautology?" — try the all-F assignment first to eliminate options.

### Common Trap
Confusing **valid formula** (tautology) with **valid argument** (conclusion true whenever premises true).

### Concept Connections
Equivalence checking connects to **Boolean minimization** and **K-map** simplification.

---

## 4. Normal Forms — CNF and DNF

### Concept
**DNF** (Disjunctive Normal Form): OR of ANDs (sum of products). **CNF** (Conjunctive Normal Form): AND of ORs (product of sums).

### Intuition
DNF: list ways formula can be true (each term is one satisfying row). CNF: list ways formula can be false.

### Formal Definition
- **Literal**: P or ¬P
- **Term (minterm)**: AND of literals
- **Clause (maxterm)**: OR of literals
- **DNF**: ∨ of terms; **CNF**: ∧ of clauses

### Derivation/Proof — Converting to CNF
Method: eliminate →, ↔; push ¬ inward (De Morgan); distribute ∨ over ∧.

Example: (P∨Q)→R
1. ¬(P∨Q)∨R
2. (¬P∧¬Q)∨R
3. **(¬P∨R)∧(¬Q∨R)** (distribute)

### Worked Example 1
Convert P∧(P→Q) to CNF.
- P∧(¬P∨Q) — already CNF (one clause after ∧).

### Worked Example 2
DNF of (P→Q)∧(P→¬Q)?
- Forces P→Q and P→¬Q, so if P then Q and ¬Q — impossible when P=T. When P=F: formula T.
- DNF: **¬P** (single term).

### GATE Connection
CNF conversion and "how many clauses" questions. Resolution requires CNF.

### Common Trap
CNF conversion can cause **exponential blow-up** — GATE usually keeps formulas small.

### Concept Connections
CNF links to **SAT solvers**; DNF to **canonical representation** of Boolean functions.

---

## 5. Inference Rules and Resolution

### Concept
An argument is **valid** if whenever all premises are T, the conclusion is T. **Resolution** is a refutation technique for CNF.

### Intuition
Resolution: if "P or A" and "not-P or B" are true, then "A or B" must be true.

### Formal Definition
- **Modus Ponens**: P, P→Q ⊢ Q
- **Modus Tollens**: ¬Q, P→Q ⊢ ¬P
- **Hypothetical Syllogism**: P→Q, Q→R ⊢ P→R
- **Resolution**: (A∨L) ∧ (B∨¬L) ⊢ (A∨B). Empty clause □ = contradiction.

### Worked Example 1
Premises: P→Q, Q→R, P. Prove R.
- Modus ponens: P, P→Q ⊢ Q. Then Q, Q→R ⊢ **R**.

### Worked Example 2
Resolve {P∨Q, ¬P∨R, ¬Q, ¬R}.
- P∨Q + ¬Q → P
- ¬P∨R + P → R
- R + ¬R → **□** (contradiction — unsatisfiable set).

### GATE Connection
One-step resolution and "is this argument valid?" using inference chains.

### Common Trap
Resolution requires **complementary literals** in CNF. Skolemization is beyond GATE scope.

### Concept Connections
Resolution is the basis of **automated theorem proving** and **Prolog** execution.

---

## 6. Validity vs Satisfiability

### Concept
- **Satisfiable**: ∃ assignment making formula T
- **Valid (tautology)**: ∀ assignments formula is T
- **Unsatisfiable**: no assignment makes it T (contradiction)

### Intuition
Satisfiable = at least one happy customer. Valid = every customer happy. Unsatisfiable = no one happy.

### Important Properties
| Status | Satisfiable? | Valid? |
|--------|-------------|--------|
| Tautology | Yes | Yes |
| Contingency | Yes | No |
| Contradiction | No | No |

### Worked Example 1
(P∨Q)∧(¬P∨Q)∧(¬Q): satisfiable?
- Third clause forces Q=F. First: P∨F → P=T. Second: ¬T∨F = F. **Unsatisfiable.**

### GATE Connection
"How many satisfying assignments?" — count truth table rows.

### Common Trap
Valid argument ≠ tautology. P, P→Q ⊢ Q is valid inference but (P∧(P→Q))→Q is the tautology form.

---

## 7. First-Order Logic (FOL)

### Concept
FOL extends propositional logic with **quantifiers** (∀, ∃), **predicates**, **constants**, and **functions**.

### Intuition
∀ = "for every", ∃ = "there exists." Predicates are statements about objects: P(x) = "x is prime."

### Formal Definition
- **∀x P(x)**: P holds for every x in domain.
- **∃x P(x)**: P holds for at least one x.
- **Scope**: quantifier binds the closest formula.
- **Free variable**: not bound by any quantifier. **Closed formula**: no free variables.

### Important Properties — Quantifier negation
| Negation | Equivalent |
|----------|------------|
| ¬∀x P(x) | ∃x ¬P(x) |
| ¬∃x P(x) | ∀x ¬P(x) |

### Important Properties — Order matters
- ∀x ∃y Loves(x,y): everyone loves someone (y can depend on x).
- ∃y ∀x Loves(x,y): someone is loved by everyone (same y for all x).
- **These are NOT equivalent.**

### Worked Example 1
Translate: "All students are smart."
- **∀x (Student(x) → Smart(x))** — NOT ∀x(Student(x)∧Smart(x)) which says everyone is a smart student.

### Worked Example 2
Negate: ∀x ∃y (x < y) over integers.
- ∃x ∀y ¬(x < y) ≡ **∃x ∀y (x ≥ y)** — "some x is maximal."

### GATE Connection
FOL translation, negation of quantified formulas, and "which is equivalent?"

### Common Trap
"All are P" uses → (∀x(P(x)→Q(x))); "Some are P" uses ∧ (∃x(P(x)∧Q(x))).

### Concept Connections
FOL is the language of **database queries** (SQL), **specification**, and **AI knowledge representation**.
