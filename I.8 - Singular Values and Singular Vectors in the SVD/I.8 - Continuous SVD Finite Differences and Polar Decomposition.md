---
title: Continuous SVD Finite Differences and Polar Decomposition
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-07-26
tags: [type/topic, status/seedling, part/1, section/I-8, svd, operators, finite-differences, dct, dst, jpeg, polar-decomposition, fourier]
related: ["[[Home]]", "[[I.8 - Forward Reverse and the Block Matrix for SVD]]", "[[I.8 - Degrees of Freedom in the SVD]]"]
sources: ["[[2026-07-26 Unpacking SVD Forward and Reverse]]"]
---

# Continuous SVD, Finite Differences, and Polar Decomposition

## Summary

The SVD architecture survives the leap from matrices to calculus: integration and differentiation act as operators with sine / cosine singular functions. Discretizing the derivative produces a finite-difference matrix $D$ whose singular vectors are discrete sines and cosines — the DST and DCT, and the engine under JPEG. Rearranging the same SVD factors gives the polar decomposition $A = QS$: stretch, then rotate.

## Key Results

### Operators instead of matrices

Treat functions $x(t)$ as vectors. Two operators:

$$
(Ax)(s) = \int_0^s x(t)\, dt, \qquad (Dx)(t) = \frac{dx}{dt}.
$$

$DA = I$ (Fundamental Theorem), but $AD \neq I$ because constants lie in $N(D)$. So $D$ is only a **pseudoinverse** of $A$.

### Continuous singular vectors

Feed a cosine into the integrator:

$$
A(\cos kt) = \frac{1}{k} \sin(kt).
$$

Matches $Av = \sigma u$ with $v = \cos(kt)$, $u = \sin(kt)$, $\sigma = 1/k$. Orthogonality of distinct cosines / sines is the continuous inner product

$$
\langle f, g \rangle = \int f(t) g(t)\, dt.
$$

### Finite differences: calculus on a grid

