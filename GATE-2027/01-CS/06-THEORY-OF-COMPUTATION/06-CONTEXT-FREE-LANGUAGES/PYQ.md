# Context-Free Languages — PYQ analysis

Mapping: [questions.md](../../13-PYQ-TOPIC-MAPPING/06-THEORY-OF-COMPUTATION/06-CONTEXT-FREE-LANGUAGES/questions.md).

| Year | Q# | Concept | On-topic? |
|---|---|---|---|
| 2025 | Q.45 CS-1 | `a^m b^m c^{m+n}` vs `a^m b^n c^{m+n}` | Yes |
| 2021 | Q.1 Set-1 | regular `L1`, CFL `L2`; which combination need not be CFL | Yes (extract garbled; PDF) |
| 2021 | Q.12 Set-2 | stored, options destroyed | Unreadable |
| 2017 | Q.4 Session 2 | CFL ∪, complement?, `L − R`, ∩ | Yes (extract damaged; standard fact: ∪ and `L−R` yes, ∩ no) |
| 2011 | Q.24 | `P` regular, `Q` CFL, `Q ⊆ P`; what is always regular | Yes |

**Patterns:** one-stack vs two-agreements; CFL vs regular closures.

**Traps:** `L − R` is CFL when `R` is regular; `R − L` need not be. Complement of `{a^n b^n}` *is* CFL.
