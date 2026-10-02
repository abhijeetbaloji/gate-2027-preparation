# Propositional and First-Order Logic — Formulas

| Formula | Meaning | Variables | Conditions | Derivation (see NOTES) | Typical GATE use | Common mistake |
|---------|---------|-----------|------------|------------------------|------------------|----------------|
| P→Q ≡ ¬P∨Q | Implication rewrite | P,Q: propositions | Always | Material implication definition | CNF conversion, equivalence | Treating as "if and only if" |
| P↔Q ≡ (P→Q)∧(Q→P) | Biconditional split | P,Q | Always | Definition of iff | Equivalence proofs | Confusing with → |
| ¬(P→Q) ≡ P∧¬Q | Negated implication | P,Q | Always | ¬(¬P∨Q) = P∧¬Q | Simplify negations | Writing ¬P∧¬Q |
| P→Q ≡ ¬Q→¬P | Contrapositive | P,Q | Always | Both ≡ ¬P∨Q | Proof by contrapositive | Using converse Q→P |
| ¬(P∧Q) ≡ ¬P∨¬Q | De Morgan (AND) | P,Q | Always | Truth table | Push negation inward | Forgetting to flip ∧/∨ |
| ¬(P∨Q) ≡ ¬P∧¬Q | De Morgan (OR) | P,Q | Always | Truth table | CNF from negated formula | Leaving ∨ inside |
| (A∨L)∧(B∨¬L) ⊢ A∨B | Resolution | A,B: clauses, L: literal | CNF form | Case split on L | Refutation, SAT | Resolving non-complementary literals |
| ¬∀x P(x) ≡ ∃x ¬P(x) | Quantifier negation | x: variable, P: predicate | Valid in FOL | Logical equivalence | Negate universal statements | Forgetting to flip quantifier |
| ¬∃x P(x) ≡ ∀x ¬P(x) | Quantifier negation | x, P | FOL | Dual of above | Negate existential | Negating predicate only |
| Truth table rows = 2^n | Combinations | n: distinct variables | Finite PL | Each var T/F independently | Count assignments | Forgetting dependent vars |
