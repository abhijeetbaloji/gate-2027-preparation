# Undecidability — Revision

- Decidable / RE-not-decidable / not RE. `L` decidable ⇔ both `L` and `L̄` RE.
- Reduction `A ≤ B`: undecidable `A` ⇒ undecidable `B`. The other direction is false.
- Rice: nontrivial property of `L(M)` is undecidable. “`M` has 5 states” is not Rice.
- **DFA / RE:** membership, empty, finite, equal, `Σ*` — all decidable.
- **CFG:** membership, empty, finite — decidable. Equal, `Σ*`, ambiguous, “is regular?”, intersection-empty — undecidable.
- **TM:** membership RE-not-decidable; emptiness not RE; non-emptiness RE-not-decidable; regularity / `Σ*` / equivalence — Rice.
- Fixed `k`-step properties of a TM (on every / some input) — decidable (finite window).
- Every NFA has a DPDA for the same language (always yes).
- CFG language is a decidable *set*. “`L(G)` is an undecidable language” is false.
- NP ⊆ decidable.
