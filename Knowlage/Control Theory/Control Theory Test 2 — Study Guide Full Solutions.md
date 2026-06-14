
---

# General Notes

This document gives full study-guide style solutions for all tasks.

The formatting is prepared for Obsidian:

- Inline equations use `$...$`.
- Display equations use `$$...$$`.
- No square-bracket LaTeX delimiters are used.
- Every displayed equation is separated by blank lines for clean Obsidian rendering.

---

# Task 1 — Estimator Pole Placement and Observability

## Problem

Consider the LTI system:

$$
\dot{x}=
\begin{bmatrix}
5 & 2\\
1 & 4
\end{bmatrix}x+
\begin{bmatrix}
1\\
e
\end{bmatrix}u
$$

$$
y=
\begin{bmatrix}
f & 1
\end{bmatrix}x
$$

Determine for which values of $e\in\mathbb{R}$ and $f\in\mathbb{R}$ it is possible to locate the estimator poles arbitrarily.

---

## Theory

For an observer or estimator, the observer dynamics usually have the form:

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

where:

- $\hat{x}$ is the estimated state,
- $L$ is the observer gain matrix,
- $y$ is the measured output,
- $C$ is the output matrix.

The observer error is:

$$
\tilde{x}=x-\hat{x}
$$

The error dynamics are:

$$
\dot{\tilde{x}}=(A-LC)\tilde{x}
$$

Therefore, the estimator poles are the eigenvalues of:

$$
A-LC
$$

We can place these poles arbitrarily if and only if the pair $(A,C)$ is observable.

For a second-order system, the observability matrix is:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

The system is observable if:

$$
\operatorname{rank}(\mathcal{O})=2
$$

For a $2\times 2$ observability matrix, this is equivalent to:

$$
\det(\mathcal{O})\neq 0
$$

---

## Step 1: Identify $A$, $B$, and $C$

From the system:

$$
A=
\begin{bmatrix}
5 & 2\\
1 & 4
\end{bmatrix}
$$

$$
B=
\begin{bmatrix}
1\\
e
\end{bmatrix}
$$

$$
C=
\begin{bmatrix}
f & 1
\end{bmatrix}
$$

For estimator pole placement, only $A$ and $C$ are important.

The parameter $e$ appears only in $B$, so we expect that $e$ will not affect observability.

---

## Step 2: Build the observability matrix

The observability matrix is:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

We already know:

$$
C=
\begin{bmatrix}
f & 1
\end{bmatrix}
$$

Now calculate $CA$:

$$
CA=
\begin{bmatrix}
f & 1
\end{bmatrix}
\begin{bmatrix}
5 & 2\\
1 & 4
\end{bmatrix}
$$

Multiply row by columns.

First element:

$$
f\cdot 5+1\cdot 1=5f+1
$$

Second element:

$$
f\cdot 2+1\cdot 4=2f+4
$$

So:

$$
CA=
\begin{bmatrix}
5f+1 & 2f+4
\end{bmatrix}
$$

Therefore:

$$
\mathcal{O}=
\begin{bmatrix}
f & 1\\
5f+1 & 2f+4
\end{bmatrix}
$$

---

## Step 3: Apply the observability condition

We need:

$$
\det(\mathcal{O})\neq 0
$$

Compute the determinant:

$$
\det(\mathcal{O})
=
\begin{vmatrix}
f & 1\\
5f+1 & 2f+4
\end{vmatrix}
$$

For a $2\times 2$ matrix:

$$
\det
\begin{bmatrix}
a & b\\
c & d
\end{bmatrix}
=ad-bc
$$

Thus:

$$
\det(\mathcal{O})
=
f(2f+4)-1(5f+1)
$$

Expand:

$$
\det(\mathcal{O})
=
2f^2+4f-5f-1
$$

Simplify:

$$
\det(\mathcal{O})
=
2f^2-f-1
$$

Factor:

$$
2f^2-f-1=(2f+1)(f-1)
$$

Therefore:

$$
\det(\mathcal{O})=(2f+1)(f-1)
$$

The system is observable if:

$$
(2f+1)(f-1)\neq 0
$$

So:

$$
2f+1\neq 0
$$

$$
f\neq -\frac{1}{2}
$$

and:

$$
f-1\neq 0
$$

$$
f\neq 1
$$

---

## Final Answer

The estimator poles can be placed arbitrarily when:

$$
f\neq -\frac{1}{2}
$$

and

$$
f\neq 1
$$

The parameter $e$ does not influence the answer because it appears only in $B$, not in $A$ or $C$.

Therefore:

$$
\boxed{
e\in\mathbb{R},\qquad
f\in\mathbb{R}\setminus\left\{-\frac{1}{2},1\right\}
}
$$

---

# Task 2 — Equilibrium Points of a Nonlinear System

## Problem

Consider the nonlinear system:

$$
\dot{x}_1=x_2(1-x_2^2)
$$

$$
\dot{x}_2=x_1
$$

Find the equilibrium points.

---

## Theory

An equilibrium point is a point where all derivatives are zero.

For a two-state system:

