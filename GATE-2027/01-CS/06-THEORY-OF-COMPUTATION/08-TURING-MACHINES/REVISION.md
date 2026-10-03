# Turing Machines — Revision

- Unbounded resource: the tape. Configuration = state + tape + head.
- **Recognizes `L`:** accept exactly `L`; may loop outside `L`.
- **Decides `L`:** halt on every input; accept `L` and reject the rest.
- `L` decidable ⇔ `L` and `L̄` both RE.
- Decidable closed under complement. RE not closed under complement.
- Both closed under ∪ and ∩.
- Multi-tape / NTM: same RE languages.
- `A_TM` RE, not decidable. `complement(A_TM)` not RE.
- Regular ⊂ CFL ⊂ decidable ⊂ RE.
- `{a^p | p prime}`: decidable, not CFL.
- `0*1*` regular; `{0^n 1^n}` CFL; `{0^n 1^n 0^n}` not CFL; TM decides all three.
