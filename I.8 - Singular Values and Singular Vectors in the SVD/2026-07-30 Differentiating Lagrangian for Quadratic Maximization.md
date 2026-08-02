---
title: Differentiating Lagrangian for Quadratic Maximization
type: source
source: Gemini
created: 2026-07-30
tags: [type/source, part/1, section/I-8, svd, lagrange-multipliers, matrix-calculus, norms]
related: ["[[I.8 - Differentiating the Lagrangian]]", "[[I.8 - Forward Reverse and the Block Matrix for SVD]]"]
---

> From: https://gemini.google.com/app/60b9bfed0290ca88?_gl=1*16c05zd*_ga*OTc2MDI5MDc5LjE3NDc0Nzk2NjI.*_ga_WC57KJ50ZZ*czE3NDc0Nzk2NjYkbzEkZzEkdDE3NDc0Nzk4MzIkajAkbDAkaDA.

# you asked

message time: 2026-07-30 15:44:43

Help me solve problem 9. I have difficulty in differentiating expressions which have matrices and vectors so go slower there

---

# gemini response

Matrix and vector differentiation can definitely feel unintuitive at first because you are dealing with multiple variables simultaneously. The best way to demystify these rules is to break the matrices and vectors down into their individual algebraic components using summation notation. 

Let's walk through Problem 9 from "image.png" step-by-step.

### The Problem Setup

We are given the Lagrangian equation used to maximize a quadratic form subject to a constraint:
$$L(\boldsymbol{x}, \lambda) = \boldsymbol{x}^T S \boldsymbol{x} - \lambda(\boldsymbol{x}^T \boldsymbol{x} - 1)$$

To find the critical points, we need to find where the gradient of $L$ with respect to the vector $\boldsymbol{x}$ is equal to the zero vector ($\nabla L = 0$). The gradient is simply a vector containing the partial derivative of $L$ with respect to each individual variable $x_i$:
$$\nabla L = \left( \frac{\partial L}{\partial x_1}, \frac{\partial L}{\partial x_2}, \dots, \frac{\partial L}{\partial x_n} \right)^T$$

To evaluate this, we will find the derivative of the two main terms separately: $\boldsymbol{x}^T \boldsymbol{x}$ and $\boldsymbol{x}^T S \boldsymbol{x}$.

---

### Part 1: Differentiating $\boldsymbol{x}^T \boldsymbol{x}$

The term $\boldsymbol{x}^T \boldsymbol{x}$ is the standard dot product of a vector with itself. If we write this out without matrix notation, it is just the sum of the squared components:
$$\boldsymbol{x}^T \boldsymbol{x} = x_1^2 + x_2^2 + \dots + x_n^2 = \sum_{i=1}^n x_i^2$$

Now, imagine we want to find the partial derivative with respect to just one specific variable in that vector, let's call it $x_k$. When taking a partial derivative, all other variables are treated as constants (so their derivatives are zero). 
$$\frac{\partial}{\partial x_k} (\boldsymbol{x}^T \boldsymbol{x}) = \frac{\partial}{\partial x_k} (x_k^2) = 2x_k$$

If we compute this for every single variable from $x_1$ to $x_n$ and stack those results back into a gradient vector, we get:
$$\nabla (\boldsymbol{x}^T \boldsymbol{x}) = \begin{bmatrix} 2x_1 \\ 2x_2 \\ \vdots \\ 2x_n \end{bmatrix} = 2 \begin{bmatrix} x_1 \\ x_2 \\ \vdots \\ x_n \end{bmatrix} = 2\boldsymbol{x}$$

### Part 2: Differentiating $\boldsymbol{x}^T S \boldsymbol{x}$

This term is a quadratic form. Let's expand this matrix multiplication into a double sum to see what it actually looks like algebraically:
$$\boldsymbol{x}^T S \boldsymbol{x} = \sum_{i=1}^n \sum_{j=1}^n x_i S_{ij} x_j$$

Again, we want to find the partial derivative with respect to a single arbitrary variable, $x_k$. We need to look at the double sum and isolate only the terms where $x_k$ appears. There are three situations where this happens:
1.  **When $i = k$ (but $j \neq k$):** The terms look like $x_k S_{kj} x_j$.
2.  **When $j = k$ (but $i \neq k$):** The terms look like $x_i S_{ik} x_k$.
3.  **When both $i = k$ and $j = k$:** This is the single term $x_k S_{kk} x_k = S_{kk} x_k^2$.

