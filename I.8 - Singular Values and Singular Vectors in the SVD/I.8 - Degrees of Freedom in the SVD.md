---
title: Degrees of Freedom in the SVD
book: Linear Algebra and Learning from Data
part: I
section: I.8 Singular Values and Singular Vectors in the SVD
pages:
status: seedling
created: 2026-08-01
tags: [type/topic, status/seedling, part/1, section/I-8, svd, degrees-of-freedom, orthogonal-matrices, rank, cr-factorization, inverse, positive-definite]
related: ["[[Home]]", "[[I.8 - Forward Reverse and the Block Matrix for SVD]]", "[[I.8 - Eigenvalues Bounded by the Largest Singular Value]]", "[[I.7 - The Crucial Matrix ATCA]]"]
sources: ["[[2026-08-01 SVD Degrees of Freedom Explained]]"]
---

# Degrees of Freedom in the SVD

## Summary

A rank-$r$ matrix carries exactly $r(m + n - r)$ independent parameters. Counting angles in $U_r$, $\Sigma_r$, and $V_r$ recovers that number; so does the $A = CR$ factorization after removing a hidden $r \times r$ identity. Along the way: the SVD of $A^{-1}$, the singular values of $A^T A$, and the precise reason $A^T A$ is positive (semi)definite.

## Key Results

### Problem 14: a $2 \times 3$ matrix

A $2 \times 3$ matrix has at most two nonzero singular values. Parameter count for a full-rank $A$:

| Piece | Parameters |
| --- | --- |
| Entries of $A$ | $2 \cdot 3 = 6$ |
| $U$ ($2 \times 2$ orthogonal) | $1$ angle |
| $\Sigma$ | $2$ singular values |
| $V$ ($3 \times 3$ orthogonal) | $3$ angles |

Check: $1 + 2 + 3 = 6$.

Geometry of those 3 angles for $V$:

- $v_1, v_2$ span the **row space** (a plane in $\mathbb{R}^3$); $v_3$ spans the nullspace and is the normal to that plane.
- Orienting the plane = pointing the unit normal $v_3$ = **2** angles.
- Rotating the orthonormal pair $(v_1, v_2)$ inside the plane = **1** angle.
- Total: $2 + 1 = 3$.

### Why $v_1, v_2$ *are* the row space

$$
Av_1 = \sigma_1 u_1, \quad Av_2 = \sigma_2 u_2, \quad Av_3 = 0.
$$

So $v_3 \in N(A)$. The row space is $N(A)^\perp$, and $\{v_1, v_2\}$ is an orthonormal basis of that complement.

### Problem 18: inverse and singular values of $A^T A$

If $A$ is square and invertible, $A = U \Sigma V^T$ inverts to

$$
A^{-1} = V \Sigma^{-1} U^T,
$$

which is itself an SVD: singular values of $A^{-1}$ are $1/\sigma_i$.

Substitute into $A^T A$:

$$
A^T A = (V \Sigma U^T)(U \Sigma V^T) = V \Sigma^2 V^T.
$$

Singular values (and eigenvalues) of $A^T A$ are $\sigma_1^2, \dots, \sigma_n^2$.

### Why $A^T A$ is always PSD — and PD when $A$ is invertible

Energy test:

$$
x^T (A^T A) x = \|Ax\|^2 \ge 0.
$$

Always positive *semi*-definite. Strict inequality for all $x \neq 0$ iff $Ax \neq 0$ whenever $x \neq 0$ iff $N(A) = \{0\}$. For square $A$, that is invertibility — exactly Problem 18's hypothesis.

### Problem 23: the count $r(m + n - r)$

Orthonormal columns of $U_r$ in $\mathbb{R}^m$: $u_1$ has $m-1$ free parameters (unit length); $u_k$ has $m-k$ (unit length plus orthogonality to $k-1$ predecessors). Sum:

$$
\sum_{k=1}^{r} (m - k) = mr - \frac{r(r+1)}{2}.
$$

Same for $V_r$ in $\mathbb{R}^n$, plus $r$ singular values:

$$
\left(mr - \tfrac{r(r+1)}{2}\right) + r + \left(nr - \tfrac{r(r+1)}{2}\right) = r(m + n - r).
$$

### Same count from $A = CR$

$C$ is $m \times r$ (independent columns of $A$); $R$ is $r \times n$ (coefficients rebuilding every column). Apparent total $mr + nr$. But $R$ contains an $r \times r$ identity in the columns that reproduce $C$ itself — $r^2$ locked entries. Free parameters:

$$
mr + nr - r^2 = r(m + n - r).
$$

## Intuition

Degrees of freedom are invariant: they describe the manifold of rank-$r$ matrices, not a particular factorization. SVD counts them with angles and stretches; $CR$ counts them with basis columns and combination weights. Same integer.

For the $2 \times 3$ picture: building $V$ is building a framed plane in 3-space. Point the normal (2 angles), then spin the frame inside the plane (1 angle). That is a 3D rotation — three Euler angles — matching the dimension of $SO(3)$.

## Worked Problems

### Filling Problem 14's blanks

- Number of $\sigma$'s for $2 \times 3$: **2**
- Angles left for $V$: **3**
- Angles to position the row-space plane: **2**
- Angle inside the plane for $v_1, v_2$: **1**
- Total angles for $V$: **3**

### Confirming $A^{-1} = V \Sigma^{-1} U^T$

$$
(U \Sigma V^T)(V \Sigma^{-1} U^T) = U \Sigma \Sigma^{-1} U^T = U U^T = I.
$$

**Takeaway:** inversion swaps $U$ and $V$ and reciprocates the singular values — the SVD of the inverse is free once you have the SVD of $A$.

## Pitfalls

- **Maximum rank vs actual rank.** A $2 \times 3$ matrix has *at most* two nonzero $\sigma$'s; a rank-1 example has only one.
- **$A^T A$ is not automatically PD.** Semi-definite always; definite iff $A$ has independent columns (for square $A$: invertible).
- **The $r^2$ subtraction in $CR$ is not optional.** Without removing the embedded identity you double-count the information already stored in $C$.
- **Orthogonal matrices in $n$D have $\binom{n}{2}$ degrees of freedom**, not $n$. The $n = 2, 3$ cases (1 and 3 angles) are the start of that pattern.

## Connections

- [[Home]]
- [[I.8 - Forward Reverse and the Block Matrix for SVD]] for $A^T A = V \Sigma^2 V^T$ from the other direction.
- [[I.8 - Eigenvalues Bounded by the Largest Singular Value]] for $\sigma_1$ as max stretch.
- [[I.7 - The Crucial Matrix ATCA]] for the same $\|Ax\|^2$ energy argument.
- [[I.7 - Tests for Positive Definiteness]] Test 3: $S = A^T A$ with independent columns.
- Prerequisites: row space $\perp$ nullspace; orthogonal matrices as rotations.
- Later uses: low-rank models in I.9; the count $r(m+n-r)$ is the reason thin SVD / economy SVD is the right data structure for rank-$r$ matrices.

## Sources

- [[2026-08-01 SVD Degrees of Freedom Explained]]

## Open Questions

- What is the dimension of the *orthogonal* group $O(n)$ formally, and how does the Stiefel manifold dimension $nr - r(r+1)/2$ generalize the $U_r$ count?
- How do sign/phase ambiguities in singular vectors affect the naive parameter count? (They are discrete or circle-worth of gauge freedom.)
- For complex matrices, replace angles by what?
