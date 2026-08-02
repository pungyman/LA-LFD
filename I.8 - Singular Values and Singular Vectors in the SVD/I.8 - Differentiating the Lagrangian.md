---
title: Differentiating the Lagrangian
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-07-30
tags: [type/topic, status/seedling, part/1, section/I-8, svd, lagrange-multipliers, matrix-calculus, quadratic-forms, rayleigh-quotient, spectral-norm, submatrices]
related: ["[[Home]]", "[[I.8 - Forward Reverse and the Block Matrix for SVD]]", "[[I.7 - Diagonal Entries and Eigenvalue Bounds]]"]
sources: ["[[2026-07-30 Differentiating Lagrangian for Quadratic Maximization]]"]
---

# Differentiating the Lagrangian

## Summary

Maximizing $x^T S x$ on the unit sphere, via a Lagrange multiplier, collapses straight into the eigenvalue equation $Sx = \lambda x$. The only calculus required is $\nabla(x^T x) = 2x$ and $\nabla(x^T S x) = 2Sx$ for symmetric $S$. The same section of Strang proves that chopping rows and columns cannot increase the spectral norm.

## Key Results

### The Lagrangian

To maximize $x^T S x$ subject to $x^T x = 1$:

$$
L(x, \lambda) = x^T S x - \lambda(x^T x - 1).
$$

Critical points satisfy $\nabla_x L = 0$.

### Gradients of the two pieces

$$
\nabla(x^T x) = 2x.
$$

For general square $S$,

$$
\nabla(x^T S x) = Sx + S^T x.
$$

When $S$ is symmetric ($S = S^T$), this collapses to $2Sx$. In the SVD / Rayleigh setting one always has symmetry — typically $S = A^T A$.

### Critical points are eigenpairs

$$
\nabla L = 2Sx - 2\lambda x = 0 \implies Sx = \lambda x.
$$

The multiplier *is* the eigenvalue. Evaluating $x^T S x$ at a unit eigenvector recovers $\lambda$, so the maximum on the sphere is $\lambda_{\max}$.

### Submatrices cannot increase the spectral norm

If $B$ is obtained from $A$ by deleting rows and columns, then $\|B\| \le \|A\|$, where $\|\cdot\|$ is the spectral norm (largest singular value). Strang's chain:

$$
\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|.
$$

- Removing columns of $A$ to get $C$ restricts the input space (some coordinates forced to zero), so the max stretch cannot rise: $\|C\| \le \|A\|$.
- Transposing leaves singular values unchanged: $\|C^T\| = \|C\|$.
- Removing columns of $C^T$ (i.e. rows of $C$) restricts inputs again: $\|B^T\| \le \|C^T\|$.

## Intuition

### Building $x^T S x$ without memorizing double sums

In $2 \times 2$, multiply right to left:

$$
Sx = \begin{bmatrix} S_{11}x_1 + S_{12}x_2 \\ S_{21}x_1 + S_{22}x_2 \end{bmatrix},
$$

$$
x^T(Sx) = S_{11}x_1^2 + S_{12}x_1 x_2 + S_{21}x_2 x_1 + S_{22}x_2^2.
$$

A double sum $\sum_i \sum_j x_i S_{ij} x_j$ is just that nested loop written compactly. Differentiating the polynomial in $x_1$ term by term yields the first components of $Sx$ and $S^T x$; symmetry identifies them.

### Why deleting columns cannot raise the norm

$A$ has $n$ input "dials." Forming a submatrix by dropping columns locks some dials at zero. A restricted search for the longest output cannot beat an unrestricted search. Deleting rows truncates the output vector, which can only shorten it.

## Worked Problems

### Problem 9: from $L$ to $Sx = \lambda x$

Differentiate, set $\nabla L = 0$, cancel the factor of $2$. The blank in the book is the eigen-equation itself.

**Takeaway:** the Rayleigh maximization problem and the eigenvalue problem are the same critical-point condition written twice.

### Problem 10: the submatrix chain

Read $\|A\|$ as $\sigma_1(A)$, the maximum of $\|Ax\|/\|x\|$. Each step of $\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|$ is either "transpose preserves $\sigma_1$" or "fewer free input coordinates cannot increase the max."

**Takeaway:** submatrix singular values are dominated by parent singular values — a fact used constantly in perturbation and compression arguments.

## Pitfalls

- **$\nabla(x^T S x) = 2Sx$ needs symmetry.** Without it the answer is $Sx + S^T x$; only the symmetric part of $S$ contributes to the quadratic form anyway.
- **Lagrange multipliers find every critical point.** Minima and saddles appear too; $\lambda_{\max}$ is selected afterwards by comparing values.
- **Spectral norm, not entrywise or Frobenius.** The submatrix claim is about $\sigma_1$, not about every matrix norm automatically (though related inequalities exist).
- **Do not memorize the double sum.** Derive $x^T S x$ on a $2 \times 2$ until the pattern is obvious, then generalize.

## Connections

- [[Home]]
- [[I.7 - Diagonal Entries and Eigenvalue Bounds]] runs the same Lagrangian for Problem 28 of I.7.
- [[I.8 - Forward Reverse and the Block Matrix for SVD]] continues Problem 11: eigenvectors of the block matrix built from $A$.
- [[I.8 - Eigenvalues Bounded by the Largest Singular Value]] identifies $\|A\|$ with $\sigma_1$.
- Prerequisites: gradients of scalar functions of vectors; symmetric $S$.
- Later uses: Rayleigh quotients in I.10; constrained optimization throughout Part VI.

## Sources

- [[2026-07-30 Differentiating Lagrangian for Quadratic Maximization]]

## Open Questions

- Carry out the same differentiation for the *matrix* calculus identity $\frac{\partial}{\partial X}\|AXB\|$ used in Procrustes problems later in the book.
- Is there a clean variational proof of Eckart–Young that starts from this Lagrangian and adds orthogonality constraints on several $x$'s at once?
