---
title: Eigenvalues of Orthogonal and Symmetric Matrices
book: Linear Algebra and Learning from Data
part: I
section: I.6 Eigenvalues and Eigenvectors
pages:
status: seedling
created: 2026-06-16
tags: [type/topic, status/seedling, part/1, section/I-6, eigenvalues, eigenvectors, orthogonal-matrices, symmetric-matrices, normal-matrices, similar-matrices, change-of-basis, diagonalization, markov-matrices, stochastic-matrices, steady-state, complex-eigenvalues, differential-equations]
related: ["[[Part I MOC]]", "[[2026-06-16 Orthogonal Matrices and Eigenvalues]]"]
sources: ["[[2026-06-16 Orthogonal Matrices and Eigenvalues]]"]
---

# Eigenvalues of Orthogonal and Symmetric Matrices

## Summary

Orthogonal matrices preserve length, but that does **not** force every eigenvalue to be $1$. It forces every eigenvalue to have magnitude $1$, so eigenvalues of a real orthogonal matrix lie on the complex unit circle.

The special case "orthogonal and symmetric" is much more rigid: its eigenvalues can only be $+1$ and $-1$, so geometrically it acts like a reflection across a subspace.

## Key Results

### Orthogonal matrices preserve eigenvalue magnitude

If $Q$ is orthogonal, then

$$
Q^TQ = I.
$$

This means $Q$ preserves vector lengths:

$$
\|Qx\| = \|x\|.
$$

If $x$ is an eigenvector with eigenvalue $\lambda$, then $Qx = \lambda x$. Compare lengths:

$$
\|Qx\| = \|\lambda x\| = |\lambda|\|x\|.
$$

But orthogonality also gives $\|Qx\| = \|x\|$. Since $x \ne 0$,

$$
|\lambda| = 1.
$$

So the eigenvalues of an orthogonal matrix are not necessarily $1$; they are on the unit circle:

$$
\lambda = e^{i\theta}.
$$

For a real matrix, non-real complex eigenvalues come in conjugate pairs:

$$
e^{i\theta}, \quad e^{-i\theta}.
$$

### Symmetric plus orthogonal means only +1 and -1

If $A$ is symmetric, its eigenvalues are real. If $A$ is also orthogonal, its eigenvalues have magnitude $1$. Real numbers with magnitude $1$ are only:

$$
\lambda = 1 \quad \text{or} \quad \lambda = -1.
$$

Therefore a symmetric orthogonal matrix has eigenvalues only in $\{1,-1\}$.

It also satisfies:

$$
A^2 = I.
$$

This is called an **involution**: applying the transformation twice brings every vector back to where it started.

### Determinant and trace are not special to symmetric matrices

For any square matrix, not just real symmetric matrices:

$$
\det(A) = \prod_i \lambda_i
$$

and

$$
\operatorname{trace}(A) = \sum_i \lambda_i,
$$

where eigenvalues are counted with algebraic multiplicity. If the matrix has real entries, complex eigenvalues appear in conjugate pairs, so the determinant and trace remain real.

### Similar matrices are the same transformation in a new basis

Similar matrices have the form

$$
BAB^{-1}.
$$

Read the operations from right to left:

1. $B^{-1}$ translates the input vector from the original coordinate system into a new coordinate system.
2. $A$ applies the transformation in that new coordinate system.
3. $B$ translates the result back into the original coordinate system.

So $A$ and $BAB^{-1}$ represent the same underlying geometric action, but described in different coordinates.

This explains why similar matrices have the same eigenvalues. Eigenvalues measure the amount of stretching or flipping in an eigenvector direction. Changing coordinates changes how we describe the direction, but it does not change the actual amount of stretch.

Eigenvectors do change. If

$$
Ax = \lambda x,
$$

then

$$
(BAB^{-1})(Bx) = B A x = B(\lambda x) = \lambda (Bx).
$$

So $Bx$ is the corresponding eigenvector of $BAB^{-1}$.

This is also the geometric heart of diagonalization. The standard coordinate system may be poorly aligned with the natural directions of $A$. A good change of basis lines the axes up with eigenvectors, turning a complicated matrix into a simpler triangular or diagonal one. In that basis, the eigenvalues become visible on the main diagonal.

