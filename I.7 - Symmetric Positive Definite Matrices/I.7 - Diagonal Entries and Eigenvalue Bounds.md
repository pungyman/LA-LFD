---
title: Diagonal Entries and Eigenvalue Bounds
book: Linear Algebra and Learning from Data
part: I
section: I.7 Symmetric Positive Definite Matrices
pages:
status: seedling
created: 2026-07-10
tags: [type/topic, status/seedling, part/1, section/I-7, positive-definite-matrices, diagonal-entries, eigenvalue-bounds, rayleigh-quotient, quadratic-forms, basis-vectors, lagrange-multipliers, covariance]
related: ["[[Home]]", "[[I.7 - Tests for Positive Definiteness]]"]
sources: ["[[2026-07-10 Positive Definite Matrix Diagonal Properties]]"]
---

# Diagonal Entries and Eigenvalue Bounds

## Summary

Testing the energy $x^T S x$ on the standard basis vectors extracts the diagonal entries one at a time. That single trick explains why a positive definite matrix must have a strictly positive diagonal, and it generalizes into a universal fact about **every** real symmetric matrix: each diagonal entry is trapped between the smallest and largest eigenvalue.

## Key Results

### Basis vectors extract diagonal entries

For any symmetric $S$ and the standard basis vector $e_i$:

$$
e_i^T S e_i = s_{ii}
$$

The quadratic form evaluated at $e_i$ isolates the $i$th diagonal entry exactly. This is the engine behind everything below.

### The diagonal of a positive definite matrix is strictly positive

Positive definiteness demands $x^T S x > 0$ for **every** non-zero $x$, so in particular for every $e_i$. Hence $s_{ii} > 0$ for all $i$.

This is a **necessary but not sufficient** condition. See the counterexample below.

### Diagonal entries are bounded by the eigenvalues

For any real symmetric $S$, with $\lambda_{\min}$ and $\lambda_{\max}$ its extreme eigenvalues:

$$
\lambda_{\min} \le s_{jj} \le \lambda_{\max} \quad \text{for every } j.
$$

**This holds for all real symmetric matrices**, not just positive definite ones. Positive definiteness is merely the special case $\lambda_{\min} > 0$, which squeezes the chain into $0 < \lambda_{\min} \le s_{jj} \le \lambda_{\max}$ and recovers the positive-diagonal rule.

### The Rayleigh quotient

The bound above is a corollary of the Rayleigh quotient theorem. For any real symmetric $S$ and any $x \neq 0$:

$$
\lambda_{\min} \le \frac{x^T S x}{x^T x} \le \lambda_{\max}
$$

Both ends are **attained**, at the corresponding eigenvectors:

$$
\max_{x \neq 0} \frac{x^T S x}{x^T x} = \lambda_{\max}
$$

## Intuition

The diagonal entries are **the most exposed part of a matrix**. They are what you see when you probe the quadratic form along the coordinate axes and nowhere else.

Three ways to see why they must be positive when $S$ is:

1. **Extraction.** $e_i^T S e_i = s_{ii}$, and positive definiteness applies to *every* vector, basis vectors included.
2. **Subspaces.** A positive definite matrix stays positive definite on every subspace. The diagonal entries are precisely the $1 \times 1$ principal submatrices. A non-positive $s_{ii}$ means the matrix already fails in a one-dimensional subspace, which compromises the whole thing.
3. **Applied readings.** For a Hessian, $s_{ii} \le 0$ means the loss landscape is flat or sloping *downwards* as you move along that single parameter's axis, so you are not in a bowl. For a covariance matrix, $s_{ii}$ is the variance of variable $i$; a zero there is a variable with no variance at all, a deterministic constant. Such a system can be positive *semi*-definite at best.

The Rayleigh quotient makes the whole picture one statement. The fraction $\frac{x^T S x}{x^T x}$ measures curvature in the direction $x$, normalized by length. Curvature is largest along the top eigenvector and smallest along the bottom one, and every other direction is a blend that lands somewhere in between. The diagonal entries are just the curvatures along the $n$ coordinate axes, so they cannot escape that range either. **The diagonal is a middle ground, always trapped inside the extremes the eigenvalues dictate.**