Let's take the derivative of these isolated parts with respect to $x_k$:
*   The derivative of the first part is: $\sum_{j \neq k} S_{kj} x_j$
*   The derivative of the second part is: $\sum_{i \neq k} x_i S_{ik}$
*   The derivative of the third part is: $2 S_{kk} x_k$

If we add these three derivatives together, you'll notice that the $2 S_{kk} x_k$ neatly provides the missing $k$-th term for both of the sums above. We can combine them back into complete sums from $1$ to $n$:
$$\frac{\partial}{\partial x_k} (\boldsymbol{x}^T S \boldsymbol{x}) = \sum_{j=1}^n S_{kj} x_j + \sum_{i=1}^n x_i S_{ik}$$

Take a close look at what these two sums represent in standard matrix-vector multiplication:
*   The first sum ($\sum_{j=1}^n S_{kj} x_j$) is exactly the formula for the $k$-th element of the vector $S\boldsymbol{x}$.
*   The second sum ($\sum_{i=1}^n S_{ik} x_i$) is the formula for the $k$-th element of the vector $S^T\boldsymbol{x}$ (because the row and column indices $i$ and $k$ are swapped relative to the vector $x$).

Stacking these scalar derivatives back into a full gradient vector yields:
$$\nabla (\boldsymbol{x}^T S \boldsymbol{x}) = S\boldsymbol{x} + S^T\boldsymbol{x}$$

**The Symmetric Matrix Rule:** In the context of SVD and Rayleigh quotients, the matrix $S$ is symmetric (e.g., $S = A^TA$). By definition, a symmetric matrix is equal to its transpose ($S = S^T$). 
Because $S = S^T$, we can simplify our gradient:
$$\nabla (\boldsymbol{x}^T S \boldsymbol{x}) = S\boldsymbol{x} + S\boldsymbol{x} = 2S\boldsymbol{x}$$

---

### Part 3: Putting It All Together

Now that we have the derivatives of the individual matrix/vector parts, we can easily solve the whole Lagrangian expression. 

Substitute the results from Part 1 and Part 2 back into the derivative of the original equation:
$$L = \boldsymbol{x}^T S \boldsymbol{x} - \lambda(\boldsymbol{x}^T \boldsymbol{x} - 1)$$
$$\nabla L = \nabla (\boldsymbol{x}^T S \boldsymbol{x}) - \lambda \nabla (\boldsymbol{x}^T \boldsymbol{x}) - \nabla(-\lambda)$$
$$\nabla L = 2S\boldsymbol{x} - \lambda(2\boldsymbol{x}) - 0$$

To find the maximum, we set the gradient to zero:
$$2S\boldsymbol{x} - 2\lambda\boldsymbol{x} = 0$$

Moving the second term to the right side of the equals sign completes the proof requested in the problem:
$$2S\boldsymbol{x} = 2\lambda\boldsymbol{x}$$

---

# you asked

message time: 2026-07-30 15:53:12

can we go even slower when we discuss the differentiation of xtsx, i am unable to even form the double summation part, im struggling with composing the double summation in an intuitive way; id rather not have to memorize this uk

---

# gemini response

You are completely right to want to build this from the ground up rather than relying on memorization. When textbooks jump straight into double summations, it can feel like a magic trick where the intermediate steps are hidden. 

To make this intuitive, let's banish the abstract $n \times n$ matrices and $\Sigma$ symbols for a moment. We will build the expression $\boldsymbol{x}^T S \boldsymbol{x}$ completely by hand using a simple $2 \times 2$ example. 

### Step 1: Defining the Pieces

Let's work in a 2D space where everything is visible. 
Our vector $\boldsymbol{x}$ and our matrix $S$ look like this:
$$\boldsymbol{x} = \begin{bmatrix} x_1 \\ x_2 \end{bmatrix}$$
$$S = \begin{bmatrix} S_{11} & S_{12} \\ S_{21} & S_{22} \end{bmatrix}$$