A backward-difference matrix $D$ (Strang's $4 \times 3$ example) replaces $d/dt$. Then:

- $D^T D$ and $DD^T$ share the same nonzero eigenvalues (the $AB$/$BA$ fact from [[I.8 - Forward Reverse and the Block Matrix for SVD]]).
- The extra zero eigenvalue of the larger product $DD^T$ has eigenvector proportional to $(1,1,1,1)$ — the discrete constant, killed exactly as continuous constants are killed by $d/dt$.
- Right singular vectors of $D$ (eigenvectors of $D^T D$) form the **Discrete Sine Transform (DST)**.
- Left singular vectors (eigenvectors of $DD^T$) form the **Discrete Cosine Transform (DCT)**.

### JPEG in one paragraph

An image block is a vector of pixel values. Multiplying by the DCT matrix projects that block onto discrete cosine waves of increasing frequency. Human vision is insensitive to high-frequency coefficients; JPEG zeros many of them out. File size drops; perceived quality mostly does not. (Practice uses $8 \times 8$ blocks; Strang's $4 \times 4$ $U$ is the same idea at toy scale.)

### Polar decomposition

Every real square $A$ factors as $A = QS$ with $Q$ orthogonal and $S$ symmetric positive semidefinite. Steal both factors from the SVD $A = U \Sigma V^T$ by inserting $V^T V = I$:

$$
A = (U V^T)\, (V \Sigma V^T) = Q S.
$$

- $Q = UV^T$ is orthogonal (product of orthogonals).
- $S = V \Sigma V^T$ is symmetric PSD with eigenvalues $\sigma_i$; also $S^2 = A^T A$, so $S$ is the positive square root of $A^T A$.

Analogy: a complex number $r e^{i\theta}$ stretches by $r$ then rotates by $\theta$. Here $S$ stretches, $Q$ rotates.

## Intuition

| Setting | "Derivative" | Input singular vectors $v$ | Output singular vectors $u$ |
| --- | --- | --- | --- |
| Continuous | $d/dt$ | sines | cosines |
| Discrete | finite-difference $D$ | DST | DCT |

The SVD does not know whether it is acting on $\mathbb{R}^n$ or on a space of functions. Orthogonality, singular values, and the four subspaces all persist; only the inner product changes from a sum to an integral.

Polar decomposition separates **what a matrix does to lengths** ($S$) from **what it does to angles** ($Q$). In continuum mechanics that is the split between deforming a material and tumbling it through space.

### Fourier as spectral theory (optional bridge)

The second-derivative operator $L = d^2/dt^2$ has eigenfunctions $\sin(\omega t)$ and $\cos(\omega t)$ with eigenvalue $-\omega^2$ — a 2D eigenspace per frequency. The Fourier series

$$
F(t) = \frac{a_0}{2} + \sum_{n=1}^{\infty} \big( a_n \cos(nt) + b_n \sin(nt) \big)
$$

is the expansion of $F$ in that eigenbasis. Complex form $F(t) = \sum_{n=-\infty}^{\infty} c_n e^{int}$ packages each 2D eigenspace into one exponential; negative frequencies cancel imaginary parts for real signals. This is the continuous cousin of "project onto eigenvectors," not a separate subject.

## Worked Example

### Reading Strang's difference matrix

Nonzero eigenvalues of $D^T D$ and $DD^T$ match: $2+\sqrt{2}$, $2$, $2-\sqrt{2}$. The $4 \times 4$ product has one extra zero; its eigenvector is the flat vector. Columns of $U$ read as sampled cosines of rising frequency — literally the DCT matrix at $n = 4$.

**Takeaway:** JPEG is not an engineering hack bolted onto linear algebra. It is the SVD of a discrete derivative, truncated in the spectral domain.

### Building $Q$ and $S$ from a known SVD

Given $U$, $\Sigma$, $V$, compute $Q = UV^T$ and $S = V\Sigma V^T$. Verify $QS = U\Sigma V^T = A$ and $S^T = S$, $Q^T Q = I$.

**Takeaway:** polar decomposition is a regrouping, not a new factorization algorithm.

## Pitfalls

- **$DA = I$ does not make $D$ a two-sided inverse.** Nullspace of $D$ (constants) blocks $AD = I$.
- **DST vs DCT assignment.** Right singular vectors of the difference matrix $\leftrightarrow$ DST; left $\leftrightarrow$ DCT. Swapping them loses the continuous parallel (derivative sends sine $\to$ cosine).
- **Polar $S$ is PSD, not always PD.** Zero singular values make $S$ singular; $A$ need not be invertible.
- **Left vs right polar forms.** $A = QS$ (right polar) and $A = S'Q$ (left polar) both exist; $S$ and $S'$ differ unless $A$ is normal.
- **Fourier digression is scaffolding.** Strang's I.8 point is the operator SVD and the discrete parallel; full spectral theory is a longer road.

## Connections

- [[Home]]
- [[I.8 - Forward Reverse and the Block Matrix for SVD]] for $AB$/$BA$ sharing nonzero eigenvalues, used on $D^T D$ and $DD^T$.
- [[I.8 - Degrees of Freedom in the SVD]] for $A^T A = V\Sigma^2 V^T$, which is $S^2$ in the polar picture.
- [[I.8 - Eigenvalues Bounded by the Largest Singular Value]] for $\sigma_1$ as max stretch — the size of the polar stretch factor.
- Prerequisites: SVD; orthogonal matrices; $A^T A$ eigenproblem.
- Later uses: DCT/JPEG as the motivating application of orthogonal transforms; polar decomposition in continuum mechanics and in the Procrustes problem (Part IV).

## Sources

- [[2026-07-26 Unpacking SVD Forward and Reverse]]

## Open Questions

- What boundary conditions turn the continuous derivative into sine vs cosine eigenfunctions, and how do those choices produce DST vs DCT on the grid?
- How does the left polar form $A = S'Q$ relate to $AA^T$ instead of $A^T A$?
- Where in Part VII (learning from data) does the continuous–discrete dictionary reappear — neural tangent kernels, score matching, diffusion?
