# LU Decomposition — Revision Sheet

Use **after** studying `NOTES.md`.

## Factorization

- **A = LU**: L unit lower triangular, U upper triangular.
- **PA = LU** when pivoting needed.

## L structure

- Diagonal all **1**.
- Below diagonal: multipliers ℓ_{ij} from elimination.

## U structure

- Upper triangular; diagonal = pivots.

## Solving Ax=b

1. Ly = b (forward)
2. Ux = y (back)

Factor once; cheap for many b.

## det(A)

det(A) = det(P) · ∏ u_{ii}; det(L)=1.

## Existence

- Needs nonzero pivots (no swap) OR use P.
- Singular A → zero on U diagonal.

## Traps

- L is not inverse of U.
- Do not confuse with Cholesky (A=LL^T, symmetric pos def).
- Zero pivot → pivot or fail.

## Mini example

[[2,1],[4,3]]=[[1,0],[2,1]][[2,1],[0,1]].