## Worked Problems

### Problem 18: a positive diagonal is necessary

$$
S = \begin{bmatrix} 4 & 1 & 1 \\ 1 & 0 & 2 \\ 1 & 2 & 5 \end{bmatrix}
$$

The vector $x = (0, 1, 0)$ breaks it:

$$
\begin{bmatrix} 0 & 1 & 0 \end{bmatrix} \begin{bmatrix} 4 & 1 & 1 \\ 1 & 0 & 2 \\ 1 & 2 & 5 \end{bmatrix} \begin{bmatrix} 0 \\ 1 \\ 0 \end{bmatrix} = 0
$$

Choosing $e_2$ isolates $s_{22} = 0$. Positive definiteness requires $x^T S x > 0$ for *all* non-zero $x$, and we produced a non-zero $x$ giving $0$, so $S$ fails.

**Takeaway:** the problem calls out the main diagonal because the diagonal is where a matrix is easiest to break. You never had to compute an eigenvalue.

### The counterexample: not sufficient

Positive diagonals do **not** imply positive definiteness:

$$
M = \begin{bmatrix} 1 & 5 \\ 5 & 1 \end{bmatrix}
$$

Both diagonal entries are $1 > 0$. But

$$
\det(M) = (1)(1) - (5)(5) = -24 < 0,
$$

and since the determinant is the product of the eigenvalues, at least one eigenvalue is negative. $M$ is not positive definite.

**Takeaway:** positive diagonals only certify that the bowl curves up along the coordinate axes. Positive definiteness is a claim about *every conceivable direction*. When the off-diagonal entries (the interactions) are large relative to the diagonal, they overpower the system: the surface curves up along North/South and East/West but plunges downwards on the diagonal between them, which is a saddle, not a bowl. **The diagonal must dominate the off-diagonal for the surface to curve up everywhere.**

### Problem 19: a diagonal entry cannot undercut every eigenvalue

The completed statement:

> "A diagonal entry $s_{jj}$ of a symmetric matrix cannot be smaller than all the $\lambda$'s. If it were, then $S - s_{jj}I$ would have **positive** eigenvalues and would be positive definite. But $S - s_{jj}I$ has a **zero** on the main diagonal, impossible by Problem 18."

Proof by contradiction, in three moves:

1. **Shift the eigenvalues.** Suppose $s_{jj}$ *is* strictly smaller than every eigenvalue $\lambda$ of $S$. Shifting a matrix shifts its spectrum: $S - cI$ has eigenvalues $\lambda - c$. So $S - s_{jj}I$ has eigenvalues $\lambda - s_{jj}$, all strictly positive by our assumption. A symmetric matrix with all positive eigenvalues is positive definite.
2. **Shift the diagonal.** Subtracting $s_{jj}I$ subtracts $s_{jj}$ from every diagonal entry. The $j$th one becomes $s_{jj} - s_{jj} = 0$. So $S - s_{jj}I$ carries a zero on its main diagonal.
3. **Collide.** $S - s_{jj}I$ is positive definite *and* has a zero on the diagonal, which Problem 18 forbids. The assumption is false.

**Takeaway:** the shift $S - cI$ is the lever. It moves the spectrum and the diagonal in lockstep, letting a fact about diagonals (Problem 18) constrain the eigenvalues.

### The general fact behind Problem 19

Problem 19's use of positive definiteness is a teaching device to manufacture an easy contradiction. The real theorem needs only symmetry, and the Rayleigh quotient proves it in two lines. Take $x = e_j$:

- the denominator $e_j^T e_j = 1$, the squared length of a basis vector;
- the numerator $e_j^T S e_j = s_{jj}$, by the extraction property.

So $\lambda_{\min} \le \frac{x^T S x}{x^T x} \le \lambda_{\max}$ becomes

$$
\lambda_{\min} \le s_{jj} \le \lambda_{\max}.
$$

**Takeaway:** the bounding effect is a universal property of *symmetry*, not of definiteness. Problem 19 proves one half of it the hard way.

### Problem 28: the Rayleigh quotient maximum is $\lambda_{\max}$

