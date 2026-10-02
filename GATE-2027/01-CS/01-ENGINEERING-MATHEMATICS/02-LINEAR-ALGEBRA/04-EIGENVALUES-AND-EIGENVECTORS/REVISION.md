# Eigenvalues and Eigenvectors — Revision Sheet

Use **after** studying `NOTES.md`.

## Definition

Av = λv, v≠0 → λ eigenvalue, v eigenvector.

## Characteristic equation

det(A − λI) = 0

## Trace and determinant

- Σ λᵢ = **tr(A)**
- Π λᵢ = **det(A)**

## Multiplicity

- Algebraic: power in char poly
- Geometric: dim eigenspace = n − rank(A−λI)
- Diagonalizable ⟺ geometric = algebraic for all λ

## Key theorems

- Distinct λ → independent eigenvectors
- Symmetric real A → real λ, orthogonal eigenvectors, A=QΛQ^T

## Powers

A^k v = λ^k v; A^k = PΛ^k P^{-1} if diagonalizable

## Special

- λ=0 ⟺ singular
- det(A−cI) = product of (λᵢ−c)

## Traps

- Algebraic ≠ geometric always
- Non-symmetric may have complex λ (real matrix can still)
- Normalize eigenvectors only when orthogonality needed

## Mini example

λ=1,2,3 → tr=6, det=6.
