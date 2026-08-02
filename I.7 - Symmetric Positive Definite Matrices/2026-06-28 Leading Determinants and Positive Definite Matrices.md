---
title: Leading Determinants and Positive Definite Matrices
type: source
source: Gemini
created: 2026-06-28
tags: [type/source, part/1, section/I-7, positive-definite, determinants]
related: ["[[I.7 - Positive Definite Matrices and the Hessian]]"]
---

> From: https://gemini.google.com/app/ac326b2be52faeb5?_gl=1*16c05zd*_ga*OTc2MDI5MDc5LjE3NDc0Nzk2NjI.*_ga_WC57KJ50ZZ*czE3NDc0Nzk2NjYkbzEkZzEkdDE3NDc0Nzk4MzIkajAkbDAkaDA.

# you asked

message time: 2026-06-28 11:27:40

What are leading determinants? Explain test 4 in details please

---

# gemini response

## What are Leading Determinants?

Leading determinants (often referred to mathematically as **leading principal minors**) are the determinants of the square submatrices located in the top-left corner of a larger matrix. 

If you have an $n \times n$ matrix $S$, you find its leading determinants by looking at successively larger chunks of the matrix, starting from the top-left:
* $D_1$ is the determinant of the top-left $1 \times 1$ block.
* $D_2$ is the determinant of the top-left $2 \times 2$ block.
* $D_k$ is the determinant of the top-left $k \times k$ block, continuing until you reach $D_n$, which is the determinant of the entire matrix.

### Visualizing the Example

Let's break down the $4 \times 4$ symmetric "second difference matrix" shown at the top of page 48 to see exactly how these are calculated. 

$$S = \begin{bmatrix} 2 & -1 & 0 & 0 \\ -1 & 2 & -1 & 0 \\ 0 & -1 & 2 & -1 \\ 0 & 0 & -1 & 2 \end{bmatrix}$$

The text uses nested boxes to isolate these top-left sections:

* **1st determinant ($D_1$):** Look at only the first row and first column.
    $$\begin{bmatrix} 2 \end{bmatrix} \rightarrow D_1 = 2$$
* **2nd determinant ($D_2$):** Look at the intersection of the first two rows and columns.
    $$\begin{bmatrix} 2 & -1 \\ -1 & 2 \end{bmatrix} \rightarrow (2)(2) - (-1)(-1) = 3 \rightarrow D_2 = 3$$
* **3rd determinant ($D_3$):** Look at the intersection of the first three rows and columns.
    $$\begin{bmatrix} 2 & -1 & 0 \\ -1 & 2 & -1 \\ 0 & -1 & 2 \end{bmatrix} \rightarrow D_3 = 4$$
* **4th determinant ($D_4$):** The determinant of the entire $4 \times 4$ matrix. 
    $$D_4 = 5$$

---

## Explaining Test 4 (The Determinant Test)

**Test 4** is a simple, mechanical check to figure out if a symmetric matrix is **positive definite**. 

The test states: **A symmetric matrix $S$ is positive definite if and only if all of its leading determinants ($D_1, D_2, \dots, D_n$) are strictly positive (greater than zero).**

In the textbook's example, our leading determinants are 2, 3, 4, and 5. Because every single one of these numbers is positive, the matrix passes Test 4. Therefore, we know for a fact that $S$ is a positive definite matrix. 

### Why Test 4 Works: The Link to Pivots

The text bridges Test 4 (determinants) with Test 5 (pivots) to explain *why* this works. When you perform elimination on a matrix to find its pivots (the first non-zero entry in each row after elimination), the math reveals a direct relationship between the pivots and the leading determinants:

$$\text{The } k\text{th pivot} = \frac{D_k}{D_{k-1}}$$

For a matrix to be positive definite, all of its pivots must be positive (this is Test 5). Because every pivot is calculated by dividing one leading determinant by the previous one, **if all your leading determinants are positive, all your pivots are guaranteed to be positive too** (since a positive divided by a positive is always positive). 

The determinant test is often favored for smaller matrices because calculating a few small determinants by hand is usually faster than running through the full Gaussian elimination process required to find the pivots.

---

# you asked

message time: 2026-06-28 11:33:38