$$
\dot{x}_1=f_1(x_1,x_2)
$$

$$
\dot{x}_2=f_2(x_1,x_2)
$$

an equilibrium point satisfies:

$$
f_1(x_1,x_2)=0
$$

$$
f_2(x_1,x_2)=0
$$

In this problem, we need:

$$
\dot{x}_1=0
$$

and:

$$
\dot{x}_2=0
$$

---

## Step 1: Set the derivatives equal to zero

Given:

$$
\dot{x}_1=x_2(1-x_2^2)
$$

$$
\dot{x}_2=x_1
$$

Set them equal to zero:

$$
x_2(1-x_2^2)=0
$$

$$
x_1=0
$$

The second equation immediately gives:

$$
x_1=0
$$

---

## Step 2: Solve the first equation

We need:

$$
x_2(1-x_2^2)=0
$$

This is a product of two factors:

$$
x_2=0
$$

or:

$$
1-x_2^2=0
$$

Solve the second case:

$$
1-x_2^2=0
$$

$$
x_2^2=1
$$

$$
x_2=\pm 1
$$

Therefore:

$$
x_2=0
$$

$$
x_2=1
$$

$$
x_2=-1
$$

---

## Step 3: Combine with $x_1=0$

Since $x_1=0$ in every equilibrium point, the equilibrium points are:

$$
(0,0)
$$

$$
(0,1)
$$

$$
(0,-1)
$$

---

## Final Answer

$$
\boxed{
(0,0),\quad (0,1),\quad (0,-1)
}
$$

---

# Task 3 — Stability by the First Lyapunov Method

## Problem

Consider the nonlinear system:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-x_1+x_1^3
$$

Decide whether the system is stable around the equilibrium point $(0,0)$.

Use the first Lyapunov method and write the conclusion.

---

## Theory

The first Lyapunov method is also called the indirect Lyapunov method or linearization method.

For a nonlinear system:

$$
\dot{x}=f(x)
$$

we linearize the system around an equilibrium point $x_e$.

The linearized system is:

$$
\dot{x}=Ax
$$

where:

$$
A=\left.\frac{\partial f}{\partial x}\right|_{x=x_e}
$$

The rules are:

1. If all eigenvalues of $A$ have negative real parts, then the nonlinear system is locally asymptotically stable.
2. If at least one eigenvalue of $A$ has positive real part, then the nonlinear system is unstable.
3. If eigenvalues lie on the imaginary axis and none have positive real part, the method is inconclusive.

---

## Step 1: Write the vector field

Define:

$$
f_1(x_1,x_2)=x_2
$$

$$
f_2(x_1,x_2)=-x_1+x_1^3
$$

Therefore:

$$
f(x)=
\begin{bmatrix}
f_1\\
f_2
\end{bmatrix}
=
\begin{bmatrix}
x_2\\
-x_1+x_1^3
\end{bmatrix}
$$

---

## Step 2: Compute the Jacobian matrix

The Jacobian is:

$$
A(x)=
\begin{bmatrix}
\frac{\partial f_1}{\partial x_1} &
\frac{\partial f_1}{\partial x_2}\\
\frac{\partial f_2}{\partial x_1} &
\frac{\partial f_2}{\partial x_2}
\end{bmatrix}
$$

Calculate each derivative.

First row:

$$
\frac{\partial f_1}{\partial x_1}
=
\frac{\partial x_2}{\partial x_1}=0
$$

$$
\frac{\partial f_1}{\partial x_2}
=
\frac{\partial x_2}{\partial x_2}=1
$$

Second row:

$$
\frac{\partial f_2}{\partial x_1}
=
\frac{\partial}{\partial x_1}(-x_1+x_1^3)
=
-1+3x_1^2
$$

$$
\frac{\partial f_2}{\partial x_2}
=
\frac{\partial}{\partial x_2}(-x_1+x_1^3)=0
$$

So:

$$
A(x)=
\begin{bmatrix}
0 & 1\\
-1+3x_1^2 & 0
\end{bmatrix}
$$

---

## Step 3: Evaluate the Jacobian at $(0,0)$

At the origin:

$$
x_1=0
$$

Therefore:

$$
-1+3x_1^2=-1+3\cdot 0^2=-1
$$

So:

$$
A(0,0)=
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}
$$

---

## Step 4: Find eigenvalues

The characteristic equation is:

$$
\det(\lambda I-A)=0
$$

First compute:

$$
\lambda I=
\begin{bmatrix}
\lambda & 0\\
0 & \lambda
\end{bmatrix}
$$

Thus:

$$
\lambda I-A=
\begin{bmatrix}
\lambda & 0\\
0 & \lambda
\end{bmatrix}
-
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}
$$

$$
\lambda I-A=
\begin{bmatrix}
\lambda & -1\\
1 & \lambda
\end{bmatrix}
$$

Now calculate the determinant:

$$
\det(\lambda I-A)
=
\begin{vmatrix}
\lambda & -1\\
1 & \lambda
\end{vmatrix}
$$

$$
=\lambda\cdot\lambda-(-1)\cdot 1
$$