### Normal matrices and orthogonal eigenvectors

The clean general rule is:

$$
A^*A = AA^*
$$

where $A^*$ is the conjugate transpose. Matrices satisfying this are called **normal**.

Normal matrices are exactly the matrices that can be diagonalized by an orthonormal basis of eigenvectors over the complex numbers:

$$
A = U\Lambda U^*
$$

where $U$ is unitary.

Important examples:

- Real symmetric matrices are normal because $A^T = A$.
- Orthogonal matrices are normal because $Q^T = Q^{-1}$, so $Q^TQ = QQ^T = I$.
- A real orthogonal matrix may need complex eigenvectors. A plane rotation is the standard example.

### Markov matrices conserve total probability

A **Markov matrix**, often called a stochastic matrix or transition matrix, is a square matrix used to model dynamic systems that jump from one state to another over discrete steps in time. It is the mathematical engine behind a Markov chain.

In these systems, the crucial rule is that the next state depends only on the current state, completely ignoring the past.

For a standard **column-stochastic** Markov matrix, two rules matter:

1. All entries are probabilities: every entry is a non-negative real number between $0$ and $1$.
2. Every column sums to $1$.

To visualize this, imagine each column as the current state of the system, and each row as a possible next state. The numbers in a column are the probabilities of moving from that current state to each next state. Since the system must end up somewhere in the next time step, those probabilities must add to $1$.

Markov matrices fit beautifully into the eigenvalue story because they describe systems where total probability is conserved. Nothing should explode to infinity, and nothing should disappear.

Every Markov matrix has

$$
\lambda = 1
$$

as an eigenvalue. The corresponding eigenvector represents a **steady state** or equilibrium distribution. Since

$$
Ax = 1x,
$$

multiplying by the matrix leaves that vector unchanged. It is a distribution that remains stable as time passes.

All other eigenvalues have magnitude less than or equal to $1$. When they are strictly less than $1$, they represent temporary, transient behavior. Under repeated multiplication,

$$
A^n,
$$

those components shrink because $\lambda^n \to 0$ when $|\lambda| < 1$. What remains is the steady-state component attached to $\lambda = 1$.

This is the discrete-time version of the same theme that appears in differential equations: eigenvalues control which parts of a system persist, decay, grow, or oscillate.

### Differential equations use eigenvalues as growth rates

This is the continuous-time version of studying repeated matrix powers. In discrete time, a system evolves by repeated multiplication:

$$
u_k = A^k u_0.
$$

Eigenvalues then appear as powers $\lambda^k$. In continuous time, the derivative equation replaces the step-by-step update, and the matrix exponential replaces $A^k$:

$$
u(t) = e^{At}u(0).
$$

Eigenvalues appear as exponentials $e^{\lambda t}$. This is the same eigenvector idea, but with time flowing continuously instead of in integer steps.

For a system

$$
\frac{du}{dt} = Au,
$$

if $A$ has a full set of eigenvectors $x_1,\dots,x_n$, write the initial condition as

$$
u(0) = c_1x_1 + \cdots + c_nx_n.
$$

Then the solution is

$$
u(t) = c_1e^{\lambda_1t}x_1 + \cdots + c_ne^{\lambda_nt}x_n.
$$

Each eigenvector evolves independently, and its eigenvalue controls the exponential factor attached to it.

For a complex eigenvalue

$$
\lambda = a + ib,
$$

the exponential splits as

$$
e^{\lambda t} = e^{(a+ib)t} = e^{at}e^{ibt}.
$$

- $e^{at}$ controls growth or decay.
- $e^{ibt}$ controls oscillation, since $e^{ibt} = \cos(bt) + i\sin(bt)$.

So the real part of $\lambda$ controls whether the system grows, decays, or stays bounded; the imaginary part controls rotation or oscillation.

## Intuition

An orthogonal matrix is a rigid motion fixing the origin: it may rotate, reflect, or combine rotations and reflections, but it cannot stretch. Eigenvectors are directions that the matrix sends back into the same line. If the matrix cannot stretch anything, the eigenvalue attached to such a direction cannot have magnitude other than $1$.

For real eigenvectors, that leaves only two possibilities:

- $\lambda = 1$: the vector is fixed.
- $\lambda = -1$: the vector is flipped.