But then the pivot test. Can we prove it?

---

# gemini response

Yes, we can absolutely prove it! To prove the pivot test, we have to show two things:
1. If all the pivots are positive, the matrix is positive definite.
2. If the matrix is positive definite, all the pivots must be positive.

The secret to proving this lies entirely in the matrix factorization shown on the second page you uploaded: **$S = LDL^T$**.

Here is the step-by-step mathematical proof.

### The Foundation: $S = LDL^T$ Factorization
When you perform standard Gaussian elimination on a symmetric matrix $S$ (without row exchanges), you factor it into $S = LU$, where $L$ is a lower triangular matrix and $U$ is an upper triangular matrix. 

Because $S$ is symmetric, we can split $U$ further to pull out the pivots. We get:
$$S = LDL^T$$

* **$L$** is a lower triangular matrix with **$1$s on its main diagonal**.
* **$D$** is a diagonal matrix, and its diagonal entries ($d_1, d_2, \dots, d_n$) are exactly the **pivots** of $S$.
* **$L^T$** is the transpose of $L$ (making it upper triangular, also with $1$s on the diagonal).

### Connecting Pivots to the "Energy Test"
The definition of a positive definite matrix (Test 2 in your book) is that its "energy" $x^T S x$ must be strictly greater than zero for any non-zero vector $x$.

Let's substitute our $LDL^T$ factorization into the energy equation:
$$x^T S x = x^T (LDL^T) x$$

Because matrix multiplication is associative, we can group this differently:
$$x^T S x = (x^T L) D (L^T x)$$

Now, let's create a new vector $y$ and define it as $y = L^T x$. 
By the rules of transposes, $(L^T x)^T = x^T L$, which means $y^T = x^T L$. Substituting $y$ into our equation gives us a beautiful simplification:
$$x^T S x = y^T D y$$

Because $D$ is just a diagonal matrix containing the pivots, expanding $y^T D y$ results in a simple sum of squares multiplied by the pivots:
$$x^T S x = d_1 y_1^2 + d_2 y_2^2 + \dots + d_n y_n^2$$

This equation is the key to proving both directions of the test.

---

### Part 1: Proving Positive Pivots $\rightarrow$ Positive Definite
**Assumption:** All pivots are positive ($d_i > 0$).
**Goal:** Show that $x^T S x > 0$ for any non-zero vector $x$.

1. Look at our energy equation: $x^T S x = d_1 y_1^2 + d_2 y_2^2 + \dots + d_n y_n^2$.
2. Because any real number squared is positive (or zero), $y_1^2, y_2^2, \dots$ are all $\ge 0$.
3. Since we assume all pivots ($d_i$) are strictly $> 0$, every term in that sum is positive or zero.
4. Because $L$ has $1$s on its diagonal, its determinant is $1$. This means $L^T$ is an invertible matrix. Therefore, if $x$ is not the zero vector, $y = L^T x$ **cannot** be the zero vector either.
5. Since $y$ is not all zeros, at least one $y_i^2$ is strictly positive.
6. Therefore, the entire sum $d_1 y_1^2 + \dots + d_n y_n^2$ must be strictly greater than zero.

**Conclusion:** $x^T S x > 0$. The matrix is positive definite.

---

### Part 2: Proving Positive Definite $\rightarrow$ Positive Pivots
**Assumption:** The matrix is positive definite ($x^T S x > 0$ for all $x \neq 0$).
**Goal:** Show that all pivots are positive ($d_i > 0$).

1. We know that $x^T S x = d_1 y_1^2 + d_2 y_2^2 + \dots + d_n y_n^2$ must be $> 0$ for any non-zero $x$.
2. Since $L^T$ is invertible, for any vector $y$ we can dream up, there is a corresponding unique vector $x$ that makes $y = L^T x$.
3. Let's isolate the first pivot, $d_1$. We can deliberately choose an $x$ such that our resulting $y$ vector is $(1, 0, 0, \dots, 0)$. 
4. Plug this specific $y$ into our sum: 
   $$x^T S x = d_1(1)^2 + d_2(0)^2 + \dots + d_n(0)^2 = d_1$$
