# Propositional and First-Order Logic — Quick Revision

## Connectives
- ¬ > ∧ > ∨ > → > ↔ precedence
- P→Q: F **only** at (T,F); ≡ ¬P∨Q
- P↔Q ≡ (P→Q)∧(Q→P)

## Implication family
- Contrapositive ¬Q→¬P ≡ P→Q ✓
- Converse Q→P ✗; Inverse ¬P→¬Q ✗
- ¬(P→Q) ≡ **P∧¬Q**

## Key equivalences
- De Morgan: ¬(P∧Q) ≡ ¬P∨¬Q
- P→Q ≡ ¬P∨Q; ¬(P→Q) ≡ P∧¬Q

## Normal forms
- DNF = ∨ of ∧s (minterms); CNF = ∧ of ∨s (clauses)
- CNF for resolution; convert → first

## Inference
- MP: P, P→Q ⊢ Q | MT: ¬Q, P→Q ⊢ ¬P
- Resolution: (A∨L)∧(B∨¬L) ⊢ A∨B; □ = unsat

## Validity / SAT
- Tautology = always T; Satisfiable = some T row
- Valid argument ≠ tautology (unless implication of premises→conclusion is tautology)

## FOL
- ¬∀x P ≡ ∃x ¬P; ¬∃x P ≡ ∀x ¬P
- "All P are Q": ∀x(P(x)→Q(x))
- "Some P are Q": ∃x(P(x)∧Q(x))
- ∀x∃y ≠ ∃y∀x

## Traps
- P→Q is not causation
- Truth table size = 2^n
- Scope: quantifier binds closest formula only
