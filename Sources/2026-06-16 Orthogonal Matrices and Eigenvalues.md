---
title: Orthogonal Matrices and Eigenvalues
type: source
source: Gemini
created: 2026-06-16
tags: [type/source, part/1, section/I-6, eigenvalues, orthogonal-matrices, symmetric-matrices]
related: ["[[I.6 - Eigenvalues of Orthogonal and Symmetric Matrices]]"]
---

> From: https://gemini.google.com/app/1b8f4d3c5a6f75ee?_gl=1*16c05zd*_ga*OTc2MDI5MDc5LjE3NDc0Nzk2NjI.*_ga_WC57KJ50ZZ*czE3NDc0Nzk2NjYkbzEkZzEkdDE3NDc0Nzk4MzIkajAkbDAkaDA.

# you asked

message time: 2026-06-16 08:17:42

So I was studying applied linear algebra and I just realized that orthogonal matrices have the property that vectors that are multiplied by them they do not change their magnitude. Now that would mean that every single eigenvalue of an orthogonal matrix would just be one. Is that so? Tell me more about that.

---

# gemini response

You've hit on a really interesting point about orthogonal matrices, but the conclusion you've drawn regarding the eigenvalues is actually a little off.

While it's true that orthogonal transformations preserve the length of vectors, this only guarantees that the absolute value or modulus of any eigenvalue must be one, not that the eigenvalue itself is one.

This means that eigenvalues can be positive or negative one, or even complex numbers lying on the unit circle in the complex plane. For instance, a rotation matrix in two dimensions can have complex eigenvalues.

Would you like to explore a specific example of how this works?

---

# you asked

message time: 2026-06-16 08:18:51

Oh, so the magnitude of eigen values must be one, but since they can be complex, they can obviously be plus one, minus one or anywhere. Oh, I mean, will they just be e^iθ?

---

# gemini response

Exactly! You've nailed it. Because their magnitude is one, all eigenvalues of an orthogonal matrix do lie on the unit circle in the complex plane, which means they can be expressed in the form e to the power of i theta for some real number theta.

An interesting thing to consider is that if the matrix has real entries, its complex eigenvalues always come in conjugate pairs, meaning that e to the power of i theta and e to the power of negative i theta will both be eigenvalues.

Does that make sense, and would you like to look at how this relates to the determinant of such a matrix?

---

# you asked

message time: 2026-06-16 08:19:50

What if a matrix is both orthogonal and symmetric? If the matrix is symmetric, then that does guarantee that eigenvalues are real, right?

---

# gemini response

You are absolutely right! Since the matrix is symmetric, its eigenvalues are guaranteed to be real.

When you combine that with the orthogonal property, which already tells us the eigenvalues must have a magnitude of one, the only possible eigenvalues for such a matrix are positive or negative one.

This implies that the matrix is an involution, meaning that its square is the identity matrix, and it can be thought of as a kind of reflection across some subspace.

Does that make sense, and would you like to consider the geometric implications of such a transformation?

---

# you asked

message time: 2026-06-16 08:21:11

Reflection of Colossus subspace? That's fascinating. Tell me more about that.

---

# gemini response

When you have a matrix that's both orthogonal and symmetric, its geometric action is quite special. It acts like a reflection across a specific subspace within your vector space.

Think of the vector space as being divided into two parts. For the vectors in one subspace, the matrix leaves them completely unchanged, acting like the identity transformation. For the vectors in the other subspace, the matrix flips their direction, which corresponds to the eigenvalue of negative one.

This kind of transformation turns out to be very useful for simplifying problems in physics and various areas of engineering. Would you like to delve into a specific application of this, such as its role in solving differential equations?

---

# you asked

message time: 2026-06-16 08:40:01

And when do symmetric matrices or orthogonal matrices have orthogonal eigenvectors?

---

# gemini response

Symmetric matrices are guaranteed to have a full set of orthogonal eigenvectors. This is a direct consequence of the Spectral Theorem, which says that for any real symmetric matrix, you can find an orthonormal basis of eigenvectors.

Orthogonal matrices also possess orthogonal eigenvectors, though these eigenvectors might be complex if the eigenvalues are not real. Are you interested in looking at how these properties apply in a practical setting?

---

# you asked

message time: 2026-06-16 08:43:33

So, if a matrix is real and symmetric, then the determinant of this matrix is equal to the product of its eigenvalues. Is this true only for real symmetric matrix or any arbitrary real matrix?