The expression $\boldsymbol{x}^T S \boldsymbol{x}$ is evaluated from right to left. We can break it down into two physical operations:
1.  Multiply the matrix $S$ by the vector $\boldsymbol{x}$.
2.  Multiply the row vector $\boldsymbol{x}^T$ by the result of step 1.

---

### Step 2: The First Operation ($S\boldsymbol{x}$)

When a matrix multiplies a column vector, it produces a new column vector. Let's write out exactly what that new vector is using standard dot products (row multiplied by column).

$$S\boldsymbol{x} = \begin{bmatrix} S_{11} & S_{12} \\ S_{21} & S_{22} \end{bmatrix} \begin{bmatrix} x_1 \\ x_2 \end{bmatrix} = \begin{bmatrix} S_{11}x_1 + S_{12}x_2 \\ S_{21}x_1 + S_{22}x_2 \end{bmatrix}$$

Take a moment to look at how this new vector is structured. To get the top element, we locked onto the first row of $S$ (index 1) and iterated across its columns while moving down $\boldsymbol{x}$.

---

### Step 3: The Second Operation ($\boldsymbol{x}^T$ times the new vector)

Now we have a new column vector. The final step is to multiply it by the transposed vector $\boldsymbol{x}^T$, which is just a flat row: $[x_1, x_2]$.

$$\boldsymbol{x}^T (S\boldsymbol{x}) = \begin{bmatrix} x_1 & x_2 \end{bmatrix} \begin{bmatrix} (S_{11}x_1 + S_{12}x_2) \\ (S_{21}x_1 + S_{22}x_2) \end{bmatrix}$$

To multiply a row vector by a column vector, you multiply the first elements together, multiply the second elements together, and add the results. 

$$= x_1(S_{11}x_1 + S_{12}x_2) + x_2(S_{21}x_1 + S_{22}x_2)$$

Now, let's distribute the $x_1$ and $x_2$ to expand this into a simple polynomial:

$$= S_{11}x_1^2 + S_{12}x_1x_2 + S_{21}x_2x_1 + S_{22}x_2^2$$

This final polynomial is the absolute core of $\boldsymbol{x}^T S \boldsymbol{x}$. Every single term in this polynomial consists of three pieces: an element from $\boldsymbol{x}$, an element from the matrix $S$, and another element from $\boldsymbol{x}$.

---

### Step 4: Bridging to the Double Summation

If you look closely at our expanded polynomial above, you will notice it contains every possible combination of row and column indices. 

If you were writing a computer program to generate that polynomial, you wouldn't write out every term by hand. You would write a nested loop. A double summation is literally just mathematical notation for a nested `for` loop.

We want a loop that says: "Go through every row $i$, and for every row $i$, go through every column $j$, and multiply $x_i \cdot S_{ij} \cdot x_j$."

Written mathematically, that nested loop looks like this:
$$\sum_{i=1}^2 \left( \sum_{j=1}^2 x_i S_{ij} x_j \right)$$

Let's mentally "run" this loop to prove it builds our polynomial:
*   **When $i = 1$:** The inner loop runs for $j=1$ and $j=2$. This outputs: $(x_1 S_{11} x_1 + x_1 S_{12} x_2)$
*   **When $i = 2$:** The inner loop runs for $j=1$ and $j=2$. This outputs: $(x_2 S_{21} x_1 + x_2 S_{22} x_2)$

Add those two outputs together, and you get the exact same polynomial we built by hand. The double summation is not a new math rule; it is just a compact way of writing the distributive property. 

---

### Step 5: Taking the Derivative Visually

Now that we have stripped away the matrix notation and just have a standard polynomial, let's find the gradient. The gradient requires us to find the partial derivative with respect to each variable. 

Let's just find the partial derivative with respect to $x_1$. When differentiating with respect to $x_1$, we treat $x_2$ as a constant. 

Here is our polynomial again:
$$f(\boldsymbol{x}) = S_{11}x_1^2 + S_{12}x_1x_2 + S_{21}x_2x_1 + S_{22}x_2^2$$

