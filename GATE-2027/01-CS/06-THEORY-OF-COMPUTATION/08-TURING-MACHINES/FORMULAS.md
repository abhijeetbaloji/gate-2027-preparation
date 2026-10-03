# Turing Machines — Rules

| Rule | When | Example | Limitation |
|---|---|---|---|
| Decides = accept `L` and reject `L̄`, always halt | definition | 2026 | “halts on all strings” is weaker |
| Recognizes = accept `L`, do not accept `L̄` | definition | `A_TM` | may loop on `L̄` |
| Both RE ⇒ decidable | dovetail | | |
| Multi-tape = one-tape as languages | always | | time changes |
| NTM = TM as RE languages | dovetail branches | | |
| CFL ⇒ decidable | CYK | | “`L(G)` undecidable” is false |
| `{a^p prime}` decidable | test primality of `\|w\|` | 2008 | not CFL |