5. Because $S$ is positive definite, we know $x^T S x > 0$. Therefore, $d_1 > 0$.
6. You can repeat this logic for every single pivot. By choosing an $x$ that forces $y$ to be a $1$ in the $i$-th position and $0$ everywhere else, you isolate $d_i$. The positive definite rule guarantees that $d_i > 0$.

**Conclusion:** All pivots $d_i$ must be positive.

---

# you asked

message time: 2026-06-28 12:27:14

Is there an error on the second page. Look at the square roots

---

# gemini response

There is actually no error in the textbook! Gilbert Strang (the author) is completely correct here, but he skips a few algebraic simplification steps that make the transition look like a mistake at first glance.

What you are looking at is the **Cholesky factorization**, where the matrix is factored into $S = A^T A$. 

Here is the exact step-by-step breakdown of how he arrived at those specific square roots, proving the textbook's math is solid.

### The Setup: Splitting the Pivots
In the step just before the square roots, the book factors the matrix into $S = LDL^T$:

$$D = \begin{bmatrix} 2 & 0 & 0 \\ 0 & \frac{3}{2} & 0 \\ 0 & 0 & \frac{4}{3} \end{bmatrix}, \quad L^T = \begin{bmatrix} 1 & -\frac{1}{2} & 0 \\ 0 & 1 & -\frac{2}{3} \\ 0 & 0 & 1 \end{bmatrix}$$

To get the Cholesky factorization $S = A^T A$, we have to "share" the pivots in the diagonal matrix $D$ equally. We do this by taking the square root of $D$ and attaching it to $L^T$. 

Therefore, $A = \sqrt{D} L^T$.

The square root of a diagonal matrix is just the square root of its individual entries:
$$\sqrt{D} = \begin{bmatrix} \sqrt{2} & 0 & 0 \\ 0 & \sqrt{\frac{3}{2}} & 0 \\ 0 & 0 & \sqrt{\frac{4}{3}} \end{bmatrix}$$

### The "Missing" Algebra Step
Now, we multiply $\sqrt{D}$ and $L^T$ to find $A$:

$$A = \begin{bmatrix} \sqrt{2} & 0 & 0 \\ 0 & \sqrt{\frac{3}{2}} & 0 \\ 0 & 0 & \sqrt{\frac{4}{3}} \end{bmatrix} \begin{bmatrix} 1 & -\frac{1}{2} & 0 \\ 0 & 1 & -\frac{2}{3} \\ 0 & 0 & 1 \end{bmatrix}$$

When you do the matrix multiplication, you multiply the rows of the first matrix by the columns of the second. Here is where the "tricky" simplifications happen:

**1. Row 1, Column 2 of $A$:**
$$\sqrt{2} \cdot \left(-\frac{1}{2}\right) = -\frac{\sqrt{2}}{2}$$
If you rationalize this by dividing the top and bottom by $\sqrt{2}$, it simplifies to exactly what the book has: **$-\frac{1}{\sqrt{2}}$**.

**2. Row 2, Column 3 of $A$:**
$$\sqrt{\frac{3}{2}} \cdot \left(-\frac{2}{3}\right)$$
To simplify this, you can bring the $-\frac{2}{3}$ inside the square root by squaring it (which makes it $\frac{4}{9}$):
$$-\sqrt{\frac{3}{2} \cdot \frac{4}{9}} = -\sqrt{\frac{12}{18}}$$
Divide the top and bottom by 6, and you get exactly what the book has: **$-\sqrt{\frac{2}{3}}$**.

### Conclusion
If you plug those simplified terms back into the matrix $A$, you get:

$$A = \begin{bmatrix} \sqrt{2} & -\frac{1}{\sqrt{2}} & 0 \\ 0 & \sqrt{\frac{3}{2}} & -\sqrt{\frac{2}{3}} \\ 0 & 0 & \sqrt{\frac{4}{3}} \end{bmatrix}$$

This is a perfect match for the upper triangular matrix shown on the right side of the $A^T A$ equation in your book. It looks a bit wild, but the math checks out perfectly!

---

# you asked

message time: 2026-06-28 13:19:25

Here strang discusses the application of symmetric positive definite matrices to minimum problems. I see the connection, but not fully. Can you help me appreciate it in full?