Let's differentiate it term by term:
*   Derivative of $S_{11}x_1^2 \rightarrow 2S_{11}x_1$
*   Derivative of $S_{12}x_1x_2 \rightarrow S_{12}x_2$
*   Derivative of $S_{21}x_2x_1 \rightarrow S_{21}x_2$
*   Derivative of $S_{22}x_2^2 \rightarrow 0$ (Because there is no $x_1$ here, it is treated as a constant).

So, the partial derivative with respect to $x_1$ is:
$$\frac{\partial f}{\partial x_1} = 2S_{11}x_1 + S_{12}x_2 + S_{21}x_2$$

To see how this ties back to matrix notation, let's split that $2S_{11}x_1$ into two separate pieces ($S_{11}x_1 + S_{11}x_1$) and group the terms:

$$\frac{\partial f}{\partial x_1} = (S_{11}x_1 + S_{12}x_2) + (S_{11}x_1 + S_{21}x_2)$$

Look incredibly closely at those two groups in the parentheses:
*   The first group $(S_{11}x_1 + S_{12}x_2)$ is exactly the first row of the vector $S\boldsymbol{x}$ (which we calculated in Step 2).
*   The second group $(S_{11}x_1 + S_{21}x_2)$ is exactly the first row of the vector $S^T\boldsymbol{x}$ (because the index 21 means it is pulling from the column of the original matrix).

This is why the gradient of the entire expression evaluates to $S\boldsymbol{x} + S^T\boldsymbol{x}$. If you do this same exercise for $x_2$, you will find it builds the exact second rows of those same two vectors. And as established before, since $S$ is a symmetric matrix ($S = S^T$), those two vectors are identical, leaving you with a final gradient of $2S\boldsymbol{x}$.

---

# you asked

message time: 2026-07-30 16:18:14

Help me problem 10 from the image also

---

# gemini response

Problem 10 asks you to prove a very important property in linear algebra: **the norm of a submatrix is always less than or equal to the norm of the original full matrix.** 

The textbook lays out a specific breadcrumb trail to prove this:
$\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|$

To understand this sequence intuitively, we need to answer the crucial "(Why?)" in the middle of the problem text. Let's break down exactly what a matrix norm is and why removing columns or rows inherently limits it.

### Part 1: What is a Matrix Norm?

In the context of Singular Value Decomposition (SVD), the notation $\|A\|$ refers to the **spectral norm** (or induced 2-norm) of a matrix. 

Instead of thinking of a matrix as just a grid of numbers, think of matrix $A$ as a machine that takes in an input vector $\boldsymbol{x}$, transforms it, and spits out an output vector $A\boldsymbol{x}$. 

The norm $\|A\|$ is simply the **maximum stretching power** of that machine. If you feed the machine every possible vector of length 1 (a unit vector), $\|A\|$ is the length of the longest possible vector that comes out. 

Mathematically, this maximum stretch is exactly equal to the largest singular value of the matrix ($\sigma_1$).

---

### Part 2: Answering the "(Why?)" – Removing Columns

The problem states: *Remove first the $N - n$ columns of $A$. The new matrix has $\|C\| \le \|A\|$. (Why?)*

Let’s build an intuitive, visual example to answer this. Imagine $A$ is a matrix with 3 columns: $\boldsymbol{a_1}$, $\boldsymbol{a_2}$, and $\boldsymbol{a_3}$. 
When we multiply $A$ by a 3D vector $\boldsymbol{x}$, we are just mixing those columns together using the elements of $\boldsymbol{x}$ as weights:
$$A\boldsymbol{x} = x_1\boldsymbol{a_1} + x_2\boldsymbol{a_2} + x_3\boldsymbol{a_3}$$

To find the norm $\|A\|$, we are searching through *every possible combination* of $x_1$, $x_2$, and $x_3$ (where the total vector length is 1) to find the combination that gives the biggest possible result.

Now, let's create matrix $C$ by deleting the last column ($\boldsymbol{a_3}$). $C$ now only has two columns: $\boldsymbol{a_1}$ and $\boldsymbol{a_2}$.
When we multiply $C$ by a 2D vector $\boldsymbol{y}$, we get:
$$C\boldsymbol{y} = y_1\boldsymbol{a_1} + y_2\boldsymbol{a_2}$$

**Here is the intuitive leap:** Notice that the output of $C\boldsymbol{y}$ is mathematically identical to the output of $A\boldsymbol{x}$ if we were to simply force $x_3 = 0$. 

