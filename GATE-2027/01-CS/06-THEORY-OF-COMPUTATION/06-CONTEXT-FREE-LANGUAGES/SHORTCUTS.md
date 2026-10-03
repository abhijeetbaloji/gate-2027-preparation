# Context-Free Languages — Shortcuts

## 1. Draw the matching
- Equalities that nest or sit in sequence → one stack. Crossed or two uses of the same count after it was consumed → not CFL.
- **Trap:** `c^{m+n}` with free `m,n` is one stack; `c^{m+n}` with `a^m b^m` is two uses of `m`.

## 2. Standard intersection
- To kill “closed under ∩”, quote `{a^n b^n c^m} ∩ {a^n b^m c^m}`.
- To kill “closed under complement”, quote De Morgan, or the complement of `{a^n b^n c^n}` (which *is* CFL) whose complement is not.

## 3. CFL ∩ regular is CFL, not “always regular”
- `{a^n b^n} ∩ a*b* = {a^n b^n}`.
