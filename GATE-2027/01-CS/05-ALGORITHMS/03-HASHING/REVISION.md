# Hashing — Revision

## Model

- `α = n/m`. Simple uniform hashing unless the question says universal or gives a fixed `h`.
- Worst-case search is `Θ(n)` if the hash is fixed and every key collides.
- Expected `Θ(1)` requires `α = Θ(1)`.

## Formulas

| Method | Unsuccessful | Successful | Notes |
|--------|--------------|------------|-------|
| Chaining | `Θ(1+α)` | `Θ(1+α/2)` exams | Allows `α > 1`. Space `Θ(n+m)` |
| Open, uniform probing | `1/(1−α)` | `(1/α) ln(1/(1−α))` | Needs `α < 1`. Double hashing approximates this |
| Linear probing | longer than the ideal, because of primary clustering | | Sequence `(h + i) mod m` visits every slot |
| Direct address | `Θ(1)` worst | `Θ(1)` | Space `Θ(|U|)`, no collisions |

## Probes

- Linear: primary clustering.
- Quadratic: secondary clustering; may not visit every slot.
- Double: `(h1 + i h2) mod m`, `h2` coprime to `m`.

## Delete and grow

- Chaining: unlink.
- Open addressing: tombstone. Empty slot means “stop searching”.
- Rehash when `m` changes. Doubling gives expected amortised `O(1)` insert, not worst-case `O(1)`.

## Other facts

- Universal family: any fixed pair collides with probability `≤ 1/m`.
- Birthday: collisions likely by `n ≈ √(2 m ln 2)`.
- `α = 1` does not mean one key per slot.
- Perfect hashing: static set, worst-case `O(1)` search after build.
- Ranges and successors: use a tree or a sorted array.

## Traps

- `1/(1−α)` on a chained table.
- NULL delete in open addressing.
- Linear probing quoted with the uniform-probe formula without a warning.
- Hashing used for a range query.
