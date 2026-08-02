---
title: Eigenvalues Bounded by the Largest Singular Value
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-07-20
tags: [type/topic, status/seedling, part/1, section/I-8, svd, singular-values, eigenvalues, spectral-norm, rank-one, cauchy-schwarz]
related: ["[[Home]]", "[[I.8 - Degrees of Freedom in the SVD]]", "[[I.8 - Forward Reverse and the Block Matrix for SVD]]"]
sources: ["[[2026-07-20 Eigenvalues Bounded by Largest Singular Value]]"]
---

# Eigenvalues Bounded by the Largest Singular Value

## Summary

Every eigenvalue of a square matrix $A$ is bounded by its largest singular value: $|\lambda| \le \sigma_1$. The proof is a one-line reading of the SVD: orthogonal factors never change lengths, and the diagonal $\Sigma$ stretches by at most $\sigma_1$. The same geometry, applied to a rank-one matrix, recovers Cauchy–Schwarz as a corollary.

## Key Results

### The bound

> For any square $A$ with largest singular value $\sigma_1$ and any eigenvalue $\lambda$,
> $$|\lambda| \le \sigma_1.$$

### Proof via the SVD

Substitute $A = U \Sigma V^T$. Orthogonal multiplications preserve length:

$$
\|Ax\| = \|U \Sigma V^T x\| = \|\Sigma V^T x\| \le \sigma_1 \|V^T x\| = \sigma_1 \|x\|
$$

for every $x$. That is equation (13) in Strang: $\|Ax\| \le \sigma_1 \|x\|$ always.

If $x$ is an eigenvector, $\|Ax\| = |\lambda| \|x\|$. Combine:

$$
|\lambda| \|x\| \le \sigma_1 \|x\| \implies |\lambda| \le \sigma_1.
$$

### Why $\Sigma$ stretches by at most $\sigma_1$

Set $y = V^T x$. The claim reduces to $\|\Sigma y\| \le \sigma_1 \|y\|$. Because $\Sigma$ is diagonal with $\sigma_1 \ge \sigma_2 \ge \cdots \ge 0$,

$$
\Sigma y = (\sigma_1 y_1, \sigma_2 y_2, \dots, \sigma_n y_n)^T.
$$

Each component is scaled independently — no mixing, no rotation. Square the length:

$$
\|\Sigma y\|^2 = \sum_i (\sigma_i y_i)^2 \le \sum_i (\sigma_1 y_i)^2 = \sigma_1^2 \|y\|^2,
$$

where the inequality replaces every $\sigma_i$ by the largest one. Take square roots.

**How to see it.** Component-wise scaling is the clean view. Columns of $\Sigma$ are $\sigma_i e_i$; the same Pythagoras appears because those columns are orthogonal. Row-dot-products collapse to the same calculation immediately.

## Intuition

$\sigma_1$ is the **maximum stretching power** of $A$: the longest image of a unit vector. An eigenvector is a special input whose image is a pure scale by $\lambda$. That scale cannot exceed the machine's maximum stretch, so $|\lambda|$ cannot beat $\sigma_1$.

Equality is possible: when $A$ is symmetric positive definite, eigenvalues and singular values coincide, and the top ones match.

## Worked Example

### Rank-one SVD by normalizing

Given $A = x y^T$, the outer product is already almost an SVD. The missing rule is that singular vectors must be **unit length**. Force the rule:

$$
A = \underbrace{\left(\frac{x}{\|x\|}\right)}_{u_1} \underbrace{\big(\|x\| \|y\|\big)}_{\sigma_1} \underbrace{\left(\frac{y^T}{\|y\|}\right)}_{v_1^T}.
$$

No eigendecomposition required — just peel lengths off $x$ and $y$ and park them in the middle as $\sigma_1$.

### Rank-one eigenvalue, then Cauchy–Schwarz

Feed an arbitrary $z$ into $A$:

$$
Az = x (y^T z) = c\, x.
$$

Every output lies on the line spanned by $x$. The only direction that can match its own image is $x$ itself:

$$
Ax = (y^T x)\, x \implies \lambda = y^T x, \quad \text{eigenvector } x.
$$

Combine with $|\lambda| \le \sigma_1$:

$$
|y^T x| \le \|x\| \|y\|.
$$

That is Cauchy–Schwarz, arrived at through the SVD of a rank-one matrix.

**Takeaway:** the bound $|\lambda| \le \sigma_1$ is not a special fact about eigenvalues. It is the spectral-norm definition $\|A\| = \sigma_1$ applied to one vector.

## Pitfalls

- **$|\lambda| \le \sigma_1$ needs a square matrix** for eigenvalues to exist, but the stretch inequality $\|Ax\| \le \sigma_1 \|x\|$ holds for rectangular $A$ too.
- **Singular values are nonnegative; eigenvalues need not be.** The absolute value on $\lambda$ is load-bearing.
- **Component-wise scaling is special to $\Sigma$.** Do not import that picture to a general matrix; the orthogonal factors $U$ and $V$ are what strip the geometry down to a diagonal.

## Connections

- [[Home]]
- [[I.8 - Forward Reverse and the Block Matrix for SVD]] builds the SVD from $A^T A$ and $AA^T$, whose eigenvalues are the $\sigma_i^2$.
- [[I.8 - Degrees of Freedom in the SVD]] counts the free parameters inside $U$, $\Sigma$, and $V$.
- [[I.8 - From Covariance to SVD]] takes the same $\sigma_i^2$ into PCA and the KL transform.
- [[I.7 - Diagonal Entries and Eigenvalue Bounds]] is the Rayleigh-quotient cousin: curvature bounds instead of stretch bounds.
- Prerequisites: SVD definition $A = U \Sigma V^T$, orthogonal length-preservation.
- Later uses: the spectral norm $\|A\| = \sigma_1$ is the workhorse of Part II and of compressed sensing.

## Sources

- [[2026-07-20 Eigenvalues Bounded by Largest Singular Value]]

## Open Questions

- When is $|\lambda| = \sigma_1$? Characterize the matrices that attain the bound.
- How does the bound refine for the *other* singular values — e.g. Weyl-type comparisons between $|\lambda_k|$ and $\sigma_k$?
- Revisit the rank-one picture after I.9: how does adding an orthogonal second outer product change the "funnel" geometry?