The note attached to problem 28 drops multivariable calculus in without warning. It is deriving a foundational optimization theorem: **the maximum of the Rayleigh quotient is the largest eigenvalue.**

**1. Set up the constrained problem.** Scaling $x$ leaves $\frac{x^T S x}{x^T x}$ unchanged, since the factors cancel top and bottom. So lock $\lVert x \rVert = 1$ and the problem becomes:

- maximize $f(x) = x^T S x$
- subject to $g(x) = x^T x = 1$ (i.e. $x$ lies on the unit sphere).

**2. Form the Lagrangian.** Fold objective and constraint together with a multiplier $\lambda$:

$$
\mathcal{L}(x, \lambda) = x^T S x - \lambda (x^T x - 1)
$$

This is the bracketed expression in the textbook's note.

**3. Differentiate and set to zero.** For symmetric $S$, the gradient of $x^T S x$ is $2Sx$; the gradient of $x^T x$ is $2x$. So

$$
\frac{\partial \mathcal{L}}{\partial x} = 2Sx - 2\lambda x = 0 \quad \Longrightarrow \quad Sx = \lambda x.
$$

**4. Notice what happened.** We set out to maximize energy on a sphere and *fell straight back into the eigenvalue equation*. The critical points of $x^T S x$ on the unit sphere occur exactly at the eigenvectors of $S$, and the Lagrange multiplier $\lambda$ is literally the eigenvalue.

**5. Evaluate.** At a critical point, $Sx = \lambda x$, so

$$
x^T (Sx) = x^T(\lambda x) = \lambda(x^T x) = \lambda,
$$

using the constraint $x^T x = 1$. The quadratic form at an eigenvector equals its eigenvalue. To maximize, take the largest one: $\lambda_{\max}$.

**Takeaway:** this closes the loop. The Rayleigh bound says the quotient never exceeds $\lambda_{\max}$; this proves the bound is tight and tells you exactly where it is attained.

## Pitfalls

- **Necessary $\neq$ sufficient.** A positive diagonal never certifies positive definiteness. $\begin{bmatrix} 1 & 5 \\ 5 & 1 \end{bmatrix}$ is the reminder.
- **The bound needs symmetry, not definiteness.** Do not file $\lambda_{\min} \le s_{jj} \le \lambda_{\max}$ under positive definite matrices; it is a symmetry fact. Filing it too narrowly is exactly the misreading Problem 19 invites.
- **Symmetry is doing real work in the shift argument.** "All eigenvalues positive $\Rightarrow$ positive definite" is false without symmetry.
- **A zero on the diagonal only kills strict definiteness.** Such a matrix may still be positive *semi*-definite; the covariance reading (a variable with zero variance) is the intuition.
- **Lagrange multipliers find critical points, not maxima.** Problem 28's derivation returns every eigenvector — minima and saddles included. The maximum is identified afterwards, by comparing $\lambda$ values.

## Connections

- [[Home]]
- [[I.7 - Tests for Positive Definiteness]] gives Test 1 and Test 2, which the arguments here lean on.
- [[I.7 - The Crucial Matrix ATCA]] is the same energy-test-plus-substitution move from Problem 23.
- [[I.7 - Positive Definite Matrices and the Hessian]] carries the curvature reading of the diagonal.
- [[I.6 - Eigenvalues of Orthogonal and Symmetric Matrices]] for real eigenvalues of symmetric matrices, assumed throughout.
- Later uses: the Rayleigh quotient gets its own treatment in I.10; the maximization argument is the engine under PCA and spectral clustering, where the top eigenvector *is* the answer, no grid search required.

## Sources

- [[2026-07-10 Positive Definite Matrix Diagonal Properties]]

## Open Questions

- The Rayleigh bound $\lambda_{\min} \le \frac{x^T S x}{x^T x} \le \lambda_{\max}$ was quoted, not proved. Prove it via $S = Q \Lambda Q^T$: in eigenvector coordinates the quotient is a weighted average of the eigenvalues.
- How much can the diagonal dominate the off-diagonal before definiteness breaks? (Look up: diagonal dominance as a sufficient condition.)
- What do the *intermediate* eigenvalues maximize? (Look up: the Courant-Fischer min-max theorem.)