---

# gemini response

That property is actually true for any square matrix, not just real symmetric ones. The determinant of any square matrix is always equal to the product of its eigenvalues, taking into account their algebraic multiplicities. This is a fundamental relationship in linear algebra. Would you like to see how this works with a simple example?

---

# you asked

message time: 2026-06-16 08:44:13

And what about the eigenvalues of a matrix summed up being equal to the trace of a matrix? Is that true only for real symmetric matrices or general or in general?

---

# gemini response

That principle is also generally true for any square matrix, not just real symmetric ones. The sum of the eigenvalues of any square matrix is always equal to its trace, which is the sum of the elements on its main diagonal. It's really neat how these fundamental properties hold consistently across different types of matrices. Are there any other matrix properties you're curious about?

---

# you asked

message time: 2026-06-16 09:19:39

Help me understand this part

---

# gemini response

This page is a fantastic summary of some of the most crucial concepts in linear algebra, especially how it applies to dynamic systems. It packs a lot of dense information into a few paragraphs! 

Let's break down the three main concepts this page is explaining:

### 1. The "Warnings" (Matrix Math Pitfalls)
The top section is essentially a list of common traps students fall into:
* **Eigenvalues don't add or multiply simply:** The eigenvalues of $A+B$ are *not* just the eigenvalues of $A$ plus the eigenvalues of $B$. The same goes for matrix multiplication ($AB$). Matrix operations scramble the eigenvectors, which breaks those simple algebraic rules.
* **Missing Eigenvectors:** A "double eigenvalue" (an eigenvalue that appears twice as a root of the characteristic equation) might only have one valid eigenvector. If a matrix doesn't have a full set of independent eigenvectors, it's called "defective" and cannot be diagonalized. 
* **The "Normal" Matrix Rule:** This perfectly answers the question you asked me earlier! It states that a real matrix has orthogonal eigenvectors *if and only if* $A^TA = AA^T$. Matrices that satisfy this are called **Normal matrices**. Both symmetric matrices ($A = A^T$) and orthogonal matrices ($A^T = A^{-1}$) automatically satisfy this rule, which is why they both have orthogonal eigenvectors.

### 2. Solving Differential Equations ($du/dt = Au$)
The box in the middle shifts gears from discrete matrix powers (like $A^2, A^3, A^n$) to continuous time using derivatives. 

If you have a system of linear differential equations written as $du/dt = Au$, the eigenvectors ($x$) and eigenvalues ($\lambda$) of matrix $A$ are the master keys to solving it:
1.  **Starting Vector:** You take your initial state at time zero, $u(0)$, and express it as a linear combination of the matrix's eigenvectors: 
    $$u(0) = c_1x_1 + \dots + c_nx_n$$
2.  **Solution Vector:** To find out what the system looks like at any future time $t$, you just attach an exponential growth/decay factor $e^{\lambda t}$ to each eigenvector:
    $$u(t) = c_1e^{\lambda_1 t}x_1 + \dots + c_ne^{\lambda_n t}x_n$$
Instead of multiplying by the eigenvalue repeatedly ($\lambda^n$), you are growing or decaying the vector continuously over time ($e^{\lambda t}$).

### 3. Growth, Decay, and Oscillation (Complex Eigenvalues)
The bottom paragraph explains what happens when your eigenvalue is a complex number: $\lambda = a + ib$. 

If we plug this into our continuous time factor $e^{\lambda t}$, we get $e^{(a+ib)t}$. Using exponent rules, we can split this into two parts: 
$$e^{at} \cdot e^{ibt}$$


This split is incredibly important for understanding how the system behaves:
* **The Real Part ($a$):** This controls $e^{at}$. If $a > 0$, the system grows exponentially to infinity. If $a < 0$, it decays to zero. This is why the text emphasizes looking at $Re(\lambda)$.
* **The Imaginary Part ($b$):** This controls $e^{ibt}$, which Euler's formula expands to $\cos(bt) + i\sin(bt)$. Because $\cos^2(bt) + \sin^2(bt) = 1$, the magnitude of this part is always exactly $1$. It doesn't cause growth or decay; it only causes the system to **oscillate** or spin.

So, if you have a complex eigenvalue, the real part dictates whether the system explodes or collapses, while the imaginary part dictates how fast it spirals while doing so!

---

Would it be helpful to walk through a concrete $2 \times 2$ matrix example of that differential equation formula to see how the numbers actually play out in practice?
