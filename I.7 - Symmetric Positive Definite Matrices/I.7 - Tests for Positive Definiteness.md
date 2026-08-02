---
title: Tests for Positive Definiteness
book: Linear Algebra and Learning from Data
part: I
section: I.7 Symmetric Positive Definite Matrices
pages: 48-49
status: seedling
created: 2026-06-28
tags: [type/topic, status/seedling, part/1, section/I-7, positive-definite-matrices, leading-determinants, principal-minors, pivots, elimination, ldlt, cholesky, factorization]
related: ["[[Home]]", "[[I.7 - Positive Definite Matrices and the Hessian]]"]
sources: ["[[2026-06-28 Leading Determinants and Positive Definite Matrices]]"]
---

# Tests for Positive Definiteness

## Summary

A symmetric matrix $S$ is positive definite when its energy $x^T S x$ is strictly positive for every non-zero $x$. Strang gives five equivalent tests for this; the determinant test and the pivot test are the two mechanical ones, and they are equivalent because **the $k$th pivot is the ratio of consecutive leading determinants**.

## Key Results

Strang's five tests are all equivalent for a **symmetric** $S$. Any one of them implies the other four.

| Test | Statement |
| --- | --- |
| 1 | All eigenvalues are positive: $\lambda_i > 0$. |
| 2 | The energy is positive: $x^T S x > 0$ for all $x \neq 0$. |
| 3 | $S = A^T A$ for some $A$ with independent columns. |
| 4 | All leading determinants are positive: $D_1, \dots, D_n > 0$. |
| 5 | All pivots are positive. |

### Leading determinants

The **leading determinants** (mathematically, the *leading principal minors*) are the determinants of the square submatrices in the top-left corner of $S$. For an $n \times n$ matrix:

- $D_1$ is the determinant of the top-left $1 \times 1$ block.
- $D_2$ is the determinant of the top-left $2 \times 2$ block.
- $D_k$ is the determinant of the top-left $k \times k$ block, up to $D_n = \det S$.

Note the word *leading*: these are the top-left blocks specifically, not all principal minors.

### Test 4, the determinant test

> $S$ is positive definite **if and only if** every leading determinant $D_1, \dots, D_n$ is strictly greater than zero.

### The bridge between Test 4 and Test 5

Elimination reveals a direct relationship between the pivots and the leading determinants:

$$
\text{the } k\text{th pivot} = \frac{D_k}{D_{k-1}}, \qquad D_0 = 1.
$$

This is *why* the two tests are equivalent. A pivot is a positive number divided by a positive number, so if all the leading determinants are positive, every pivot is guaranteed positive too, and vice versa.

The determinant test is usually favoured for small matrices: computing a few small determinants by hand beats running full Gaussian elimination.

## Intuition

The five tests are not five different facts. They are five different vantage points on a single geometric statement: *the bowl $x^T S x$ curves upwards in every direction.*

- Test 1 (eigenvalues) reads the curvature directly along the principal axes.
- Test 2 (energy) is the definition itself.
- Test 3 ($S = A^T A$) says the bowl is really a squared length in disguise.
- Tests 4 and 5 (determinants and pivots) are the *computational* views: they never mention geometry, but elimination quietly checks every direction for you.

## Worked Example

### The determinant test on the second difference matrix

$$
S = \begin{bmatrix} 2 & -1 & 0 & 0 \\ -1 & 2 & -1 & 0 \\ 0 & -1 & 2 & -1 \\ 0 & 0 & -1 & 2 \end{bmatrix}
$$

Peel off the nested top-left blocks:

- $D_1 = \det \begin{bmatrix} 2 \end{bmatrix} = 2$
- $D_2 = \det \begin{bmatrix} 2 & -1 \\ -1 & 2 \end{bmatrix} = (2)(2) - (-1)(-1) = 3$
- $D_3 = \det \begin{bmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{bmatrix} = 4$
- $D_4 = \det S = 5$

Every leading determinant is positive, so $S$ passes Test 4 and is positive definite.

**Takeaway:** the pattern $D_k = k+1$ makes the pivot formula immediate: the pivots are $\tfrac{2}{1}, \tfrac{3}{2}, \tfrac{4}{3}, \tfrac{5}{4}$, all positive, confirming Test 5 without any elimination.

## Proving the Pivot Test

The proof rests entirely on the symmetric factorization $S = LDL^T$.

### The foundation

Gaussian elimination on a symmetric $S$ (with no row exchanges) gives $S = LU$. Because $S$ is symmetric, $U$ splits further to pull the pivots out into their own diagonal matrix:

$$
S = LDL^T
$$

- $L$ is lower triangular with **$1$s on its main diagonal**.
- $D$ is diagonal, and its entries $d_1, \dots, d_n$ are exactly the **pivots** of $S$.
- $L^T$ is upper triangular, also with $1$s on the diagonal.

### The key substitution

Put the factorization into the energy and regroup:

$$
x^T S x = x^T (LDL^T) x = (x^T L) D (L^T x)
$$

Define $y = L^T x$. Since $(L^T x)^T = x^T L$, we have $y^T = x^T L$, and the energy collapses to

$$
x^T S x = y^T D y = d_1 y_1^2 + d_2 y_2^2 + \cdots + d_n y_n^2.
$$

**The energy is a weighted sum of squares, weighted by the pivots.** Both directions of the proof fall out of this one identity.

The load-bearing detail: $L$ has $1$s on its diagonal, so $\det L = 1$ and $L^T$ is **invertible**. That invertibility is what makes the change of variable $x \leftrightarrow y$ lossless in both directions.

### Part 1: positive pivots $\Rightarrow$ positive definite

Assume every $d_i > 0$; show $x^T S x > 0$ for every $x \neq 0$.

1. Every $y_i^2 \geq 0$, since real squares are non-negative.
2. Every $d_i > 0$ by assumption, so every term $d_i y_i^2 \geq 0$.
3. $L^T$ is invertible, so $x \neq 0$ forces $y = L^T x \neq 0$.
4. Therefore at least one $y_i^2 > 0$, making its term strictly positive.
5. The sum is strictly positive. $\blacksquare$

### Part 2: positive definite $\Rightarrow$ positive pivots

Assume $x^T S x > 0$ for all $x \neq 0$; show every $d_i > 0$.

1. Because $L^T$ is invertible, *any* $y$ we like is reachable from a unique $x$.
2. Choose the $x$ that produces $y = (1, 0, \dots, 0)$. Then

$$
x^T S x = d_1(1)^2 + d_2(0)^2 + \cdots + d_n(0)^2 = d_1.
$$

3. Positive definiteness says $x^T S x > 0$, hence $d_1 > 0$.
4. Repeat with $y = e_i$ to isolate each $d_i$ in turn. $\blacksquare$

Note the symmetry of the two halves: Part 1 needs $y \neq 0$ (invertibility forwards), Part 2 needs every $y$ to be *reachable* (invertibility backwards).

## Cholesky: Where the Square Roots Come From

Test 3 says a positive definite $S$ factors as $S = A^T A$. Getting there from $S = LDL^T$ means **sharing the pivots equally** between the two halves, and that is where the square roots enter:

$$
A = \sqrt{D}\, L^T
$$

For the $3 \times 3$ second difference matrix, elimination gives

$$
D = \begin{bmatrix} 2 & 0 & 0 \\ 0 & \frac{3}{2} & 0 \\ 0 & 0 & \frac{4}{3} \end{bmatrix},
\qquad
L^T = \begin{bmatrix} 1 & -\frac{1}{2} & 0 \\ 0 & 1 & -\frac{2}{3} \\ 0 & 0 & 1 \end{bmatrix}
$$

(Those pivots $2, \tfrac{3}{2}, \tfrac{4}{3}$ are exactly $\tfrac{D_1}{D_0}, \tfrac{D_2}{D_1}, \tfrac{D_3}{D_2}$ from the worked example above.)

The square root of a diagonal matrix is entrywise:

$$
\sqrt{D} = \begin{bmatrix} \sqrt{2} & 0 & 0 \\ 0 & \sqrt{\frac{3}{2}} & 0 \\ 0 & 0 & \sqrt{\frac{4}{3}} \end{bmatrix}
$$

Multiplying out $A = \sqrt{D} L^T$ produces entries that *look* wrong against the textbook until you rationalize them:

- **Row 1, column 2:** $\sqrt{2} \cdot \left(-\tfrac{1}{2}\right) = -\tfrac{\sqrt{2}}{2} = -\tfrac{1}{\sqrt{2}}$.
- **Row 2, column 3:** $\sqrt{\tfrac{3}{2}} \cdot \left(-\tfrac{2}{3}\right) = -\sqrt{\tfrac{3}{2} \cdot \tfrac{4}{9}} = -\sqrt{\tfrac{12}{18}} = -\sqrt{\tfrac{2}{3}}$, by pulling the fraction inside the root as its square.

$$
A = \begin{bmatrix} \sqrt{2} & -\frac{1}{\sqrt{2}} & 0 \\ 0 & \sqrt{\frac{3}{2}} & -\sqrt{\frac{2}{3}} \\ 0 & 0 & \sqrt{\frac{4}{3}} \end{bmatrix}
$$

This matches the book. There is no error on the page: Strang simply skips the rationalization steps, so the transition reads like a typo at first glance.

## Pitfalls

- **All five tests presuppose symmetry.** They say nothing about a non-symmetric matrix, where "positive definite" is not even standardly defined.
- **Leading determinants are not all principal minors.** Test 4 checks only the nested top-left blocks. Checking arbitrary principal minors is a different (and stronger) condition.
- **$D_n > 0$ alone is not enough.** A negative determinant rules positive definiteness out, but a positive one proves nothing on its own: two negative eigenvalues multiply to a positive determinant. Every $D_k$ must be checked.
- **The pivot formula needs $D_{k-1} \neq 0$.** The chain $d_k = D_k / D_{k-1}$ assumes elimination runs without row exchanges, which is guaranteed for positive definite $S$ but not in general.
- **$\sqrt{D}$ is only real when the pivots are positive.** Cholesky exists *because* $S$ is positive definite; the square roots are the factorization noticing that fact.

## Connections

- [[Home]]
- [[I.7 - Positive Definite Matrices and the Hessian]] applies the energy test to the Hessian and the principal axes.
- [[I.7 - Diagonal Entries and Eigenvalue Bounds]] uses the energy test on basis vectors.
- [[I.6 - Eigenvalues of Orthogonal and Symmetric Matrices]] supplies Test 1, that symmetric matrices have real eigenvalues.
- Prerequisites: elimination and $A = LU$ (I.4), determinants.
- Later uses: Cholesky is the workhorse for solving $Sx = b$ and for sampling Gaussians.

## Sources

- [[2026-06-28 Leading Determinants and Positive Definite Matrices]]

## Open Questions

- Why exactly does $d_k = D_k / D_{k-1}$ fall out of elimination? The equivalence is used above but not derived.
- What is the semi-definite version of each test, and where does strictness break?
- Is the Cholesky factor $A$ unique if we insist on positive diagonal entries?