Complex eigenvalues appear when the matrix rotates a real plane without leaving any real line inside that plane fixed. The eigenvectors then live naturally in complex space.

Similar matrices add another layer to this picture: sometimes the transformation is simple, but the coordinate system hides that simplicity. The matrix $B$ is a change of language. It lets us move into coordinates where the action is easier to see, apply the action there, then translate back.

Markov matrices give a different kind of intuition: eigenvalue $1$ means a probability distribution can remain steady, while eigenvalues with $|\lambda| < 1$ describe transient modes that fade as the chain is multiplied forward in time.

For a symmetric orthogonal matrix, there is no rotation part. The space splits into two perpendicular pieces:

- the $+1$ eigenspace, where vectors are unchanged;
- the $-1$ eigenspace, where vectors are reversed.

That is exactly the geometry of reflection across the $+1$ eigenspace.

## Worked Examples

### Rotation matrix

A two-dimensional rotation by angle $\theta$ is

$$
Q =
\begin{bmatrix}
\cos\theta & -\sin\theta \\
\sin\theta & \cos\theta
\end{bmatrix}.
$$

It is orthogonal, so its eigenvalues must have magnitude $1$. They are

$$
\lambda_1 = e^{i\theta}, \qquad \lambda_2 = e^{-i\theta}.
$$

Unless $\theta = 0$ or $\theta = \pi$, there are no real eigenvectors. Geometrically, every real direction is rotated into a different direction.

### Reflection matrix

Reflection across the $x$-axis is

$$
R =
\begin{bmatrix}
1 & 0 \\
0 & -1
\end{bmatrix}.
$$

This matrix is both symmetric and orthogonal. Its eigenvalues are $1$ and $-1$.

- Vectors on the $x$-axis are unchanged: $R\begin{bmatrix}1\\0\end{bmatrix} = \begin{bmatrix}1\\0\end{bmatrix}$.
- Vectors on the $y$-axis are flipped: $R\begin{bmatrix}0\\1\end{bmatrix} = -\begin{bmatrix}0\\1\end{bmatrix}$.

Applying the reflection twice gives the identity:

$$
R^2 = I.
$$

## Pitfalls

- Length preservation means $|\lambda|=1$, not $\lambda=1$.
- A real orthogonal matrix may not have real eigenvectors. Rotations often require complex eigenvectors.
- Repeated eigenvalues do not guarantee enough independent eigenvectors. A matrix with missing eigenvectors is **defective** and cannot be diagonalized in the ordinary eigenvector basis.
- Eigenvalues of $A+B$ are not generally the eigenvalues of $A$ plus the eigenvalues of $B$.
- Eigenvalues of $AB$ are not generally obtained by multiplying eigenvalues of $A$ and $B$ one by one.
- Similar matrices have the same eigenvalues, but not the same eigenvectors. The eigenvectors are translated by the change-of-basis matrix.
- For column-stochastic Markov matrices, columns sum to $1$ because each column lists all possible next-state probabilities from one current state.
- Markov matrices always have $\lambda = 1$, but convergence to a single steady state can require extra conditions such as irreducibility and aperiodicity.
- The trace and determinant formulas apply to every square matrix, not just symmetric matrices.
- For $du/dt = Au$, the simple formula using eigenvectors assumes a full eigenvector basis. Defective matrices require generalized eigenvectors or Jordan form.

## Connections

- [[Part I MOC]]
- [[I.5 Orthogonal Matrices and Subspaces]]
- [[Symmetric Matrices]]
- [[Normal Matrices]]
- [[Similar Matrices]]
- [[Change of Basis]]
- [[Diagonalization]]
- [[Markov Matrices]]
- [[Steady State]]
- [[Differential Equations from Eigenvalues]]
- [[Singular Value Decomposition]]

## Sources

- [[2026-06-16 Orthogonal Matrices and Eigenvalues]]

## Open Questions

- How does Strang define and use normal matrices in this section?
- How does the book connect similar matrices to triangularization and diagonalization?
- What additional assumptions guarantee that a Markov chain converges to a unique steady state?
- How do real rotation blocks appear when a real orthogonal matrix is diagonalized over the complex numbers?
- What is the cleanest bridge from this section to the singular value decomposition later in the book?
