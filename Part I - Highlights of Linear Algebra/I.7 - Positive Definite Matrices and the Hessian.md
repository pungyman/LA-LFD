---
title: Positive Definite Matrices and the Hessian
book: Linear Algebra and Learning from Data
part: I
section: I.7 Positive Definite Matrices
pages:
status: seedling
created: 2026-06-28
tags: [type/topic, status/seedling, part/1, section/I-7, positive-definite-matrices, hessian, gradient, optimization, convexity, eigenvalues, saddle-points, principal-axis-theorem, ellipses]
related: ["[[Part I MOC]]"]
sources: []
---

# Positive Definite Matrices and the Hessian

It is one of the most satisfying "aha!" moments in mathematics when you realize that linear algebra and multivariable calculus are just speaking different dialects of the same language. Strang sets this up beautifully, but let's break down the translation so you can appreciate the full weight of what it means, especially when navigating high-dimensional spaces.

To fully grasp the connection, we have to scale up a simple concept from high school calculus into $n$-dimensional space.

## 1. The 1D Calculus Refresher

In single-variable calculus, if you want to find the minimum of a curve $f(x)$, you look for two things:

1. **The First Derivative is Zero:** $f'(x_0) = 0$. This tells you the curve is flat at $x_0$. It's a critical point.
2. **The Second Derivative is Positive:** $f''(x_0) > 0$. This tells you the curve is bending upwards (convex).

If both are true, you are at the bottom of a bowl.

## 2. The High-Dimensional Translation

Now, imagine you aren't just moving along a single line, but navigating a massive, multi-dimensional landscape. Instead of a single variable $x$, you have a vector of variables.

- **The First Derivative becomes the Gradient:** A vector of all the first partial derivatives. Setting it to zero means the landscape is perfectly flat in every direction at that specific point.
- **The Second Derivative becomes the Hessian Matrix ($H$):** A symmetric matrix containing all the second partial derivatives.

Here is the conceptual leap: **How do you say a *matrix* is "greater than zero"?** You can't just look at the individual numbers inside the matrix. A matrix is "positive" if the fundamental geometry it represents curves upwards in every possible direction. In linear algebra, a matrix that behaves this way is called **Positive Definite**.

## 3. The Energy Connection: Why $x^T S x > 0$ Matters

