# Push-Down Automata — Shortcuts

## 1. Nested vs crossed
- **Solves:** “is there a PDA?”
- **Why:** LIFO stores one unmatched count. Nested pairs work; crossed pairs and three equal counts do not.
- **Example:** `{a^n b^m c^m d^n}` yes; `{a^n b^m c^n d^m}` no.
- **Trap:** `{a^m b^m c^{m+n}}` still has two agreements involving `m`.

## 2. Marker ⇒ deterministic
- **When:** a unique symbol announces “start popping”.
- **Why:** no guess.
- **Trap:** even-length palindromes without a marker are CFL but the natural PDA is NPDA.

## 3. Regular ⇒ DPDA
- **When:** 2025-style “accepted by a DPDA?”
- **Why:** finite control, stack unused.
- **Trap:** “any CFL” / “any decidable language”.