---

# gemini response

It is one of the most satisfying "aha!" moments in mathematics when you realize that linear algebra and multivariable calculus are just speaking different dialects of the same language. Strang sets this up beautifully, but let's break down the translation so you can appreciate the full weight of what it means, especially when navigating high-dimensional spaces.

To fully grasp the connection, we have to scale up a simple concept from high school calculus into $n$-dimensional space.

### 1. The 1D Calculus Refresher
In single-variable calculus, if you want to find the minimum of a curve $f(x)$, you look for two things:
1.  **The First Derivative is Zero:** $f'(x_0) = 0$. This tells you the curve is flat at $x_0$. It's a critical point.
2.  **The Second Derivative is Positive:** $f''(x_0) > 0$. This tells you the curve is bending upwards (convex). 

If both are true, you are at the bottom of a bowl.

### 2. The High-Dimensional Translation
Now, imagine you aren't just moving along a single line, but navigating a massive, multi-dimensional landscape. Instead of a single variable $x$, you have a vector of variables. 

* **The First Derivative becomes the Gradient:** A vector of all the first partial derivatives. Setting it to zero means the landscape is perfectly flat in every direction at that specific point.
* **The Second Derivative becomes the Hessian Matrix ($H$):** A symmetric matrix containing all the second partial derivatives. 

Here is the conceptual leap: **How do you say a *matrix* is "greater than zero"?** You can't just look at the individual numbers inside the matrix. A matrix is "positive" if the fundamental geometry it represents curves upwards in every possible direction. In linear algebra, a matrix that behaves this way is called **Positive Definite**.

### 3. The Energy Connection (Why $x^T S x > 0$ matters)
To see *why* a positive definite Hessian guarantees a minimum, we look at the multi-dimensional Taylor expansion. If you are at a flat point (gradient is zero) and you take a tiny step in any direction (let's call that step vector $v$), the change in your function's height is determined almost entirely by the second derivative matrix $H$:

$$\text{Change in height} \approx \frac{1}{2} v^T H v$$

For that flat point to be a true minimum, *any* step you take away from it must increase your height. Therefore, the term $v^T H v$ must be strictly greater than zero for any non-zero step $v$. 

Does that equation look familiar? It is the exact definition of the "Energy Test" Strang introduces ($x^T S x > 0$). **Positive definite matrices are the linear algebra equivalent of a positive second derivative.**

### 4. The Geometry of the Landscape
Depending on the eigenvalues of that matrix, the geometry of your critical point changes completely:

* **All Positive Eigenvalues (Positive Definite):** The energy is positive in every direction. You are at the bottom of a strict bowl. 
* **All Negative Eigenvalues (Negative Definite):** The energy is negative in every direction. You are at the peak of a mountain.
* **Mixed Eigenvalues (Indefinite):** The energy goes up in some directions and down in others. 


This third scenario creates a **saddle point**. The gradient is zero, so it looks flat, but it curves up like a bowl on one axis and drapes down like a hill on another. 

### 5. Navigating the Real World
This isn't just theoretical elegance; it is the mathematical bedrock of training complex architectures like Transformers or diffusion models. 

When you define a loss function for a neural network, you are creating a chaotic, high-dimensional mountain range with millions or billions of parameters. Gradient descent is the process of blindly stepping downhill to minimize that loss. 

However, in deep learning, the gradient only tells you the slope. It doesn't tell you the curvature. A major problem in training is getting stuck at saddle points. The gradient becomes zero, and the model thinks it has found the solution (the minimum loss). But if the Hessian matrix of the loss function is *indefinite* at that point, the model is actually resting on a ledge, not at the bottom of the valley. 

If a function is strictly convex—meaning its second derivative matrix is symmetric positive definite everywhere—it is an optimization dream. It means the landscape is one giant, perfect bowl, and gradient descent is mathematically guaranteed to find the absolute global minimum without ever getting trapped.

How does visualizing the Hessian's eigenvalues as the curvature of a loss landscape change how you think about the optimization algorithms you use in practice?

---

# you asked

message time: 2026-06-28 16:35:51

Can you explain this application as well as you have the previous application

---

# gemini response

This is another brilliant geometric translation provided by Strang. In the previous section, we established that the "energy" of a positive definite matrix, $E = x^T S x$, creates a 3D landscape shaped like a perfect bowl opening upwards. 

Now, Strang is shifting the focus from the *bottom* of the bowl to its *cross-sections*. 

Here is how to decode this geometric application, which is formally known as the **Principal Axis Theorem**.

### 1. Slicing the Bowl
Imagine you are pouring water into this 3D energy bowl until the water level reaches exactly a height of 1. The surface of the water forms a 2D cross-section of the bowl. 

Mathematically, you are setting the energy equation to a constant:
$$x^T S x = 1$$

Because the matrix $S$ is positive definite (the bowl curves upwards in every direction), this cross-section will always be a closed loop. Specifically, it forms an **ellipse**.

If you look at the matrix $S = \begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}$, expanding $x^T S x = 1$ gives you the algebraic equation of this ellipse:
$$5x^2 + 8xy + 5y^2 = 1$$