$$
=\lambda^2+1
$$

Therefore:

$$
\lambda^2+1=0
$$

$$
\lambda^2=-1
$$

$$
\lambda_{1,2}=\pm j
$$

---

## Step 5: Interpret the result

The eigenvalues are:

$$
\lambda_1=j
$$

$$
\lambda_2=-j
$$

They are purely imaginary.

Their real parts are:

$$
\operatorname{Re}(\lambda_1)=0
$$

$$
\operatorname{Re}(\lambda_2)=0
$$

Therefore, the first Lyapunov method cannot decide stability.

---

## Final Answer

According to the first Lyapunov method:

$$
\lambda_{1,2}=\pm j
$$

Because the eigenvalues are purely imaginary, the first Lyapunov method is inconclusive.

Therefore, using only the required method:

$$
\boxed{
\text{The first Lyapunov method is inconclusive around }(0,0).
}
$$

Additional study note:

The nonlinear system has a conserved energy-like function and the origin is stable but not asymptotically stable. However, this conclusion does not come directly from the first Lyapunov method.

---

# Task 4 — Lyapunov Function and LaSalle Stability

## Problem

For the nonlinear system:

$$
\dot{x}=
\begin{bmatrix}
x_2\\
-ax_1^3-bx_2
\end{bmatrix}
$$

where:

$$
a>0,\qquad b>0
$$

evaluate the stability of the nonlinear system around the origin with the Lyapunov function:

$$
V(x_1,x_2)=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

What can you say about the stability of this system?

---

## Theory

A Lyapunov function is like an energy function.

To prove stability around the origin, we usually check:

1. $V(x)>0$ for all $x\neq 0$.
2. $V(0)=0$.
3. $\dot{V}(x)\leq 0$ or $\dot{V}(x)<0$.

If:

$$
V(x)>0
$$

and:

$$
\dot{V}(x)<0
$$

for all $x\neq 0$, then the origin is asymptotically stable.

If:

$$
\dot{V}(x)\leq 0
$$

only negative semidefinite, then Lyapunov theory gives stability, but not automatically asymptotic stability.

To prove asymptotic stability in the semidefinite case, we can use LaSalle's invariance principle.

---

## Step 1: Write the system equations

The system is:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-ax_1^3-bx_2
$$

with:

$$
a>0,\qquad b>0
$$

---

## Step 2: Check whether $V$ is positive definite

The candidate Lyapunov function is:

$$
V(x_1,x_2)=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

Since:

$$
a>0
$$

we have:

$$
a\frac{x_1^4}{4}\geq 0
$$

Also:

$$
\frac{x_2^2}{2}\geq 0
$$

Thus:

$$
V(x_1,x_2)\geq 0
$$

Now check where $V=0$.

For:

$$
V(x_1,x_2)=0
$$

we need both terms to be zero:

$$
a\frac{x_1^4}{4}=0
$$

and:

$$
\frac{x_2^2}{2}=0
$$

The first equation gives:

$$
x_1=0
$$

The second equation gives:

$$
x_2=0
$$

Therefore:

$$
V(x_1,x_2)=0
\quad\Longleftrightarrow\quad
(x_1,x_2)=(0,0)
$$

So $V$ is positive definite.

---

## Step 3: Compute $\dot{V}$

We use:

$$
\dot{V}
=
\frac{\partial V}{\partial x_1}\dot{x}_1
+
\frac{\partial V}{\partial x_2}\dot{x}_2
$$

First calculate the partial derivatives.

Since:

$$
V=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

we get:

$$
\frac{\partial V}{\partial x_1}
=
a\cdot \frac{4x_1^3}{4}
=
ax_1^3
$$

and:

$$
\frac{\partial V}{\partial x_2}
=
x_2
$$

Substitute the system equations:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-ax_1^3-bx_2
$$

Therefore:

$$
\dot{V}
=
ax_1^3x_2+x_2(-ax_1^3-bx_2)
$$

Expand:

$$
\dot{V}
=
ax_1^3x_2-ax_1^3x_2-bx_2^2
$$

The first two terms cancel:

$$
ax_1^3x_2-ax_1^3x_2=0
$$

So:

$$
\dot{V}=-bx_2^2
$$

Since $b>0$:

$$
-bx_2^2\leq 0
$$

Therefore:

$$
\dot{V}\leq 0
$$

So $\dot{V}$ is negative semidefinite.

---

## Step 4: What does negative semidefinite mean here?

We have:

$$
\dot{V}=-bx_2^2
$$

This is zero when:

$$
x_2=0
$$

So $\dot{V}$ is not strictly negative for every nonzero state.

For example, if:

$$
x_1\neq 0,\qquad x_2=0
$$

then:

$$
\dot{V}=0
$$

This means that direct Lyapunov theory proves stability, but not yet asymptotic stability.

To prove asymptotic stability, use LaSalle's invariance principle.

---

## Step 5: Use LaSalle's invariance principle

LaSalle says that trajectories approach the largest invariant set contained in:

$$
\{x:\dot{V}=0\}
$$

Here:

$$
\dot{V}=0
$$

means:

$$
-bx_2^2=0
$$

Since $b>0$:

$$
x_2=0
$$

So the set is:

$$
S=\{(x_1,x_2):x_2=0\}
$$

Now check which points in this set are invariant.

If $x_2=0$, then:

$$
\dot{x}_1=x_2=0
$$

and:

$$
\dot{x}_2=-ax_1^3-bx_2
$$

Since $x_2=0$, this becomes:

$$
\dot{x}_2=-ax_1^3
$$

For the trajectory to stay in the set $x_2=0$, we need:

$$
\dot{x}_2=0
$$

Thus:

$$
-ax_1^3=0
$$

Since $a>0$:

$$
x_1=0
$$

Therefore, the largest invariant set inside $\dot{V}=0$ is only:

$$
(0,0)
$$

By LaSalle's invariance principle, the origin is asymptotically stable.

---

## Step 6: Global stability

The Lyapunov function is:

$$
V(x_1,x_2)=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

As $\|(x_1,x_2)\|\to\infty$, at least one of $|x_1|$ or $|x_2|$ goes to infinity.

Then:

$$
a\frac{x_1^4}{4}\to\infty
$$

or:

$$
\frac{x_2^2}{2}\to\infty
$$

Therefore:

$$
V(x_1,x_2)\to\infty
$$

This means $V$ is radially unbounded.

Since $V$ is positive definite, radially unbounded, and LaSalle gives convergence to the origin, the stability is global.

---

## Final Answer

The origin is stable because $V$ is positive definite and $\dot{V}\leq 0$.

Using LaSalle's invariance principle, the only invariant set inside $\dot{V}=0$ is the origin.

Therefore:

$$
\boxed{
\text{The origin is globally asymptotically stable.}
}
$$

---

# Task 5 — State Feedback Pole Placement

## Problem

Consider the LTI system:

$$
\dot{x}=Ax+Bu
$$

where:

$$
A=
\begin{bmatrix}
1 & 2\\
0 & 3
\end{bmatrix}
$$

$$
B=
\begin{bmatrix}
0\\
1
\end{bmatrix}
$$

Design a state feedback controller:

$$
u=-Kx
$$

such that the closed-loop eigenvalues are:

$$
\lambda_1=-1,\qquad \lambda_2=-2
$$

---

## Theory

For state feedback:

$$
u=-Kx
$$

where:

$$
K=
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
$$

Substitute into the system:

$$
\dot{x}=Ax+B(-Kx)
$$

$$
\dot{x}=(A-BK)x
$$

The closed-loop matrix is:

$$
A_{cl}=A-BK
$$

The eigenvalues of the closed-loop system are the roots of:

$$
\det(sI-A_{cl})=0
$$

To design $K$, we match this characteristic polynomial with the desired characteristic polynomial.

---

## Step 1: Define $K$

Let:

$$
K=
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
$$

Then:

$$
BK=
\begin{bmatrix}
0\\
1
\end{bmatrix}
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
$$

Matrix multiplication gives:

$$
BK=
\begin{bmatrix}
0\cdot k_1 & 0\cdot k_2\\
1\cdot k_1 & 1\cdot k_2
\end{bmatrix}
$$

So:

$$
BK=
\begin{bmatrix}
0 & 0\\
k_1 & k_2
\end{bmatrix}
$$

---

## Step 2: Compute $A-BK$

Given:

$$
A=
\begin{bmatrix}
1 & 2\\
0 & 3
\end{bmatrix}
$$

Therefore:

$$
A-BK=
\begin{bmatrix}
1 & 2\\
0 & 3
\end{bmatrix}
-
\begin{bmatrix}
0 & 0\\
k_1 & k_2
\end{bmatrix}
$$

So:

$$
A-BK=
\begin{bmatrix}
1 & 2\\
-k_1 & 3-k_2
\end{bmatrix}
$$

Thus:

$$
A_{cl}=
\begin{bmatrix}
1 & 2\\
-k_1 & 3-k_2
\end{bmatrix}
$$

---

## Step 3: Desired characteristic polynomial

The desired eigenvalues are:

$$
\lambda_1=-1
$$

$$
\lambda_2=-2
$$

Therefore, the desired characteristic polynomial is:

$$
(s-\lambda_1)(s-\lambda_2)
$$

Substitute:

$$
(s-(-1))(s-(-2))
$$

$$
(s+1)(s+2)
$$

Expand:

$$
(s+1)(s+2)=s^2+3s+2
$$

So the desired polynomial is:

$$
p_d(s)=s^2+3s+2
$$

---

## Step 4: Compute the actual characteristic polynomial

We need:

$$
\det(sI-A_{cl})
$$

First:

$$
sI=
\begin{bmatrix}
s & 0\\
0 & s
\end{bmatrix}
$$

Then:

$$
sI-A_{cl}
=
\begin{bmatrix}
s & 0\\
0 & s
\end{bmatrix}
-
\begin{bmatrix}
1 & 2\\
-k_1 & 3-k_2
\end{bmatrix}
$$

Therefore:

