---
title: From Covariance to SVD
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-07-22
tags: [type/topic, status/seedling, part/1, section/I-8, svd, pca, kl-transform, covariance, eckart-young, positive-semidefinite]
related: ["[[Home]]", "[[I.8 - Eigenvalues Bounded by the Largest Singular Value]]", "[[I.7 - The Crucial Matrix ATCA]]"]
sources: ["[[2026-07-20 Eigenvalues Bounded by Largest Singular Value]]"]
---

# From Covariance to SVD

## Summary

The Karhunen–Loève (KL) transform, PCA, and the SVD are three names for one geometry. Start with a covariance matrix $V$; its eigenvectors $u_i$ are the new basis; truncating that basis is optimal by Eckart–Young. In the discrete case the engine that computes it is the SVD of the data matrix.

## Key Results

### Covariance is symmetric and PSD

A covariance matrix $V$ of a zero-mean process is symmetric and positive semidefinite. Its eigenvalues are therefore real and nonnegative; Strang writes them as squared singular values $\sigma_1^2 \ge \sigma_2^2 \ge \cdots \ge 0$.

### The KL / PCA expansion

The eigenvectors $u_i$ of $V$ form an orthonormal basis. Any vector expands as

$$
v = \sum_i (u_i^T v)\, u_i.
$$

The coefficients $u_i^T v$ are the coordinates in the eigenbasis. Because those $u_i$ diagonalize the covariance, the transform **decorrelates** the process: that is PCA in discrete statistics, and KL in the continuous stochastic setting.

### The SVD computes it

For a centered data matrix $A$, the right singular vectors (columns of $V$ in $A = U \Sigma V^T$) are the eigenvectors of the Gram / covariance matrix $A^T A$. The singular values of $A$ are the square roots of the eigenvalues of that covariance.

### Eckart–Young

Stopping the expansion after $k$ terms minimizes expected squared error. Ordering $\sigma_1^2 \ge \sigma_2^2 \ge \cdots$ puts the highest-variance directions first; truncating the SVD to the top $k$ singular values is the optimal rank-$k$ approximation of the data.

## Intuition

Three layers, one idea:

| Layer | Object | Role |
| --- | --- | --- |
| Continuous theory | KL transform | eigenfunctions of a covariance operator |
| Discrete statistics | PCA | eigenvectors of a sample covariance |
| Linear algebra engine | SVD of $A$ | computes those eigenvectors as right singular vectors |

The phrase "decorrelates the random process" means: in the $u_i$ coordinates, off-diagonal covariances vanish. You have rotated into the principal axes of the cloud.

## Worked Example

### Building the $10 \times 10$ covariance, then cutting to 5D

$n$ observations of a 10-dimensional vector form a data matrix $X$ of size $n \times 10$. Mean-center each column to get $X_c$. The sample covariance is

$$
C = \frac{1}{n-1} X_c^T X_c \in \mathbb{R}^{10 \times 10}.
$$

Eigenvectors of $C$, sorted by descending eigenvalue, are the principal axes. Keep the top 5 and project onto them to reduce dimension.

### Why $C$ is always PSD

Algebra: for any $v$,

$$
v^T (X_c^T X_c) v = (X_c v)^T (X_c v) = \|X_c v\|^2 \ge 0.
$$

Same substitution used for $A^T A$ in [[I.7 - The Crucial Matrix ATCA]] and again in [[I.8 - Degrees of Freedom in the SVD]].

Statistics: $v^T C v$ is the variance of the data projected onto the line spanned by $v$. Variance cannot be negative, so $C$ cannot fail the energy test.

**Takeaway:** PSD is not an extra assumption on covariance matrices. It is the statement that variance is a squared length.

## Pitfalls

- **Center first.** Skipping mean-centering mixes the mean into the leading "principal component."
- **$A^T A$ vs $\frac{1}{n-1} A^T A$.** Scaling changes eigenvalues but not eigenvectors; PCA directions are the same either way.
- **KL is continuous; PCA is discrete.** The geometry matches; the objects (operators vs matrices) differ.
- **Eckart–Young optimizes Frobenius / spectral error for matrices**, not every conceivable loss. It is the right theorem for squared error, not a blank check.

## Connections

- [[Home]]
- [[I.8 - Eigenvalues Bounded by the Largest Singular Value]] for $\sigma_1$ as maximum stretch.
- [[I.8 - Degrees of Freedom in the SVD]] for why $A^T A$ is PSD / PD.
- [[I.7 - The Crucial Matrix ATCA]] for the $x^T A^T A x = \|Ax\|^2$ move.
- [[I.7 - Positive Definite Matrices and the Hessian]] for principal axes of a quadratic form — same geometry, energy bowl instead of data cloud.
- Later uses: I.9 (best low-rank matrix / PCA) is the full treatment; this note is the I.8 bridge.

## Sources

- [[2026-07-20 Eigenvalues Bounded by Largest Singular Value]]

## Open Questions

- Exact statement of Eckart–Young for the spectral norm vs the Frobenius norm — same optimizers?
- How does the continuous KL eigenfunction problem reduce to a matrix eigenproblem under discretization?
- When the sample size $n$ is smaller than the dimension, what does the SVD of $X_c$ buy you over forming $C$ explicitly?
