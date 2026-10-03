# Push-Down Automata — Rules

| Rule | When | Example | Limitation |
|---|---|---|---|
| NPDA final-state = CFL | family, not one machine | `{a^n b^n}` | the two modes of *one* PDA can differ |
| NPDA empty-stack = CFL | family | | conversions can break determinism |
| Regular ⊂ DCFL | ignore the stack | any DFA | DCFL ⊂ CFL is proper |
| `{w c w^R}` DCFL | centre marker | | without `c`, guess the middle |
| Empty-stack DPDA ⇒ prefix-free | determinism + empty stack | not `a*` | final-state DPDA can accept `a*` |
| PDA × DFA | CFL ∩ regular | | two PDAs: intersection need not be CFL |