$$
sI-A_{cl}
=
\begin{bmatrix}
s-1 & -2\\
k_1 & s-3+k_2
\end{bmatrix}
$$

Now compute determinant:

$$
\det(sI-A_{cl})
=
\begin{vmatrix}
s-1 & -2\\
k_1 & s-3+k_2
\end{vmatrix}
$$

Using $ad-bc$:

$$
\det(sI-A_{cl})
=
(s-1)(s-3+k_2)-(-2)k_1
$$

So:

$$
\det(sI-A_{cl})
=
(s-1)(s-3+k_2)+2k_1
$$

Expand the product:

$$
(s-1)(s-3+k_2)
$$

Notice:

$$
s-3+k_2=s+(k_2-3)
$$

Thus:

$$
(s-1)(s+k_2-3)
$$

Expand:

$$
s(s+k_2-3)-1(s+k_2-3)
$$

$$
=s^2+(k_2-3)s-s-(k_2-3)
$$

$$
=s^2+(k_2-4)s-k_2+3
$$

Therefore:

$$
\det(sI-A_{cl})
=
s^2+(k_2-4)s-k_2+3+2k_1
$$

So the actual characteristic polynomial is:

$$
p(s)=s^2+(k_2-4)s+(3-k_2+2k_1)
$$

---

## Step 5: Match coefficients

We need:

$$
p(s)=p_d(s)
$$

So:

$$
s^2+(k_2-4)s+(3-k_2+2k_1)
=
s^2+3s+2
$$

Compare coefficients of $s$:

$$
k_2-4=3
$$

Therefore:

$$
k_2=7
$$

Compare constant terms:

$$
3-k_2+2k_1=2
$$

Substitute $k_2=7$:

$$
3-7+2k_1=2
$$

$$
-4+2k_1=2
$$

$$
2k_1=6
$$

$$
k_1=3
$$

---

## Final Answer

$$
K=
\begin{bmatrix}
3 & 7
\end{bmatrix}
$$

The controller is:

$$
u=-Kx
$$

Therefore:

$$
u=
-\begin{bmatrix}
3 & 7
\end{bmatrix}
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

So:

$$
\boxed{
u=-3x_1-7x_2
}
$$

---

# Task 6 — Luenberger Observer

## Problem

Consider the state-space system:

$$
\dot{x}=
\begin{bmatrix}
0 & 1 & 0\\
0 & 0 & 1\\
-5 & -10 & -2
\end{bmatrix}x+
\begin{bmatrix}
0\\
0\\
1
\end{bmatrix}u
$$

$$
y=
\begin{bmatrix}
1 & 0 & 0
\end{bmatrix}x
$$

A controller was designed for this system. Its closed-loop poles are located at:

$$
s=-5+j
$$

$$
s=-5-j
$$

$$
s=-1
$$

Questions:

1. Extend the system using a Luenberger observer that works 10 times faster than the controller. Write all observer poles.
2. Draw a scheme of the system with controller and observer.
3. What is the role of an observer?

---

## Theory

A Luenberger observer estimates the internal state vector $x$ when not all states are directly measured.

The plant is:

$$
\dot{x}=Ax+Bu
$$

$$
y=Cx
$$

The observer is:

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-\hat{y})
$$

where:

$$
\hat{y}=C\hat{x}
$$

Substitute $\hat{y}$:

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

The estimation error is:

$$
\tilde{x}=x-\hat{x}
$$

The error dynamics are:

$$
\dot{\tilde{x}}=(A-LC)\tilde{x}
$$

The observer poles are the eigenvalues of:

$$
A-LC
$$

In practice, observer poles are often chosen faster than controller poles. A common rule is 5 to 10 times faster.

Here, the problem says 10 times faster.

---

## Step 1: Controller poles

Given controller poles:

$$
s_1=-5+j
$$

$$
s_2=-5-j
$$

$$
s_3=-1
$$

---

## Step 2: Choose observer poles 10 times faster

If the observer should be 10 times faster, multiply the real and imaginary parts by 10.

For the first pole:

$$
s_1=-5+j
$$

Multiply by 10:

$$
s_{o1}=10(-5+j)
$$

$$
s_{o1}=-50+10j
$$

For the second pole:

$$
s_2=-5-j
$$

Multiply by 10:

$$
s_{o2}=10(-5-j)
$$

$$
s_{o2}=-50-10j
$$

For the third pole:

$$
s_3=-1
$$

Multiply by 10:

$$
s_{o3}=10(-1)
$$

$$
s_{o3}=-10
$$

---

## Answer to Question 1

The observer poles should be:

$$
\boxed{
s_{o1}=-50+10j,\qquad
s_{o2}=-50-10j,\qquad
s_{o3}=-10
}
$$

---

## Question 2: Scheme of controller with observer

A simple block diagram in text form:

```text
              +-------------------+
              |                   |
              |   State feedback  |
              |   u = -K x_hat    |
              |                   |
              +---------+---------+
                        |
                        v
                  +-----+-----+
                  |           |
                  |   Plant   |
                  |           |
                  | x_dot=Ax+Bu
                  | y=Cx      |
                  +-----+-----+
                        |
                        | y
                        v
              +---------+---------+
              |                   |
              | Luenberger        |
              | Observer          |
              |                   |
              | x_hat_dot =       |
              | A x_hat + Bu      |
              | + L(y-C x_hat)    |
              |                   |
              +---------+---------+
                        |
                        | x_hat
                        +------------- back to controller
```

Mathematically:

$$
u=-K\hat{x}
$$

The plant is:

$$
\dot{x}=Ax+Bu
$$

$$
y=Cx
$$

The observer is:

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

The controller uses $\hat{x}$ instead of $x$ because the real state vector may not be fully measured.

---

## Question 3: Role of the observer

Required short sentence form:

$$
\boxed{
\text{It estimates the state vector }x\text{ based on the measured output }y\text{ and the known input }u.
}
$$

---

# Task 7 — Desired Characteristic Polynomial from Overshoot and Settling Time

## Problem

Given the open-loop plant:

$$
G(s)=\frac{30}{(s+1)(s+3)(s+6)}
$$

A controller was designed to achieve:

$$
20\%
$$

overshoot and a settling time of:

$$
2\text{ seconds}
$$

using the $2\%$ criterion.

What is the desired characteristic polynomial of the resulting closed-loop system?

---

## Theory

For a dominant second-order closed-loop system, the standard characteristic polynomial is:

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$

where:

- $\zeta$ is the damping ratio,
- $\omega_n$ is the natural frequency.

The percentage overshoot is related to $\zeta$ by:

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

The $2\%$ settling time criterion is:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

---

## Step 1: Convert overshoot to decimal

Given:

$$
M_p=20\%
$$

Convert to decimal:

$$
M_p=0.20
$$

---

## Step 2: Find damping ratio $\zeta$

Use:

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

Substitute:

$$
0.20=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

Take natural logarithm:

$$
\ln(0.20)=
-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}
$$

Since:

$$
\ln(0.20)\approx -1.6094
$$

we have:

$$
1.6094=
\frac{\zeta\pi}{\sqrt{1-\zeta^2}}
$$

A useful direct formula is:

$$
\zeta=
\frac{-\ln(M_p)}
{\sqrt{\pi^2+\ln^2(M_p)}}
$$

Substitute:

$$
\zeta=
\frac{-\ln(0.20)}
{\sqrt{\pi^2+\ln^2(0.20)}}
$$

$$
\zeta=
\frac{1.6094}
{\sqrt{\pi^2+1.6094^2}}
$$

$$
\zeta\approx 0.456
$$

---

## Step 3: Use settling time to find $\omega_n$

For the $2\%$ criterion:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

Given:

$$
T_s=2
$$

Therefore:

$$
2=\frac{4}{\zeta\omega_n}
$$

Multiply both sides by $\zeta\omega_n$:

$$
2\zeta\omega_n=4
$$

Divide by 2:

$$
\zeta\omega_n=2
$$

Thus:

$$
\omega_n=\frac{2}{\zeta}
$$

Substitute:

$$
\omega_n=\frac{2}{0.456}
$$

$$
\omega_n\approx 4.386
$$

---

## Step 4: Build the desired second-order polynomial

The second-order desired polynomial is:

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$

We know:

$$
\zeta\omega_n=2
$$

Therefore:

$$
2\zeta\omega_n=4
$$

Also:

$$
\omega_n^2=(4.386)^2
$$

$$
\omega_n^2\approx 19.24
$$

So:

$$
p_d(s)=s^2+4s+19.24
$$

---

## Step 5: Desired dominant poles

The desired dominant poles are:

$$
s_{1,2}=-\zeta\omega_n\pm j\omega_n\sqrt{1-\zeta^2}
$$

Since:

$$
\zeta\omega_n=2
$$

the real part is:

$$
-2
$$

The imaginary part is:

$$
\omega_n\sqrt{1-\zeta^2}
$$

Substitute values:

$$
4.386\sqrt{1-0.456^2}
$$

$$
4.386\sqrt{1-0.208}
$$

$$
4.386\sqrt{0.792}
$$

$$
4.386\cdot 0.890
$$

$$
\approx 3.904
$$

Thus:

$$
s_{1,2}=-2\pm j3.904
$$

---

## Important Note About the Third-Order Plant

The given plant is third order:

$$
G(s)=\frac{30}{(s+1)(s+3)(s+6)}
$$

Therefore, the actual closed-loop characteristic polynomial may be third order.

However, the overshoot and settling time specifications define only a dominant second-order pair.

To form a complete third-order desired characteristic polynomial, one additional non-dominant pole must be selected.

A typical design rule is to place the extra pole far to the left, for example 5 to 10 times faster than the dominant real part.

The dominant real part is:

$$
-2
$$

So a possible additional pole could be:

$$
s_3=-10
$$

or:

$$
s_3=-20
$$

But the task does not specify this pole.

Thus, the safest answer is the dominant second-order characteristic polynomial:

$$
\boxed{
p_d(s)=s^2+4s+19.24
}
$$