By deleting a column, we haven't created a fundamentally new machine; we have just taken the original machine $A$ and **restricted its inputs**. We are telling the machine, "You must calculate your stretch, but you are no longer allowed to use the third dial." 

If you are trying to maximize a score, and suddenly your choices are restricted (by forcing some variables to be exactly zero), your maximum possible score can either stay the same or go down. It is physically impossible for your maximum score to increase when you have fewer options to choose from. 

Therefore, the maximum stretching power of $C$ must be less than or equal to the maximum stretching power of $A$:
$$\|C\| \le \|A\|$$

---

### Part 3: The Transpose Property

The next step in the problem says: *Then transpose $C$: no change in norm.*

This is a fundamental property of matrices. A matrix $C$ and its transpose $C^T$ always share the exact same non-zero singular values. 

Since the norm is defined as the largest singular value ($\sigma_1$), transposing a matrix flips its shape but does absolutely nothing to its maximum stretching power. 
Therefore:
$$\|C^T\| = \|C\|$$

---

### Part 4: Putting the Chain Together

Now we can follow the exact chain of logic the textbook provides to reach the final proof for submatrix $B$.

1.  **Start with matrix $A$.**
2.  **Remove columns to get $C$:** As we established, restricting the inputs by removing columns means the maximum stretch cannot increase.
    $$\|C\| \le \|A\|$$
3.  **Transpose $C$ to get $C^T$:** Transposing doesn't change the norm. 
    $$\|C^T\| = \|C\|$$
4.  **Remove columns from $C^T$ to get $B^T$:** Removing columns from $C^T$ restricts the inputs again. Using the exact same logic we used in Step 2, the norm cannot increase.
    $$\|B^T\| \le \|C^T\|$$
5.  **Transpose $B^T$ to get $B$:** Transposing back to our final submatrix $B$ does not change the norm.
    $$\|B\| = \|B^T\|$$

When you string all of these logical steps together, you get the final proof exactly as the book writes it:
$$\|B\| = \|B^T\| \le \|C^T\| = \|C\| \le \|A\|$$

By stringing together column deletions (which restrict the input space) and transposes (which allow you to delete rows by turning them into columns), you prove that any smaller submatrix $B$ carved out of $A$ will never have a larger spectral norm than $A$ itself.

---

# you asked

message time: 2026-07-30 16:38:31

In problem 11, help me out with figuring out the eigenvectors of S. I do not see that yet.

---

# gemini response

Block matrices can make eigenvalue problems look much more intimidating than they actually are. To figure out the eigenvectors of $S$, the trick is to stop looking at $S$ as one giant $2n \times 2n$ grid, and instead treat it as a system of two separate equations.

Here is how we can break down Problem 11 step-by-step to reveal those eigenvectors.

### Step 1: Set up the Block Equation

We are trying to solve the standard eigenvalue equation:
$$S\boldsymbol{v} = \lambda \boldsymbol{v}$$

Because $S$ is a block matrix partitioned into four $n \times n$ sections, any eigenvector $\boldsymbol{v}$ of length $2n$ can simply be split into a "top half" and a "bottom half", each of length $n$. Let's call the top half vector $\boldsymbol{x}$ and the bottom half vector $\boldsymbol{y}$.

Also, the problem states $A$ is a square diagonal matrix. A fundamental property of diagonal matrices is that they are symmetric, meaning $A = A^T$. 

Let's plug our block vector and $A$ into the eigenvalue equation:
$$\begin{bmatrix} 0 & A \\ A & 0 \end{bmatrix} \begin{bmatrix} \boldsymbol{x} \\ \boldsymbol{y} \end{bmatrix} = \lambda \begin{bmatrix} \boldsymbol{x} \\ \boldsymbol{y} \end{bmatrix}$$

### Step 2: Extract the Coupled Equations

If we perform the matrix multiplication on the left side, we get two separate equations (one for the top block row, one for the bottom block row):
1.  **Top:** $0\boldsymbol{x} + A\boldsymbol{y} = \lambda \boldsymbol{x} \implies A\boldsymbol{y} = \lambda \boldsymbol{x}$
2.  **Bottom:** $A\boldsymbol{x} + 0\boldsymbol{y} = \lambda \boldsymbol{y} \implies A\boldsymbol{x} = \lambda \boldsymbol{y}$

