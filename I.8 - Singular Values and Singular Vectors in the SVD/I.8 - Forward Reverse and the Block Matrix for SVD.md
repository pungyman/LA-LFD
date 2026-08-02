---
title: Forward Reverse and the Block Matrix for SVD
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-07-26
tags: [type/topic, status/seedling, part/1, section/I-8, svd, singular-vectors, block-matrices, nullspace, eigenvalues, ata, aat]
related: ["[[Home]]", "[[I.8 - Differentiating the Lagrangian]]", "[[I.8 - Eigenvalues Bounded by the Largest Singular Value]]", "[[I.8 - Continuous SVD Finite Differences and Polar Decomposition]]"]
sources: ["[[2026-07-26 Unpacking SVD Forward and Reverse]]", "[[2026-07-30 Differentiating Lagrangian for Quadratic Maximization]]"]
---

# Forward Reverse and the Block Matrix for SVD

## Summary

$A$ maps right singular vectors to left ones; $A^T$ runs the map in reverse. Gluing both directions into one symmetric block matrix

$$
S = \begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}
$$

packages the entire SVD as a single eigenproblem. The same algebra shows that $AB$ and $BA$ share every nonzero eigenvalue — the reason $A^T A$ and $AA^T$ produce matching $\sigma_i^2$.

## Key Results

### Forward and reverse

$$
A v_k = \sigma_k u_k, \qquad A^T u_k = \sigma_k v_k.
$$

For indices past the rank, $A v_k = 0$ ($k > r$) and $A^T u_k = 0$ ($k > r$). Extra singular vectors live in the nullspaces.

### The all-in-one block matrix

For $A$ of size $m \times n$,

$$
S = \begin{bmatrix} 0 & A \\ A^T & 0 \end{bmatrix}
$$

is symmetric of size $(m+n) \times (m+n)$. Stacking singular vectors gives eigenvectors of $S$:

$$
S \begin{bmatrix} u_k \\ v_k \end{bmatrix}
= \begin{bmatrix} A v_k \\ A^T u_k \end{bmatrix}
= \sigma_k \begin{bmatrix} u_k \\ v_k \end{bmatrix}.
$$

The same construction with a minus sign produces eigenvalue $-\sigma_k$ with eigenvector $(u_k, -v_k)$ (or similar sign pattern). So each positive singular value contributes a $\pm\sigma_k$ pair: $2r$ eigenpairs from the $r$ nonzero singular values.

### The remaining $m + n - 2r$ eigenvectors

$S$ needs $m+n$ independent eigenvectors. The missing ones come from the nullspaces, padded with zeros, and all have eigenvalue $0$:

- $v_k \in N(A)$ ($n - r$ of them): $S \begin{bmatrix} 0 \\ v_k \end{bmatrix} = 0$.
- $u_k \in N(A^T)$ ($m - r$ of them): $S \begin{bmatrix} u_k \\ 0 \end{bmatrix} = 0$.

Count: $(n-r) + (m-r) = m + n - 2r$.

### $AB$ and $BA$ share nonzero eigenvalues

If $ABx = \lambda x$ with $\lambda \neq 0$, multiply by $B$:

$$
(BA)(Bx) = \lambda (Bx).
$$

So $Bx$ is an eigenvector of $BA$ for the same $\lambda$. The hypothesis $\lambda \neq 0$ guarantees $Bx \neq 0$. Taking $B = A^T$ shows that $AA^T$ and $A^T A$ share their nonzero eigenvalues — precisely the squared singular values $\sigma_i^2$.

If $m > n$, the larger product $AA^T$ carries $m - n$ extra zero eigenvalues to fill out its count.

## Intuition

$A$ is a machine $v \mapsto u$. $A^T$ is the reverse machine $u \mapsto v$. The block matrix $S$ is both machines wired into one symmetric system: feed it a stacked $(u, v)$ and it returns $\sigma$ times the same stack.

The nullspace leftovers are directions the machines crush to zero. Padding them with a block of zeros embeds those crushed directions into the big space of $S$, where they become ordinary eigenvectors for $\lambda = 0$.

## Worked Example

### Problem 11: diagonal $A$ inside the block

Strang takes $A = \operatorname{diag}(1, 2, \dots, n)$ and

$$
S = \begin{bmatrix} 0 & A \\ A & 0 \end{bmatrix}
$$

(using $A = A^T$). Split an eigenvector as $(x, y)$. The block equation becomes the coupled system

$$
Ay = \lambda x, \qquad Ax = \lambda y.
$$

Substitute $y = \lambda^{-1} A x$ into the first equation:

$$
A^2 x = \lambda^2 x.
$$

Eigenvalues of $A^2$ are $1^2, \dots, n^2$, so $\lambda = \pm k$ for each $k$. With $x = e_k$:

- $\lambda = k$ gives $y = e_k$, eigenvector $\begin{bmatrix} e_k \\ e_k \end{bmatrix}$;
- $\lambda = -k$ gives $y = -e_k$, eigenvector $\begin{bmatrix} e_k \\ -e_k \end{bmatrix}$.

**Takeaway:** the abstract $\pm\sigma$ picture is completely explicit when $A$ is diagonal — singular values are the $|a_{ii}|$, and the stacked $\pm$ eigenvectors are visible by hand.

## Pitfalls

- **Signs for $-\sigma_k$.** Different texts stack $(u, -v)$ or $(-u, v)$; both work. Track one convention consistently.
- **Zero eigenvalues of $S$ are not a defect.** They are exactly the nullspace contributions; count them rather than fearing them.
- **$AB$ and $BA$ need not be the same size.** Only the *nonzero* spectra match; the larger matrix pads with zeros.
- **$\lambda \neq 0$ is essential in the shifting argument.** If $\lambda = 0$, $Bx$ might vanish and you cannot promote it to an eigenvector of $BA$.

## Connections

- [[Home]]
- [[I.8 - Differentiating the Lagrangian]] is the source of Problem 11's calculation.
- [[I.8 - Eigenvalues Bounded by the Largest Singular Value]] uses $\|Ax\| \le \sigma_1 \|x\|$, which is the forward map's stretch.
- [[I.8 - Continuous SVD Finite Differences and Polar Decomposition]] reuses $D^T D$ vs $DD^T$ sharing nonzero eigenvalues.
- [[I.8 - Degrees of Freedom in the SVD]] for $A^T A = V \Sigma^2 V^T$ as an explicit eigen/SVD factorization.
- Prerequisites: four fundamental subspaces; symmetric eigenproblems.
- Later uses: computing the SVD via the eigenproblem for $A^T A$ (or the stable Golub–Kahan bidiagonalization that avoids forming it explicitly).

## Sources

- [[2026-07-26 Unpacking SVD Forward and Reverse]]
- [[2026-07-30 Differentiating Lagrangian for Quadratic Maximization]]

## Open Questions

- How does Golub–Kahan bidiagonalization compute the same information as $S$'s eigenproblem without forming $A^T A$?
- What is the condition number relationship between $A$ and the block matrix $S$?
- For complex $A$, what replaces the real block construction — the Hermitian dilation?