To see *why* a positive definite Hessian guarantees a minimum, we look at the multi-dimensional Taylor expansion. If you are at a flat point (gradient is zero) and you take a tiny step in any direction (let's call that step vector $v$), the change in your function's height is determined almost entirely by the second derivative matrix $H$:

$$
\text{Change in height} \approx \frac{1}{2} v^T H v
$$

For that flat point to be a true minimum, *any* step you take away from it must increase your height. Therefore, the term $v^T H v$ must be strictly greater than zero for any non-zero step $v$.

Does that equation look familiar? It is the exact definition of the "Energy Test" Strang introduces:

$$
x^T S x > 0.
$$

**Positive definite matrices are the linear algebra equivalent of a positive second derivative.**

## 4. The Geometry of the Landscape

Depending on the eigenvalues of that matrix, the geometry of your critical point changes completely:

- **All Positive Eigenvalues (Positive Definite):** The energy is positive in every direction. You are at the bottom of a strict bowl.
- **All Negative Eigenvalues (Negative Definite):** The energy is negative in every direction. You are at the peak of a mountain.
- **Mixed Eigenvalues (Indefinite):** The energy goes up in some directions and down in others.

This third scenario creates a **saddle point**. The gradient is zero, so it looks flat, but it curves up like a bowl on one axis and drapes down like a hill on another.

## 5. Navigating the Real World

This isn't just theoretical elegance; it is the mathematical bedrock of training complex architectures like Transformers or diffusion models.

When you define a loss function for a neural network, you are creating a chaotic, high-dimensional mountain range with millions or billions of parameters. Gradient descent is the process of blindly stepping downhill to minimize that loss.

However, in deep learning, the gradient only tells you the slope. It doesn't tell you the curvature. A major problem in training is getting stuck at saddle points. The gradient becomes zero, and the model thinks it has found the solution (the minimum loss). But if the Hessian matrix of the loss function is *indefinite* at that point, the model is actually resting on a ledge, not at the bottom of the valley.

If a function is strictly convex, meaning its second derivative matrix is symmetric positive definite everywhere, it is an optimization dream. It means the landscape is one giant, perfect bowl, and gradient descent is mathematically guaranteed to find the absolute global minimum without ever getting trapped.

## Positive Definite Matrices and Principal Axes

This is another brilliant geometric translation provided by Strang. In the previous section, we established that the "energy" of a positive definite matrix, $E = x^T S x$, creates a 3D landscape shaped like a perfect bowl opening upwards.

Now, Strang is shifting the focus from the *bottom* of the bowl to its *cross-sections*.

Here is how to decode this geometric application, which is formally known as the **Principal Axis Theorem**.

## 1. Slicing the Bowl

Imagine you are pouring water into this 3D energy bowl until the water level reaches exactly a height of 1. The surface of the water forms a 2D cross-section of the bowl.

Mathematically, you are setting the energy equation to a constant:

$$
x^T S x = 1
$$

Because the matrix $S$ is positive definite (the bowl curves upwards in every direction), this cross-section will always be a closed loop. Specifically, it forms an **ellipse**.

If you look at the matrix $S = \begin{bmatrix} 5 & 4 \\ 4 & 5 \end{bmatrix}$, expanding $x^T S x = 1$ gives you the algebraic equation of this ellipse:

$$
5x^2 + 8xy + 5y^2 = 1
$$

## 2. The Problem with the "Tilt"

If you were to graph that equation on a standard $x$-$y$ grid (as seen on the left side of page 51), you would notice something annoying: the ellipse is tilted.

The culprit behind this tilt is the **$8xy$ cross-term**. In linear algebra, whenever your off-diagonal elements in a symmetric matrix are non-zero (the $4$s in matrix $S$), your resulting geometric shape will be rotated relative to the standard coordinate axes.

Working with tilted shapes is mathematically messy. We want to align the ellipse perfectly with our axes so it looks like the neat, upright ellipse on the right side of the page.

## 3. The Solution: Eigendecomposition ($S = Q \Lambda Q^T$)

This is where the magic of eigenvectors and eigenvalues comes in. By factoring the matrix into $S = Q \Lambda Q^T$, we can completely untangle the tilt and the stretching of the ellipse.

- **The Eigenvectors ($Q$) dictate the DIRECTIONS:** The eigenvectors of a symmetric matrix are always orthogonal (perpendicular) to each other. They point exactly along the **principal axes** of the ellipse. In the book, $q_1$ and $q_2$ point perfectly along the longest and shortest diameters of the tilted shape.

By changing our coordinate system from the old $(x, y)$ to new coordinates $(X, Y)$ that line up with these eigenvectors, we effectively rotate our perspective so the ellipse sits straight up. The cross-term vanishes completely.

- **The Eigenvalues ($\Lambda$) dictate the LENGTHS:**
Once the ellipse is straightened out, its new equation uses the eigenvalues ($\lambda_1 = 9$ and $\lambda_2 = 1$) as the coefficients:

$$
9X^2 + 1Y^2 = 1
$$

This is the exact same ellipse, just viewed from our new, perfectly aligned coordinate system!

## 4. The Counter-Intuitive Golden Rule

There is one beautiful, slightly counter-intuitive detail Strang highlights at the bottom of the page regarding the lengths of the axes.

The half-length of an axis is equal to **$1 / \sqrt{\lambda}$**.

This means there is an inverse relationship between the eigenvalue and the physical length of the ellipse:

- The **larger** eigenvalue ($\lambda_1 = 9$) corresponds to the **shorter** axis (length $= 1/\sqrt{9} = 1/3$).
- The **smaller** eigenvalue ($\lambda_2 = 1$) corresponds to the **longer** axis (length $= 1/\sqrt{1} = 1$).

**Why does this happen?** Think back to the 3D bowl. A large eigenvalue means the bowl curves upwards very steeply in that direction. Because it is so steep, it reaches the water level (height = 1) very quickly. Therefore, the distance from the center to the edge (the axis of the ellipse) is very short! A small eigenvalue means a shallow slope, so it takes a longer horizontal distance to reach a height of 1.

When you scale this up to $n$ dimensions, you are no longer dealing with a 2D ellipse, but an $n$-dimensional hyper-ellipsoid. The exact same rules apply: the eigenvectors define its orientation in high-dimensional space, and the eigenvalues dictate how far it stretches in each of those directions.

If you were to apply this concept of stretching and rotation to the spread of a massive dataset, how do you think these principal axes (eigenvectors) might help you identify the most important features in that data?