These are "coupled" equations because $\boldsymbol{x}$ depends on $\boldsymbol{y}$, and $\boldsymbol{y}$ depends on $\boldsymbol{x}$. We need to decouple them to solve for just one variable. 

Let's rearrange equation 2 to isolate $\boldsymbol{y}$: 
$$\boldsymbol{y} = \frac{1}{\lambda} A\boldsymbol{x}$$

Now, substitute that definition of $\boldsymbol{y}$ into equation 1:
$$A \left( \frac{1}{\lambda} A\boldsymbol{x} \right) = \lambda \boldsymbol{x}$$
$$A^2\boldsymbol{x} = \lambda^2 \boldsymbol{x}$$

### Step 3: Find the Eigenvalues ($\lambda$)

Look closely at $A^2\boldsymbol{x} = \lambda^2 \boldsymbol{x}$. This is just a standard eigenvalue equation for the matrix $A^2$. 

The problem tells us that $A$ is a diagonal matrix with entries $1, 2, \dots, n$. 
When you square a diagonal matrix, you simply square its diagonal entries. So, the eigenvalues of $A^2$ are $1^2, 2^2, \dots, n^2$. 

This means that for any $k$-th entry on the diagonal:
$$\lambda^2 = k^2$$

Taking the square root gives us two possible eigenvalues for every entry $k$:
$$\lambda = k \quad \text{and} \quad \lambda = -k$$

Since $k$ ranges from $1$ to $n$, this gives us exactly the **$2n$ eigenvalues** the problem asks for: $\pm 1, \pm 2, \dots, \pm n$.

### Step 4: Construct the Eigenvectors ($\boldsymbol{v}$)

Now we need to build the full eigenvector $\boldsymbol{v} = [\boldsymbol{x}, \boldsymbol{y}]^T$. 

Because $A$ is diagonal, its eigenvectors (which are our $\boldsymbol{x}$ vectors) are simply the standard basis vectors. Let's define $\boldsymbol{e}_k$ as a vector with a 1 in the $k$-th position and zeros everywhere else. 

If we choose $\boldsymbol{x} = \boldsymbol{e}_k$, let's find out what the bottom half, $\boldsymbol{y}$, must be. We can use equation 2 from Step 2: $A\boldsymbol{x} = \lambda \boldsymbol{y}$.
$$A\boldsymbol{e}_k = \lambda \boldsymbol{y}$$

Because multiplying $A$ by $\boldsymbol{e}_k$ simply extracts the $k$-th diagonal entry, $A\boldsymbol{e}_k = k\boldsymbol{e}_k$. So:
$$k\boldsymbol{e}_k = \lambda \boldsymbol{y}$$

Now, we evaluate this for both the positive and negative eigenvalues we found in Step 3:

**Case 1: The Positive Eigenvalue ($\lambda = k$)**
$$k\boldsymbol{e}_k = k\boldsymbol{y}$$
$$\boldsymbol{y} = \boldsymbol{e}_k$$
If the top half is $\boldsymbol{e}_k$, the bottom half must also be $\boldsymbol{e}_k$. 

**Case 2: The Negative Eigenvalue ($\lambda = -k$)**
$$k\boldsymbol{e}_k = -k\boldsymbol{y}$$
$$\boldsymbol{y} = -\boldsymbol{e}_k$$
If the top half is $\boldsymbol{e}_k$, the bottom half must be $-\boldsymbol{e}_k$.

### The Final Result

By stacking $\boldsymbol{x}$ and $\boldsymbol{y}$ back into our $2n$-dimensional vector space, we get our $2n$ eigenvectors. 

For each $k \in \{1, 2, \dots, n\}$, there is a pair of eigenvectors:
*   The eigenvector for $\lambda = k$ is $\begin{bmatrix} \boldsymbol{e}_k \\ \boldsymbol{e}_k \end{bmatrix}$
*   The eigenvector for $\lambda = -k$ is $\begin{bmatrix} \boldsymbol{e}_k \\ -\boldsymbol{e}_k \end{bmatrix}$

---
Powered by [AI Exporter](https://saveai.net)