### 2. The Problem with the "Tilt"
If you were to graph that equation on a standard $x$-$y$ grid (as seen on the left side of page 51), you would notice something annoying: the ellipse is tilted. 

The culprit behind this tilt is the **$8xy$ cross-term**. In linear algebra, whenever your off-diagonal elements in a symmetric matrix are non-zero (the $4$s in matrix $S$), your resulting geometric shape will be rotated relative to the standard coordinate axes. 

Working with tilted shapes is mathematically messy. We want to align the ellipse perfectly with our axes so it looks like the neat, upright ellipse on the right side of the page. 

### 3. The Solution: Eigendecomposition ($S = Q \Lambda Q^T$)
This is where the magic of eigenvectors and eigenvalues comes in. By factoring the matrix into $S = Q \Lambda Q^T$, we can completely untangle the tilt and the stretching of the ellipse.

* **The Eigenvectors ($Q$) dictate the DIRECTIONS:** The eigenvectors of a symmetric matrix are always orthogonal (perpendicular) to each other. They point exactly along the **principal axes** of the ellipse. In the book, $q_1$ and $q_2$ point perfectly along the longest and shortest diameters of the tilted shape. 
        By changing our coordinate system from the old $(x, y)$ to new coordinates $(X, Y)$ that line up with these eigenvectors, we effectively rotate our perspective so the ellipse sits straight up. The cross-term vanishes completely.

* **The Eigenvalues ($\Lambda$) dictate the LENGTHS:**
    Once the ellipse is straightened out, its new equation uses the eigenvalues ($\lambda_1 = 9$ and $\lambda_2 = 1$) as the coefficients:
    $$9X^2 + 1Y^2 = 1$$
    This is the exact same ellipse, just viewed from our new, perfectly aligned coordinate system!

### 4. The Counter-Intuitive Golden Rule
There is one beautiful, slightly counter-intuitive detail Strang highlights at the bottom of the page regarding the lengths of the axes. 

The half-length of an axis is equal to **$1 / \sqrt{\lambda}$**. 
This means there is an inverse relationship between the eigenvalue and the physical length of the ellipse:
* The **larger** eigenvalue ($\lambda_1 = 9$) corresponds to the **shorter** axis (length $= 1/\sqrt{9} = 1/3$).
* The **smaller** eigenvalue ($\lambda_2 = 1$) corresponds to the **longer** axis (length $= 1/\sqrt{1} = 1$).

**Why does this happen?** Think back to the 3D bowl. A large eigenvalue means the bowl curves upwards very steeply in that direction. Because it is so steep, it reaches the water level (height = 1) very quickly. Therefore, the distance from the center to the edge (the axis of the ellipse) is very short! A small eigenvalue means a shallow slope, so it takes a longer horizontal distance to reach a height of 1.

---

When you scale this up to $n$ dimensions, you are no longer dealing with a 2D ellipse, but an $n$-dimensional hyper-ellipsoid. The exact same rules apply: the eigenvectors define its orientation in high-dimensional space, and the eigenvalues dictate how far it stretches in each of those directions.

If you were to apply this concept of stretching and rotation to the spread of a massive dataset, how do you think these principal axes (eigenvectors) might help you identify the most important features in that data?