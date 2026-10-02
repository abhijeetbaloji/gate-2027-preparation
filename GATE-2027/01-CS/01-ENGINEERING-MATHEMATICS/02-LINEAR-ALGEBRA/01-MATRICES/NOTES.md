# Matrices

## Concept links
- **Matrices** are the objects; **determinants** measure whether a square matrix is invertible.
- **Linear systems** Ax = b are solved using matrix operations and rank.
- **Eigenvalues/eigenvectors** are defined via matrix–vector multiplication Av = λv.
- **LU decomposition** factors a matrix for efficient solving.

---

## 1. Basics

An **m×n matrix** A has m rows and n columns. Entry aᵢⱼ sits in row i, column j.

- **Square matrix**: m = n.
- **Identity Iₙ**: diagonal entries 1, all others 0. AI = IA = A.
- **Zero matrix O**: all entries 0.
- **Transpose Aᵀ**: (Aᵀ)ᵢⱼ = aⱼᵢ.

**Worked example.** If A = [[1,2],[3,4]], then Aᵀ = [[1,3],[2,4]].

---

## 2. Matrix operations

### Addition and scalar multiplication
Same dimensions required. (A + B)ᵢⱼ = aᵢⱼ + bᵢⱼ; (kA)ᵢⱼ = k·aᵢⱼ.

### Matrix product
If A is m×p and B is p×n, then AB is m×n with

**(AB)ᵢⱼ = Σₖ aᵢₖ bₖⱼ**

**Derivation idea.** Each entry is the dot product of row i of A with column j of B.

**Worked example.** A = [[1,2],[0,3]] (2×2), B = [[4],[5]] (2×1):

AB = [[1·4+2·5],[0·4+3·5]] = [[14],[15]].

### Key properties
- (AB)ᵀ = BᵀAᵀ (order reverses)
- (AB)⁻¹ = B⁻¹A⁻¹ when both inverses exist
- AB ≠ BA in general (non-commutative)

---

## 3. Special matrices

| Type | Condition | GATE note |
|------|-----------|-----------|
| Symmetric | Aᵀ = A | Real eigenvalues |
| Skew-symmetric | Aᵀ = −A | Diagonal must be 0 |
| Orthogonal | AᵀA = I | A⁻¹ = Aᵀ, det = ±1 |
| Idempotent | A² = A | Eigenvalues 0 or 1 |
| Nilpotent | Aᵏ = O for some k | All eigenvalues 0 |

**Worked example.** A both symmetric and skew-symmetric ⇒ Aᵀ = A = −A ⇒ 2A = O ⇒ **A = O**.

---

## 4. Inverse

For square A, **A⁻¹** exists iff det(A) ≠ 0 (links to determinants topic).

**2×2 formula:**

A = [[a,b],[c,d]], det = ad − bc ≠ 0

A⁻¹ = (1/det) [[d,−b],[−c,a]]

**Worked example.** A = [[2,1],[4,3]], det = 2 ⇒ A⁻¹ = [[3/2,−1/2], [−2,1]].

---

## 5. Rank and trace

- **Rank(A)**: number of linearly independent rows (= columns). rank ≤ min(m,n).
- **Trace tr(A)**: Σ aᵢᵢ (square only). tr(AB) = tr(BA) when product defined.

**Worked example.** A = [[1,2,3],[2,4,6]] — row 2 = 2×row 1 ⇒ rank = **1**.

---

## 6. Block matrices

For block-diagonal [[A,0],[0,B]], product and inverse work block-wise when blocks are compatible.

---

## GATE Connection

- **Dimension MCQs**: inner dimensions must match for AB.
- **Property questions**: test (AB)ᵀ, inverse order, symmetric/skew-symmetric.
- **Rank**: links directly to solution type of Ax = b (unique / infinite / none).
- **Trace**: sum of eigenvalues (eigenvalues topic).

## Common traps

- Confusing (AB)⁻¹ with A⁻¹B⁻¹ — correct order is **B⁻¹A⁻¹**.
- Assuming AB = BA.
- Forgetting zero matrix has **no** inverse.
- det(kA) = kⁿ det(A), not k·det(A).

---

## 7. Derivation: why (AB)ᵀ = BᵀAᵀ

Entry-wise: (AB)ᵀᵢⱼ = (AB)ⱼᵢ = Σₖ aⱼₖ bₖᵢ.

(BᵀAᵀ)ᵢⱼ = Σₖ (Bᵀ)ᵢₖ (Aᵀ)ₖⱼ = Σₖ bₖᵢ aⱼₖ — same sum.

**Worked example.** A=[[1,2],[0,3]], B=[[4,1],[5,0]].

(AB)ᵀ = [[14,15],[1,0]]; BᵀAᵀ = [[4,5],[1,0]][[1,0],[2,3]] = [[14,15],[1,0]]. ✓

---

## 8. Derivation: why tr(AB) = tr(BA)

tr(AB) = Σᵢ (AB)ᵢᵢ = Σᵢ Σⱼ aᵢⱼ bⱼᵢ = Σⱼ Σᵢ bⱼᵢ aᵢⱼ = tr(BA).

**GATE use:** Simplify expressions like tr(ABC) using cyclic permutations: tr(ABC) = tr(BCA) = tr(CAB) — but **not** tr(ACB) in general.

**Worked example.** A=[[1,2],[3,4]], B=[[0,1],[1,0]] → tr(AB)=tr(BA)=**5**.

---

## 9. Powers and nilpotent matrices

Aᵏ = A·A·…·A (k times). If A is diagonalizable (eigenvalues topic): Aᵏ = PΛᵏP⁻¹.

**Worked example.** A = [[1,1],[0,1]] (Jordan block): Aⁿ = [[1,n],[0,1]].

Nilpotent: Aᵏ = O for some k ⇒ all eigenvalues 0 ⇒ det(A)=0.

---

## 10. Graph connection (walk counting)

If A is adjacency matrix of a graph, (Aᵏ)ᵢⱼ = number of walks of length k from vertex i to j.

**GATE Connection:** Links discrete mathematics graphs to matrix powers.

---

## 11. Worked example — full matrix product chain

A (2×3), B (3×2), C (2×2): compute ABC dimensions.

AB is 2×2; (AB)C is 2×2. BA would be 3×3 — different product.

---

## 12. Concept map (study order)

```
01-MATRICES → 02-DETERMINANTS (det, singular)
            → 03-SYSTEMS (Ax=b, rank)
            → 04-EIGENVALUES (Av=λv)
            → 05-LU (A=LU)
```

Study `REVISION.md` after completing this file and linked topics.
