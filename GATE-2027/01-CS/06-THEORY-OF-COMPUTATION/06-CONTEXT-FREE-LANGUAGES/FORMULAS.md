# Context-Free Languages — Rules

| Rule | When | Example | Limitation |
|---|---|---|---|
| ∪, ·, * closed | CFLs | `S → S1 \| S2` | |
| ∩ regular closed | `L` CFL, `R` regular | PDA × DFA | intersection is CFL, not always regular |
| `L − R` closed | `R` regular | `L ∩ R̄` | `R − L` need not be CFL |
| ∩ of two CFLs | **not** closed | `{a^n b^n c^n}` | |
| complement | **not** closed | De Morgan + ∪ would close ∩ | a particular complement may still be CFL |
| `{a^n b^n c^m d^m}` CFL | sequential pairs | | `{a^n b^m c^n d^m}` is not |
| `{a^m b^n c^{m+n}}` CFL | one sum | 2025 `L2` | `{a^m b^m c^{m+n}}` is not (`L1`) |