If the teacher expects a third-order polynomial and we choose $s_3=-10$, then:

$$
p_d(s)=(s^2+4s+19.24)(s+10)
$$

Expand:

$$
(s^2+4s+19.24)(s+10)
$$

$$
=s^3+10s^2+4s^2+40s+19.24s+192.4
$$

$$
=s^3+14s^2+59.24s+192.4
$$

So one possible third-order desired polynomial would be:

$$
p_d(s)=s^3+14s^2+59.24s+192.4
$$

But this depends on the chosen extra pole.

---

## Final Answer

Dominant second-order desired polynomial:

$$
\boxed{
p_d(s)=s^2+4s+19.24
}
$$

If a third-order polynomial is required, one extra non-dominant pole must be chosen.

For example, with $s_3=-10$:

$$
\boxed{
p_d(s)=s^3+14s^2+59.24s+192.4
}
$$

---

# Task 8 — Stability of an LTI System and Lyapunov Method

## Problem

Consider:

$$
\dot{x}=Ax
$$

where:

$$
A=
\begin{bmatrix}
-4 & 1\\
4 & -5
\end{bmatrix}
$$

Tasks:

1. Determine whether the system is asymptotically stable, marginally stable, or unstable.
2. Write out the steps used to determine stability of an LTI system using the Lyapunov method.

---

# Part 1 — Stability Using Eigenvalues

## Theory

For an LTI system:

$$
\dot{x}=Ax
$$

the stability depends on the eigenvalues of $A$.

Rules:

1. If all eigenvalues have negative real parts, the system is asymptotically stable.
2. If at least one eigenvalue has positive real part, the system is unstable.
3. If eigenvalues have non-positive real parts and at least one eigenvalue is on the imaginary axis, then the system may be marginally stable depending on multiplicity and Jordan form.

For a $2\times 2$ real matrix, we find eigenvalues from:

$$
\det(\lambda I-A)=0
$$

---

## Step 1: Compute $\lambda I-A$

Given:

$$
A=
\begin{bmatrix}
-4 & 1\\
4 & -5
\end{bmatrix}
$$

Also:

$$
\lambda I=
\begin{bmatrix}
\lambda & 0\\
0 & \lambda
\end{bmatrix}
$$

Then:

$$
\lambda I-A
=
\begin{bmatrix}
\lambda & 0\\
0 & \lambda
\end{bmatrix}
-
\begin{bmatrix}
-4 & 1\\
4 & -5
\end{bmatrix}
$$

So:

$$
\lambda I-A
=
\begin{bmatrix}
\lambda+4 & -1\\
-4 & \lambda+5
\end{bmatrix}
$$

---

## Step 2: Compute the determinant

$$
\det(\lambda I-A)
=
\begin{vmatrix}
\lambda+4 & -1\\
-4 & \lambda+5
\end{vmatrix}
$$

Using $ad-bc$:

$$
\det(\lambda I-A)
=
(\lambda+4)(\lambda+5)-(-1)(-4)
$$

Since:

$$
(-1)(-4)=4
$$

we get:

$$
\det(\lambda I-A)
=
(\lambda+4)(\lambda+5)-4
$$

Expand:

$$
(\lambda+4)(\lambda+5)
=
\lambda^2+5\lambda+4\lambda+20
$$

$$
=
\lambda^2+9\lambda+20
$$

Therefore:

$$
\det(\lambda I-A)
=
\lambda^2+9\lambda+20-4
$$

$$
=
\lambda^2+9\lambda+16
$$

The characteristic equation is:

$$
\lambda^2+9\lambda+16=0
$$

---

## Step 3: Solve for eigenvalues

Use the quadratic formula:

$$
\lambda=
\frac{-b\pm\sqrt{b^2-4ac}}{2a}
$$

Here:

$$
a=1,\qquad b=9,\qquad c=16
$$

So:

$$
\lambda_{1,2}
=
\frac{-9\pm\sqrt{9^2-4\cdot 1\cdot 16}}{2\cdot 1}
$$

$$
\lambda_{1,2}
=
\frac{-9\pm\sqrt{81-64}}{2}
$$

$$
\lambda_{1,2}
=
\frac{-9\pm\sqrt{17}}{2}
$$

Approximate values:

$$
\sqrt{17}\approx 4.123
$$

Therefore:

$$
\lambda_1=
\frac{-9+4.123}{2}
$$

$$
\lambda_1\approx \frac{-4.877}{2}
$$

$$
\lambda_1\approx -2.438
$$

and:

$$
\lambda_2=
\frac{-9-4.123}{2}
$$

$$
\lambda_2\approx \frac{-13.123}{2}
$$

$$
\lambda_2\approx -6.562
$$

---

## Step 4: Interpret eigenvalues

Both eigenvalues are real and negative:

$$
\lambda_1\approx -2.438<0
$$

$$
\lambda_2\approx -6.562<0
$$

Therefore, both eigenvalues have negative real parts.

---

## Part 1 Final Answer

$$
\boxed{
\text{The system is asymptotically stable.}
}
$$

---

# Part 2 — Lyapunov Method for LTI Systems

## Theory

For the LTI system:

$$
\dot{x}=Ax
$$

a standard Lyapunov candidate is:

$$
V(x)=x^TPx
$$

where:

$$
P=P^T>0
$$

This means that $P$ is symmetric positive definite.

The derivative of $V$ along system trajectories is:

$$
\dot{V}
=
\dot{x}^TPx+x^TP\dot{x}
$$

Since:

$$
\dot{x}=Ax
$$

we get:

$$
\dot{x}^T=(Ax)^T=x^TA^T
$$

Substitute:

$$
\dot{V}
=
x^TA^TPx+x^TPAx
$$

Factor out $x^T$ and $x$:

$$
\dot{V}
=
x^T(A^TP+PA)x
$$

To make $\dot{V}$ negative definite, choose:

$$
A^TP+PA=-Q
$$

where:

$$
Q=Q^T>0
$$

Then:

$$
\dot{V}
=
-x^TQx
$$

Since $Q>0$:

$$
x^TQx>0
$$

for all $x\neq 0$.

Therefore:

$$
\dot{V}<0
$$

for all $x\neq 0$.

This proves asymptotic stability.

---

## Step-by-Step Procedure

### Step 1: Choose a positive definite matrix $Q$

Usually choose:

$$
Q=I
$$

For a two-dimensional system:

$$
Q=
\begin{bmatrix}
1 & 0\\
0 & 1
\end{bmatrix}
$$

---

### Step 2: Solve the Lyapunov equation

Solve:

$$
A^TP+PA=-Q
$$

where $P$ is unknown.

For a two-dimensional system, assume:

$$
P=
\begin{bmatrix}
p_{11} & p_{12}\\
p_{12} & p_{22}
\end{bmatrix}
$$

because $P$ must be symmetric.

---

### Step 3: Check whether $P$ is positive definite

For a $2\times 2$ symmetric matrix:

$$
P=
\begin{bmatrix}
p_{11} & p_{12}\\
p_{12} & p_{22}
\end{bmatrix}
$$

positive definiteness can be checked using leading principal minors:

$$
p_{11}>0
$$

and:

$$
\det(P)>0
$$

If both are true, then:

$$
P>0
$$

---

### Step 4: Define the Lyapunov function

Use:

$$
V(x)=x^TPx
$$

If $P>0$, then:

$$
V(x)>0
$$

for all $x\neq 0$, and:

$$
V(0)=0
$$

Thus, $V$ is positive definite.

---

### Step 5: Compute $\dot{V}$

Using:

$$
\dot{x}=Ax
$$

we get:

$$
\dot{V}
=
x^T(A^TP+PA)x
$$

Since $P$ satisfies:

$$
A^TP+PA=-Q
$$

then:

$$
\dot{V}
=
-x^TQx
$$

---

### Step 6: Conclude stability

If:

$$
Q>0
$$

then:

$$
x^TQx>0
$$

for all $x\neq 0$.

Therefore:

$$
\dot{V}<0
$$

for all $x\neq 0$.

So the system is asymptotically stable.

---

## Final Lyapunov Method Statement

For the LTI system:

$$
\dot{x}=Ax
$$

if for any chosen symmetric positive definite matrix $Q$, the Lyapunov equation:

$$
A^TP+PA=-Q
$$

has a symmetric positive definite solution:

$$
P=P^T>0
$$

then:

$$
V(x)=x^TPx
$$

is a valid Lyapunov function and the system is asymptotically stable.

Final statement:

$$
\boxed{
\text{If there exists }P=P^T>0\text{ such that }A^TP+PA=-Q,\;Q=Q^T>0,
\text{ then the LTI system is asymptotically stable.}
}
$$

---

# Final Summary of Answers

## Task 1

$$
\boxed{
e\in\mathbb{R},\qquad
f\in\mathbb{R}\setminus\left\{-\frac12,1\right\}
}
$$

## Task 2

$$
\boxed{
(0,0),\quad (0,1),\quad (0,-1)
}
$$

## Task 3

$$
\boxed{
\text{The first Lyapunov method is inconclusive because }\lambda_{1,2}=\pm j.
}
$$

## Task 4

$$
\boxed{
\text{The origin is globally asymptotically stable.}
}
$$

## Task 5

$$
\boxed{
K=\begin{bmatrix}3&7\end{bmatrix}
}
$$

$$
\boxed{
u=-3x_1-7x_2
}
$$

## Task 6

$$
\boxed{
s_o=\{-50+10j,\;-50-10j,\;-10\}
}
$$

Observer role:

$$
\boxed{
\text{It estimates the state vector }x\text{ based on measured output }y\text{ and known input }u.
}
$$

## Task 7

Dominant second-order polynomial:

$$
\boxed{
s^2+4s+19.24
}
$$

Possible third-order polynomial if choosing extra pole $s_3=-10$:

$$
\boxed{
s^3+14s^2+59.24s+192.4
}
$$

## Task 8

$$
\boxed{
\text{The system is asymptotically stable.}
}
$$
