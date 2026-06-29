# Control Theory Study Guide by Topic

This guide is based on the same Control Theory test, but instead of solving task by task, it groups the material by topic.

Each topic contains:

1. What kind of exam tasks belong to this topic.
2. Simple explanation in words.
3. Standard solution steps.
4. Mathematical template.
5. Special cases.
6. Things to pay attention to.
7. Connection to the tasks from the test.

The formatting is prepared for Obsidian:

- Inline math uses `$...$`.
- Display math uses `$$...$$`.
- No `\[` or `\]` delimiters are used.

---

# 1. Linearization

## 1.1 What kind of tasks belong here?

Linearization appears when the system is nonlinear and the task asks you to analyze behavior near an equilibrium point.

Typical exam wording:

- "Linearize the system around the equilibrium point."
- "Use the first Lyapunov method."
- "Find the Jacobian matrix."
- "Decide stability around $(0,0)$."
- "Analyze local stability."

In the test, this appears mainly in **Task 3**.

---

## 1.2 Simple idea in words

A nonlinear system can be difficult to analyze directly.

So, close to an equilibrium point, we replace the nonlinear system by a linear approximation.

This linear approximation is obtained using the Jacobian matrix.

The nonlinear system:

$$
\dot{x}=f(x)
$$

is approximated near an equilibrium point $x_e$ by:

$$
\dot{x}=Ax
$$

where:

$$
A=
\left.
\frac{\partial f}{\partial x}
\right|_{x=x_e}
$$

The matrix $A$ is the Jacobian evaluated at the equilibrium point.

---

## 1.3 Typical steps for a linearization task

### Step 1: Write the nonlinear system in vector form

For example, if:

$$
\dot{x}_1=f_1(x_1,x_2)
$$

$$
\dot{x}_2=f_2(x_1,x_2)
$$

then:

$$
\dot{x}=
\begin{bmatrix}
\dot{x}_1\\
\dot{x}_2
\end{bmatrix}
=
\begin{bmatrix}
f_1(x_1,x_2)\\
f_2(x_1,x_2)
\end{bmatrix}
$$

---

### Step 2: Find the equilibrium point

At an equilibrium point, all derivatives are zero.

So solve:

$$
\dot{x}_1=0
$$

$$
\dot{x}_2=0
$$

or generally:

$$
f(x_e)=0
$$

If the task already gives the equilibrium point, you can use it directly, but it is still good to verify it.

---

### Step 3: Compute the Jacobian matrix

For a two-state nonlinear system:

$$
f(x)=
\begin{bmatrix}
f_1(x_1,x_2)\\
f_2(x_1,x_2)
\end{bmatrix}
$$

the Jacobian is:

$$
J(x)=
\begin{bmatrix}
\frac{\partial f_1}{\partial x_1} &
\frac{\partial f_1}{\partial x_2}\\
\frac{\partial f_2}{\partial x_1} &
\frac{\partial f_2}{\partial x_2}
\end{bmatrix}
$$

This means:

- first row comes from derivatives of $f_1$,
- second row comes from derivatives of $f_2$,
- first column means derivatives with respect to $x_1$,
- second column means derivatives with respect to $x_2$.

---

### Step 4: Substitute the equilibrium point

After finding the symbolic Jacobian $J(x)$, substitute the equilibrium point.

If the equilibrium point is:

$$
x_e=(0,0)
$$

then:

$$
A=J(0,0)
$$

This gives the linearized system:

$$
\dot{x}=Ax
$$

---

### Step 5: Use the linearized system

Usually you then compute eigenvalues:

$$
\det(\lambda I-A)=0
$$

The eigenvalues tell you about local stability by the indirect Lyapunov method.

---

## 1.4 Example from the test

The system from Task 3 is:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-x_1+x_1^3
$$

Write:

$$
f_1=x_2
$$

$$
f_2=-x_1+x_1^3
$$

The Jacobian is:

$$
J(x)=
\begin{bmatrix}
\frac{\partial x_2}{\partial x_1} &
\frac{\partial x_2}{\partial x_2}\\
\frac{\partial (-x_1+x_1^3)}{\partial x_1} &
\frac{\partial (-x_1+x_1^3)}{\partial x_2}
\end{bmatrix}
$$

Calculate each derivative:

$$
\frac{\partial x_2}{\partial x_1}=0
$$

$$
\frac{\partial x_2}{\partial x_2}=1
$$

$$
\frac{\partial (-x_1+x_1^3)}{\partial x_1}
=
-1+3x_1^2
$$

$$
\frac{\partial (-x_1+x_1^3)}{\partial x_2}=0
$$

So:

$$
J(x)=
\begin{bmatrix}
0 & 1\\
-1+3x_1^2 & 0
\end{bmatrix}
$$

At $(0,0)$:

$$
A=J(0,0)=
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}
$$

---

## 1.5 Special cases

### Special case 1: More than one equilibrium point

Sometimes the system has several equilibrium points.

Then you must evaluate the Jacobian separately at every equilibrium.

Example:

$$
x_e^{(1)}=(0,0)
$$

$$
x_e^{(2)}=(0,1)
$$

$$
x_e^{(3)}=(0,-1)
$$

Then calculate:

$$
J(x_e^{(1)})
$$

$$
J(x_e^{(2)})
$$

$$
J(x_e^{(3)})
$$

Each equilibrium may have different stability.

---

### Special case 2: Equilibrium not at the origin

If the equilibrium point is not $(0,0)$, do not automatically substitute zeros.

For example, if:

$$
x_e=(2,-1)
$$

then:

$$
A=J(2,-1)
$$

---

### Special case 3: Linearization gives zero or imaginary eigenvalues

If after linearization you get:

$$
\lambda=0
$$

or:

$$
\lambda=\pm j\omega
$$

then the indirect method is inconclusive.

This does not automatically mean stable or unstable.

---

## 1.6 Things to pay attention to

- Always find or verify the equilibrium point first.
- Do not evaluate the Jacobian before knowing the equilibrium.
- Do not confuse $f(x)$ with $f_1$ and $f_2$.
- Be careful with derivatives of nonlinear terms like $x_1^3$.
- Remember:

$$
\frac{d}{dx_1}x_1^3=3x_1^2
$$

- If the system has multiple equilibria, repeat the linearization for each one.

---

# 2. Properties

This topic includes controllability, observability, and the question of whether arbitrary pole placement is possible.

---

## 2.1 What kind of tasks belong here?

Typical exam wording:

- "Can the controller poles be placed arbitrarily?"
- "Can the estimator poles be placed arbitrarily?"
- "Check controllability."
- "Check observability."
- "Determine for which parameter values the system is observable."
- "Determine for which parameter values the system is controllable."

In the test, this appears mainly in **Task 1**.

---

## 2.2 Simple idea in words

There are two very important properties:

1. Controllability
2. Observability

They answer different questions.

---

## 2.3 Controllability

Controllability tells us whether the input $u$ can influence all states of the system.

The system:

$$
\dot{x}=Ax+Bu
$$

is controllable if the pair $(A,B)$ is controllable.

For a system of order $n$, the controllability matrix is:

$$
\mathcal{C}=
\begin{bmatrix}
B & AB & A^2B & \dots & A^{n-1}B
\end{bmatrix}
$$

The system is controllable if:

$$
\operatorname{rank}(\mathcal{C})=n
$$

For a two-state system:

$$
\mathcal{C}=
\begin{bmatrix}
B & AB
\end{bmatrix}
$$

If $\mathcal{C}$ is a $2\times 2$ matrix, controllability can be checked by:

$$
\det(\mathcal{C})\neq 0
$$

---

## 2.4 Observability

Observability tells us whether we can reconstruct the internal state $x$ from the measured output $y$.

The system:

$$
\dot{x}=Ax+Bu
$$

$$
y=Cx
$$

is observable if the pair $(A,C)$ is observable.

For a system of order $n$, the observability matrix is:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA\\
CA^2\\
\vdots\\
CA^{n-1}
\end{bmatrix}
$$

The system is observable if:

$$
\operatorname{rank}(\mathcal{O})=n
$$

For a two-state system:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

If $\mathcal{O}$ is a $2\times 2$ matrix, observability can be checked by:

$$
\det(\mathcal{O})\neq 0
$$

---

## 2.5 Which property should you use?

This is one of the most important exam decisions.

### If the task asks about controller poles

Use controllability:

$$
(A,B)
$$

### If the task asks about estimator poles or observer poles

Use observability:

$$
(A,C)
$$

---

## 2.6 Typical steps for observability tasks

### Step 1: Identify $A$ and $C$

From:

$$
\dot{x}=Ax+Bu
$$

$$
y=Cx
$$

extract $A$ and $C$.

---

### Step 2: Build the observability matrix

For two states:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

---

### Step 3: Calculate $CA$

Multiply:

$$
C A
$$

Be careful: $C$ is a row vector and $A$ is a matrix.

---

### Step 4: Compute determinant or rank

For a $2\times 2$ observability matrix:

$$
\det(\mathcal{O})\neq 0
$$

---

### Step 5: Solve parameter restrictions

If determinant depends on a parameter, solve:

$$
\det(\mathcal{O})\neq 0
$$

---

## 2.7 Example from the test

Given:

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

The task asks about estimator poles.

Estimator means observer.

Observer means observability.

So we use:

$$
(A,C)
$$

not $(A,B)$.

Build:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

Calculate:

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

The determinant is:

$$
\det(\mathcal{O})
=
f(2f+4)-1(5f+1)
$$

$$
\det(\mathcal{O})
=
2f^2+4f-5f-1
$$

$$
\det(\mathcal{O})
=
2f^2-f-1
$$

Factor:

$$
2f^2-f-1=(2f+1)(f-1)
$$

So:

$$
(2f+1)(f-1)\neq 0
$$

Thus:

$$
f\neq -\frac{1}{2}
$$

and:

$$
f\neq 1
$$

The parameter $e$ is in $B$ only, so it does not affect observability.

Final result:

$$
e\in\mathbb{R}
$$

$$
f\in\mathbb{R}\setminus\left\{-\frac{1}{2},1\right\}
$$

---

## 2.8 Special cases

### Special case 1: Parameter appears only in $B$

Then it affects controllability but not observability.

So if the task asks about observer or estimator, the parameter in $B$ may be irrelevant.

---

### Special case 2: Parameter appears only in $C$

Then it affects observability but not controllability.

---

### Special case 3: Determinant equals zero for some parameter values

If:

$$
\det(\mathcal{O})=0
$$

then the system is not observable for those parameter values.

For those values, arbitrary estimator pole placement is not possible.

---

## 2.9 Things to pay attention to

- Estimator = observer.
- Observer pole placement requires observability.
- Controller pole placement requires controllability.
- Do not use $B$ when checking observability.
- Do not use $C$ when checking controllability.
- If a parameter does not appear in the property matrix, it does not affect that property.

---

# 3. Stability — Indirect Lyapunov Method

The indirect Lyapunov method is basically stability analysis using linearization.

---

## 3.1 What kind of tasks belong here?

Typical exam wording:

- "Use the first Lyapunov method."
- "Use the indirect Lyapunov method."
- "Linearize and conclude stability."
- "Determine stability around an equilibrium point."

In the test, this appears in **Task 3**.

---

## 3.2 Simple idea in words

The method says:

Instead of analyzing the full nonlinear system, look at its linear approximation near the equilibrium.

If the linear approximation is clearly stable or clearly unstable, then the nonlinear system has the same local behavior.

But if the linear approximation is borderline, the method cannot decide.

---

## 3.3 Mathematical idea

For:

$$
\dot{x}=f(x)
$$

and equilibrium:

$$
f(x_e)=0
$$

linearize:

$$
\dot{x}=Ax
$$

where:

$$
A=
\left.
\frac{\partial f}{\partial x}
\right|_{x=x_e}
$$

Then compute eigenvalues of $A$:

$$
\det(\lambda I-A)=0
$$

---

## 3.4 Stability rules

### Case 1: All eigenvalues have negative real parts

If:

$$
\operatorname{Re}(\lambda_i)<0
$$

for all $i$, then:

$$
\boxed{\text{The nonlinear system is locally asymptotically stable.}}
$$

---

### Case 2: At least one eigenvalue has positive real part

If:

$$
\operatorname{Re}(\lambda_i)>0
$$

for at least one eigenvalue, then:

$$
\boxed{\text{The nonlinear system is unstable.}}
$$

---

### Case 3: Eigenvalues on imaginary axis

If at least one eigenvalue has zero real part and none have positive real part, then:

$$
\boxed{\text{The method is inconclusive.}}
$$

Examples:

$$
\lambda=\pm j
$$

or:

$$
\lambda=0
$$

---

## 3.5 Typical solution template

### Step 1

Find equilibrium:

$$
f(x_e)=0
$$

### Step 2

Compute Jacobian:

$$
J(x)=\frac{\partial f}{\partial x}
$$

### Step 3

Evaluate:

$$
A=J(x_e)
$$

### Step 4

Find eigenvalues:

$$
\det(\lambda I-A)=0
$$

### Step 5

Write conclusion using the stability rules.

---

## 3.6 Example from the test

For:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-x_1+x_1^3
$$

the Jacobian at the origin is:

$$
A=
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}
$$

Find eigenvalues:

$$
\det(\lambda I-A)=0
$$

$$
\lambda I-A=
\begin{bmatrix}
\lambda & -1\\
1 & \lambda
\end{bmatrix}
$$

$$
\det(\lambda I-A)=\lambda^2+1
$$

So:

$$
\lambda^2+1=0
$$

$$
\lambda_{1,2}=\pm j
$$

The eigenvalues are purely imaginary.

Therefore:

$$
\boxed{\text{The indirect Lyapunov method is inconclusive.}}
$$

---

## 3.7 Special cases

### Pure imaginary eigenvalues

If:

$$
\lambda=\pm j\omega
$$

the method is inconclusive.

Do not write asymptotically stable.

---

### Zero eigenvalue

If:

$$
\lambda=0
$$

the method is inconclusive.

---

### Repeated eigenvalue with zero real part

If an eigenvalue has zero real part, the indirect method usually cannot decide without extra analysis.

---

## 3.8 Things to pay attention to

- "Inconclusive" is a valid exam answer when using the first Lyapunov method.
- Purely imaginary eigenvalues do not imply asymptotic stability.
- The indirect method only gives local conclusions.
- If the method is inconclusive, another method may still prove stability or instability.

---

# 4. Stability — Direct Lyapunov Method

This is used when a Lyapunov function is given or when you are asked to prove stability directly.

---

## 4.1 What kind of tasks belong here?

Typical exam wording:

- "Use the Lyapunov function..."
- "Evaluate stability using the Lyapunov function..."
- "Show that the origin is stable..."
- "Use direct Lyapunov method..."
- "Use LaSalle's invariance principle..."

In the test, this appears in **Task 4**.

---

## 4.2 Simple idea in words

A Lyapunov function behaves like an energy function.

If the energy is always positive except at the origin, and it decreases over time, then the system moves toward the origin.

The function:

$$
V(x)
$$

measures the "energy" of the system.

Its derivative:

$$
\dot{V}(x)
$$

tells whether the energy increases or decreases.

---

## 4.3 What must be checked?

### Condition 1: $V$ is positive definite

This means:

$$
V(0)=0
$$

and:

$$
V(x)>0
$$

for every:

$$
x\neq 0
$$

---

### Condition 2: $\dot{V}$ is negative

Compute:

$$
\dot{V}
$$

If:

$$
\dot{V}<0
$$

for all $x\neq 0$, then the origin is asymptotically stable.

If:

$$
\dot{V}\leq 0
$$

then the origin is stable, but asymptotic stability requires more analysis, often LaSalle.

---

## 4.4 Typical steps

### Step 1: Write the Lyapunov function

Example:

$$
V(x_1,x_2)=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

---

### Step 2: Check positive definiteness

Check that every term is nonnegative and that $V=0$ only at the origin.

For example:

$$
a>0
$$

and:

$$
x_1^4\geq 0
$$

so:

$$
a\frac{x_1^4}{4}\geq 0
$$

Also:

$$
\frac{x_2^2}{2}\geq 0
$$

So:

$$
V(x)\geq 0
$$

Then check:

$$
V(x)=0
$$

only when:

$$
x_1=0,\qquad x_2=0
$$

Therefore $V$ is positive definite.

---

### Step 3: Compute $\dot{V}$

Use the chain rule:

$$
\dot{V}
=
\frac{\partial V}{\partial x_1}\dot{x}_1
+
\frac{\partial V}{\partial x_2}\dot{x}_2
$$

For more states:

$$
\dot{V}
=
\nabla V(x)^T\dot{x}
$$

---

### Step 4: Substitute the system equations

If:

$$
\dot{x}_1=x_2
$$

and:

$$
\dot{x}_2=-ax_1^3-bx_2
$$

then substitute these into $\dot{V}$.

---

### Step 5: Simplify

Terms often cancel.

In the test example:

$$
\dot{V}=-bx_2^2
$$

---

### Step 6: Interpret $\dot{V}$

If:

$$
\dot{V}=-bx_2^2
$$

and:

$$
b>0
$$

then:

$$
\dot{V}\leq 0
$$

This is negative semidefinite.

---

## 4.5 LaSalle's invariance principle

If $\dot{V}$ is only negative semidefinite, use LaSalle.

### Step 1: Find where $\dot{V}=0$

For:

$$
\dot{V}=-bx_2^2
$$

we get:

$$
-bx_2^2=0
$$

Since:

$$
b>0
$$

this means:

$$
x_2=0
$$

So:

$$
S=\{(x_1,x_2):x_2=0\}
$$

---

### Step 2: Find the largest invariant set inside $S$

If:

$$
x_2=0
$$

then:

$$
\dot{x}_1=x_2=0
$$

and:

$$
\dot{x}_2=-ax_1^3-bx_2
$$

Since $x_2=0$:

$$
\dot{x}_2=-ax_1^3
$$

To stay inside $x_2=0$, we need:

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

So the largest invariant set is only:

$$
(0,0)
$$

Therefore, by LaSalle:

$$
\boxed{\text{The origin is asymptotically stable.}}
$$

---

## 4.6 Global asymptotic stability

To say stability is global, check if $V$ is radially unbounded.

This means:

$$
V(x)\to\infty
$$

as:

$$
\|x\|\to\infty
$$

For:

$$
V=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

if $|x_1|\to\infty$, then:

$$
a\frac{x_1^4}{4}\to\infty
$$

If $|x_2|\to\infty$, then:

$$
\frac{x_2^2}{2}\to\infty
$$

So $V$ is radially unbounded.

Thus the stability is global.

Final result:

$$
\boxed{\text{The origin is globally asymptotically stable.}}
$$

---

## 4.7 Special cases

### Case 1: $\dot{V}<0$

Direct conclusion:

$$
\boxed{\text{Asymptotically stable}}
$$

---

### Case 2: $\dot{V}\leq 0$

You can conclude stability.

For asymptotic stability, use LaSalle.

---

### Case 3: $\dot{V}=0$ on a large set

Check whether that set is invariant.

Do not automatically say asymptotically stable.

---

### Case 4: $V$ is not positive definite

Then it is not a valid Lyapunov function for proving stability.

---

## 4.8 Things to pay attention to

- Always check $V$ before $\dot{V}$.
- Negative semidefinite is not the same as negative definite.
- If $\dot{V}\leq 0$, think about LaSalle.
- To say global, check radial unboundedness.
- Do not forget that $a>0$ and $b>0$ matter.

---

# 5. State Feedback

State feedback is used to place closed-loop poles by choosing a gain matrix $K$.

---

## 5.1 What kind of tasks belong here?

Typical exam wording:

- "Design a state feedback controller."
- "Find $K$."
- "Use $u=-Kx$."
- "Place closed-loop poles at..."
- "Closed-loop eigenvalues should be..."

In the test, this appears in **Task 5**.

---

## 5.2 Simple idea in words

The original system is:

$$
\dot{x}=Ax+Bu
$$

We choose input:

$$
u=-Kx
$$

This changes the system dynamics to:

$$
\dot{x}=(A-BK)x
$$

The goal is to choose $K$ so that the eigenvalues of $A-BK$ are exactly where we want them.

---

## 5.3 Mathematical setup

Let:

$$
K=
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
$$

Then:

$$
u=-Kx
$$

and:

$$
A_{cl}=A-BK
$$

The desired poles define the desired polynomial.

If desired poles are:

$$
\lambda_1,\lambda_2
$$

then:

$$
p_d(s)=(s-\lambda_1)(s-\lambda_2)
$$

---

## 5.4 Typical steps

### Step 1: Define $K$

For a two-state, one-input system:

$$
K=
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
$$

---

### Step 2: Compute $BK$

If:

$$
B=
\begin{bmatrix}
0\\
1
\end{bmatrix}
$$

then:

$$
BK=
\begin{bmatrix}
0\\
1
\end{bmatrix}
\begin{bmatrix}
k_1 & k_2
\end{bmatrix}
=
\begin{bmatrix}
0 & 0\\
k_1 & k_2
\end{bmatrix}
$$

---

### Step 3: Compute $A-BK$

If:

$$
A=
\begin{bmatrix}
1 & 2\\
0 & 3
\end{bmatrix}
$$

then:

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

$$
A-BK=
\begin{bmatrix}
1 & 2\\
-k_1 & 3-k_2
\end{bmatrix}
$$

---

### Step 4: Compute characteristic polynomial

Compute:

$$
\det(sI-(A-BK))
$$

For the example:

$$
sI-(A-BK)=
\begin{bmatrix}
s-1 & -2\\
k_1 & s-3+k_2
\end{bmatrix}
$$

Then:

$$
\det(sI-(A-BK))
=
(s-1)(s-3+k_2)+2k_1
$$

After expansion:

$$
p(s)=s^2+(k_2-4)s+(3-k_2+2k_1)
$$

---

### Step 5: Build desired polynomial

If desired poles are:

$$
-1,\quad -2
$$

then:

$$
p_d(s)=(s+1)(s+2)
$$

$$
p_d(s)=s^2+3s+2
$$

---

### Step 6: Compare coefficients

Set:

$$
s^2+(k_2-4)s+(3-k_2+2k_1)
=
s^2+3s+2
$$

Compare coefficient of $s$:

$$
k_2-4=3
$$

$$
k_2=7
$$

Compare constant term:

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

Thus:

$$
K=
\begin{bmatrix}
3 & 7
\end{bmatrix}
$$

Controller:

$$
u=-3x_1-7x_2
$$

---

## 5.5 Special cases

### Case 1: System not controllable

If the system is not controllable, arbitrary pole placement is not possible.

Before pole placement, the condition is:

$$
\operatorname{rank}(\mathcal{C})=n
$$

---

### Case 2: Sign convention

The task usually defines:

$$
u=-Kx
$$

Then the closed-loop matrix is:

$$
A-BK
$$

If instead the task used:

$$
u=Kx
$$

then the closed-loop matrix would be:

$$
A+BK
$$

So always check the sign.

---

### Case 3: Higher-order systems

For a third-order system, $K$ has three gains:

$$
K=
\begin{bmatrix}
k_1 & k_2 & k_3
\end{bmatrix}
$$

The desired polynomial has degree three.

---

## 5.6 Things to pay attention to

- Always write $A_{cl}=A-BK$ for $u=-Kx$.
- Do not forget to compute $BK$ with correct dimensions.
- Match coefficients carefully.
- Desired poles $-1,-2$ give $(s+1)(s+2)$, not $(s-1)(s-2)$.
- If the system is not controllable, pole placement cannot be arbitrary.

---

# 6. Observer

Observer design is used when not all states are measured.

---

## 6.1 What kind of tasks belong here?

Typical exam wording:

- "Design a Luenberger observer."
- "Observer should be 10 times faster."
- "Write observer poles."
- "What is the role of observer?"
- "Draw controller with observer."
- "Estimator poles."

In the test, this appears in **Task 6** and also relates to **Task 1**.

---

## 6.2 Simple idea in words

A controller often needs the full state vector $x$.

But in real systems, we may only measure output:

$$
y=Cx
$$

The observer estimates the missing states.

The estimate is called:

$$
\hat{x}
$$

The controller can then use:

$$
u=-K\hat{x}
$$

instead of:

$$
u=-Kx
$$

---

## 6.3 Observer equation

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

where:

- $\hat{x}$ is the estimated state,
- $L$ is the observer gain,
- $y$ is the measured output,
- $C\hat{x}$ is the estimated output.

The estimated output is:

$$
\hat{y}=C\hat{x}
$$

So the correction term is:

$$
y-\hat{y}=y-C\hat{x}
$$

This is the output estimation error.

---

## 6.4 Observer error dynamics

Define the estimation error:

$$
\tilde{x}=x-\hat{x}
$$

Then the error dynamics are:

$$
\dot{\tilde{x}}=(A-LC)\tilde{x}
$$

Therefore, observer poles are the eigenvalues of:

$$
A-LC
$$

To place observer poles arbitrarily, the pair $(A,C)$ must be observable.

---

## 6.5 Typical steps for observer pole task

### Step 1: Write the controller poles

Example from the test:

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

### Step 2: Apply "10 times faster"

If observer must be 10 times faster, multiply each pole by 10.

First pole:

$$
10(-5+j)=-50+10j
$$

Second pole:

$$
10(-5-j)=-50-10j
$$

Third pole:

$$
10(-1)=-10
$$

---

### Step 3: Write observer poles

$$
s_{o1}=-50+10j
$$

$$
s_{o2}=-50-10j
$$

$$
s_{o3}=-10
$$

So:

$$
\boxed{
s_o=\{-50+10j,\;-50-10j,\;-10\}
}
$$

---

### Step 4: Write the observer equation

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

---

### Step 5: Explain role of observer

Exam sentence:

$$
\boxed{
\text{It estimates the state vector }x\text{ based on the measured output }y\text{ and known input }u.
}
$$

---

## 6.6 Diagram for observer with controller

A simple text diagram:

```text
              +----------------------+
              |                      |
              |   Controller         |
              |   u = -K x_hat       |
              |                      |
              +----------+-----------+
                         |
                         v
                  +------+------+
                  |             |
                  |   Plant     |
                  |             |
                  | x_dot=Ax+Bu |
                  | y=Cx        |
                  +------+------+
                         |
                         | y
                         v
              +----------+-----------+
              |                      |
              | Luenberger Observer |
              |                      |
              | x_hat_dot =          |
              | A x_hat + Bu         |
              | + L(y-C x_hat)       |
              |                      |
              +----------+-----------+
                         |
                         | x_hat
                         +------ back to controller
```

---

## 6.7 Special cases

### Case 1: Observer 5 times faster

If controller pole is:

$$
-2+3j
$$

then observer pole 5 times faster is:

$$
-10+15j
$$

---

### Case 2: Observer 10 times faster

If controller pole is:

$$
-2+3j
$$

then observer pole 10 times faster is:

$$
-20+30j
$$

---

### Case 3: Complex conjugate poles

If one pole is:

$$
-5+j
$$

the other must be:

$$
-5-j
$$

Observer poles should also remain conjugate:

$$
-50+10j
$$

$$
-50-10j
$$

---

### Case 4: Observer possible only if observable

Observer pole placement requires:

$$
\operatorname{rank}(\mathcal{O})=n
$$

where:

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA\\
\vdots\\
CA^{n-1}
\end{bmatrix}
$$

---

## 6.8 Things to pay attention to

- Observer uses $A$ and $C$, not $A$ and $B$.
- Observer poles should be faster, meaning farther left in the complex plane.
- "10 times faster" usually means multiply pole locations by 10.
- Use $\hat{x}$ in the controller if real $x$ is not measured.
- The observer estimates states; it does not directly control the plant.

---

# 7. Bonus Topic — Equilibrium Points

This topic appears in **Task 2** and often comes before linearization.

---

## 7.1 Simple idea

An equilibrium point is a state where the system does not move.

That means:

$$
\dot{x}=0
$$

For a two-state system:

$$
\dot{x}_1=0
$$

$$
\dot{x}_2=0
$$

---

## 7.2 Typical steps

### Step 1: Set derivatives equal to zero

If:

$$
\dot{x}_1=x_2(1-x_2^2)
$$

$$
\dot{x}_2=x_1
$$

then solve:

$$
x_2(1-x_2^2)=0
$$

$$
x_1=0
$$

---

### Step 2: Solve each equation

From:

$$
x_1=0
$$

we immediately get:

$$
x_1=0
$$

From:

$$
x_2(1-x_2^2)=0
$$

we get:

$$
x_2=0
$$

or:

$$
1-x_2^2=0
$$

So:

$$
x_2^2=1
$$

$$
x_2=\pm 1
$$

---

### Step 3: Combine results

Since $x_1=0$, the equilibria are:

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

## 7.3 Things to pay attention to

- A nonlinear system can have more than one equilibrium.
- Do not assume the only equilibrium is the origin.
- Factor equations carefully.
- If you later linearize, do it separately at each equilibrium.

---

# 8. Bonus Topic — Second-Order Design from Overshoot and Settling Time

This topic appears in **Task 7**.

---

## 8.1 What kind of tasks belong here?

Typical wording:

- "20% overshoot"
- "settling time of 2 seconds"
- "2% criterion"
- "desired characteristic polynomial"
- "dominant second-order poles"

---

## 8.2 Simple idea

Overshoot gives the damping ratio $\zeta$.

Settling time gives the natural frequency $\omega_n$.

Then the desired second-order polynomial is:

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$

---

## 8.3 Important formulas

Percentage overshoot:

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

Direct damping ratio formula:

$$
\zeta=
\frac{-\ln(M_p)}
{\sqrt{\pi^2+\ln^2(M_p)}}
$$

Settling time using the $2\%$ criterion:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

Standard second-order polynomial:

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$

---

## 8.4 Typical steps

### Step 1: Convert overshoot

If overshoot is $20\%$, then:

$$
M_p=0.20
$$

---

### Step 2: Calculate $\zeta$

$$
\zeta=
\frac{-\ln(0.20)}
{\sqrt{\pi^2+\ln^2(0.20)}}
$$

$$
\zeta\approx 0.456
$$

---

### Step 3: Use settling time

Given:

$$
T_s=2
$$

Use:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

So:

$$
2=\frac{4}{\zeta\omega_n}
$$

$$
\zeta\omega_n=2
$$

$$
\omega_n=\frac{2}{\zeta}
$$

$$
\omega_n\approx 4.386
$$

---

### Step 4: Build polynomial

Since:

$$
2\zeta\omega_n=4
$$

and:

$$
\omega_n^2\approx 19.24
$$

the desired second-order polynomial is:

$$
\boxed{
s^2+4s+19.24
}
$$

---

## 8.5 Special case: plant is third order

If the plant is third order, the dominant second-order specs give only two poles.

You may need to choose an additional non-dominant pole.

Example:

$$
s_3=-10
$$

Then:

$$
p_d(s)=(s^2+4s+19.24)(s+10)
$$

Expanding:

$$
p_d(s)=s^3+14s^2+59.24s+192.4
$$

But if the task does not specify the third pole, the safest answer is to state the dominant second-order polynomial and mention that an extra pole is needed for a complete third-order polynomial.

---

## 8.6 Things to pay attention to

- Convert percent overshoot to decimal.
- $20\%$ means $0.20$, not $20$.
- The $2\%$ settling time formula is:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

- A third-order plant needs a third pole if a full third-order polynomial is required.
- If no third pole is specified, mention that it must be selected.

---

# 9. Final Exam Recognition Checklist

Use this section to quickly identify what method to apply.

## If you see nonlinear equations

Think:

$$
\dot{x}=f(x)
$$

Possible tasks:

- find equilibrium,
- linearize,
- Lyapunov method.

---

## If you see "equilibrium points"

Set:

$$
\dot{x}=0
$$

Solve all equations.

---

## If you see "first Lyapunov method"

Do:

1. equilibrium,
2. Jacobian,
3. eigenvalues,
4. conclusion.

---

## If you see "Lyapunov function"

Do:

1. check $V>0$,
2. compute $\dot{V}$,
3. check sign,
4. use LaSalle if needed.

---

## If you see "estimator poles"

Use observability:

$$
(A,C)
$$

---

## If you see "observer"

Use:

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

and observability.

---

## If you see "state feedback"

Use:

$$
u=-Kx
$$

and:

$$
A_{cl}=A-BK
$$

---

## If you see "controller poles"

Use controllability and pole placement.

---

## If you see "overshoot" and "settling time"

Use:

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

and:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

---

# 10. Common Exam Mistakes

## Mistake 1: Confusing controllability and observability

Wrong:

Observer poles require controllability.

Correct:

Observer poles require observability.

---

## Mistake 2: Saying purely imaginary eigenvalues mean stable in indirect Lyapunov method

Wrong:

$$
\lambda=\pm j
$$

therefore stable.

Correct:

$$
\lambda=\pm j
$$

therefore the method is inconclusive.

---

## Mistake 3: Forgetting the minus sign in feedback

If:

$$
u=-Kx
$$

then:

$$
A_{cl}=A-BK
$$

not:

$$
A+BK
$$

---

## Mistake 4: Calling negative semidefinite derivative asymptotic stability too early

If:

$$
\dot{V}\leq 0
$$

you may need LaSalle.

---

## Mistake 5: Not checking positive definiteness of $V$

Before using $\dot{V}$, always check that $V$ is positive definite.

---

## Mistake 6: Treating third-order system as fully specified by second-order specs

Overshoot and settling time usually define only the dominant second-order part.

For a third-order plant, one extra pole may be needed.

---

# 11. Quick Formula Sheet

## Observability

$$
\mathcal{O}=
\begin{bmatrix}
C\\
CA\\
\vdots\\
CA^{n-1}
\end{bmatrix}
$$

$$
\operatorname{rank}(\mathcal{O})=n
$$

---

## Controllability

$$
\mathcal{C}=
\begin{bmatrix}
B & AB & \dots & A^{n-1}B
\end{bmatrix}
$$

$$
\operatorname{rank}(\mathcal{C})=n
$$

---

## State feedback

$$
u=-Kx
$$

$$
A_{cl}=A-BK
$$

---

## Observer

$$
\dot{\hat{x}}=A\hat{x}+Bu+L(y-C\hat{x})
$$

---

## Lyapunov derivative

$$
\dot{V}=
\nabla V^T\dot{x}
$$

For two states:

$$
\dot{V}
=
\frac{\partial V}{\partial x_1}\dot{x}_1
+
\frac{\partial V}{\partial x_2}\dot{x}_2
$$

---

## LTI Lyapunov equation

$$
A^TP+PA=-Q
$$

---

## Overshoot

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

---

## Damping ratio from overshoot

$$
\zeta=
\frac{-\ln(M_p)}
{\sqrt{\pi^2+\ln^2(M_p)}}
$$

---

## Settling time

$$
T_s=\frac{4}{\zeta\omega_n}
$$

---

## Second-order characteristic polynomial

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$


---

# 12. Taylor Series for Linearization

This section explains why linearization works and how Taylor series is used in control theory.

---

## 12.1 Main idea

In control theory, nonlinear systems can be hard to analyze directly.

A nonlinear system may contain terms such as:

$$
x^2,\quad x^3,\quad \sin(x),\quad x_1x_2
$$

Linearization replaces the nonlinear system by a linear approximation near a chosen point, usually an equilibrium point.

Taylor series is the mathematical reason why this is possible.

In simple words:

> Taylor series approximates a nonlinear function near a point using the value of the function and its derivatives at that point.

For control theory linearization, we usually keep only the first-order terms.

---

## 12.2 Taylor series for one variable

For a function:

$$
y=f(x)
$$

Taylor expansion around a point $x_0$ is:

$$
f(x)
=
f(x_0)
+
f'(x_0)(x-x_0)
+
\frac{f''(x_0)}{2!}(x-x_0)^2
+
\frac{f'''(x_0)}{3!}(x-x_0)^3
+
\dots
$$

For linearization, keep only:

$$
f(x)\approx f(x_0)+f'(x_0)(x-x_0)
$$

This is the first-order Taylor approximation.

The ignored terms are:

$$
(x-x_0)^2,\quad (x-x_0)^3,\quad \dots
$$

These are small close to $x_0$.

Example, if:

$$
x-x_0=0.1
$$

then:

$$
(x-x_0)^2=0.01
$$

and:

$$
(x-x_0)^3=0.001
$$

So higher-order terms become much smaller near the linearization point.

---

## 12.3 Simple scalar example

Let:

$$
f(x)=x^3
$$

Linearize around:

$$
x_0=1
$$

Calculate:

$$
f(1)=1
$$

Derivative:

$$
f'(x)=3x^2
$$

At $x_0=1$:

$$
f'(1)=3
$$

Use the first-order Taylor approximation:

$$
f(x)\approx f(1)+f'(1)(x-1)
$$

$$
f(x)\approx 1+3(x-1)
$$

$$
f(x)\approx 3x-2
$$

So near $x=1$:

$$
x^3\approx 3x-2
$$

This approximation is local. It is good near $x=1$, but not necessarily far away.

---

## 12.4 Taylor series for systems

In control theory, a nonlinear autonomous system is often written as:

$$
\dot{x}=f(x)
$$

where:

$$
x=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$

and:

$$
f(x)=
\begin{bmatrix}
f_1(x_1,x_2)\\
f_2(x_1,x_2)
\end{bmatrix}
$$

For a system, Taylor expansion around an equilibrium point $x_e$ is:

$$
f(x)\approx f(x_e)+J(x_e)(x-x_e)
$$

where $J(x_e)$ is the Jacobian matrix evaluated at $x_e$.

For two states:

$$
J(x)=
\begin{bmatrix}
\frac{\partial f_1}{\partial x_1} &
\frac{\partial f_1}{\partial x_2}\\
\frac{\partial f_2}{\partial x_1} &
\frac{\partial f_2}{\partial x_2}
\end{bmatrix}
$$

The Jacobian is the multi-variable version of the derivative.

---

## 12.5 Why equilibrium points simplify linearization

At an equilibrium point:

$$
f(x_e)=0
$$

because:

$$
\dot{x}=0
$$

Therefore:

$$
f(x)\approx f(x_e)+J(x_e)(x-x_e)
$$

becomes:

$$
f(x)\approx J(x_e)(x-x_e)
$$

Define the deviation variable:

$$
\Delta x=x-x_e
$$

Then the linearized system is:

$$
\Delta \dot{x}=A\Delta x
$$

where:

$$
A=J(x_e)
$$

If the equilibrium is the origin:

$$
x_e=0
$$

then:

$$
\Delta x=x
$$

and the linearized system can be written as:

$$
\dot{x}=Ax
$$

---

## 12.6 Example from the test

The nonlinear system is:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-x_1+x_1^3
$$

Write:

$$
f_1=x_2
$$

$$
f_2=-x_1+x_1^3
$$

The Jacobian is:

$$
J(x)=
\begin{bmatrix}
\frac{\partial f_1}{\partial x_1} &
\frac{\partial f_1}{\partial x_2}\\
\frac{\partial f_2}{\partial x_1} &
\frac{\partial f_2}{\partial x_2}
\end{bmatrix}
$$

Substitute $f_1$ and $f_2$:

$$
J(x)=
\begin{bmatrix}
\frac{\partial x_2}{\partial x_1} &
\frac{\partial x_2}{\partial x_2}\\
\frac{\partial(-x_1+x_1^3)}{\partial x_1} &
\frac{\partial(-x_1+x_1^3)}{\partial x_2}
\end{bmatrix}
$$

Calculate derivatives:

$$
\frac{\partial x_2}{\partial x_1}=0
$$

$$
\frac{\partial x_2}{\partial x_2}=1
$$

$$
\frac{\partial(-x_1+x_1^3)}{\partial x_1}
=
-1+3x_1^2
$$

$$
\frac{\partial(-x_1+x_1^3)}{\partial x_2}=0
$$

So:

$$
J(x)=
\begin{bmatrix}
0 & 1\\
-1+3x_1^2 & 0
\end{bmatrix}
$$

At the equilibrium point:

$$
x_e=(0,0)
$$

we have:

$$
x_1=0
$$

Therefore:

$$
-1+3x_1^2=-1+3\cdot 0^2=-1
$$

So:

$$
A=J(0,0)=
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}
$$

The linearized system is:

$$
\dot{x}=
\begin{bmatrix}
0 & 1\\
-1 & 0
\end{bmatrix}x
$$

or:

$$
\dot{x}_1=x_2
$$

$$
\dot{x}_2=-x_1
$$

---

## 12.7 Why did $x_1^3$ disappear?

The original equation was:

$$
\dot{x}_2=-x_1+x_1^3
$$

After linearization around zero:

$$
\dot{x}_2=-x_1
$$

The nonlinear term:

$$
x_1^3
$$

disappears because it is a higher-order term near zero.

For example, if:

$$
x_1=0.1
$$

then:

$$
x_1^3=0.001
$$

So close to zero, $x_1^3$ is much smaller than $x_1$.

Taylor linearization keeps only the first-order terms.

That is why:

$$
-x_1+x_1^3
$$

becomes approximately:

$$
-x_1
$$

near the origin.

---

## 12.8 Linearization with input

For a nonlinear system with input:

$$
\dot{x}=f(x,u)
$$

and output:

$$
y=g(x,u)
$$

linearize around an operating point:

$$
(x_e,u_e)
$$

Use deviation variables:

$$
\Delta x=x-x_e
$$

$$
\Delta u=u-u_e
$$

$$
\Delta y=y-y_e
$$

The linearized model is:

$$
\Delta \dot{x}=A\Delta x+B\Delta u
$$

$$
\Delta y=C\Delta x+D\Delta u
$$

where:

$$
A=
\left.
\frac{\partial f}{\partial x}
\right|_{x_e,u_e}
$$

$$
B=
\left.
\frac{\partial f}{\partial u}
\right|_{x_e,u_e}
$$

$$
C=
\left.
\frac{\partial g}{\partial x}
\right|_{x_e,u_e}
$$

$$
D=
\left.
\frac{\partial g}{\partial u}
\right|_{x_e,u_e}
$$

---

## 12.9 Special cases

### Equilibrium at the origin

If:

$$
x_e=0
$$

then:

$$
\Delta x=x
$$

So:

$$
\dot{x}=Ax
$$

---

### Equilibrium not at the origin

If:

$$
x_e\neq 0
$$

then use:

$$
\Delta x=x-x_e
$$

and write:

$$
\Delta \dot{x}=A\Delta x
$$

Do not write $\dot{x}=Ax$ unless you clearly shifted coordinates.

---

### Higher-order terms vanish around zero

Terms such as:

$$
x^2,\quad x^3,\quad x_1x_2
$$

usually vanish in first-order linearization around the origin.

---

### Nonlinear functions can become linear

Example:

$$
\sin(x)\approx x
$$

near zero, because:

$$
\sin(0)=0
$$

and:

$$
\cos(0)=1
$$

So:

$$
\sin(x)\approx 0+1(x-0)=x
$$

---

## 12.10 Things to pay attention to

- Taylor linearization is local, not global.
- Always linearize around a specific point.
- If no point is given, first find equilibrium points.
- Use the Jacobian for multi-variable systems.
- At equilibrium, $f(x_e)=0$.
- If the equilibrium is not the origin, use deviation variables.
- Higher-order terms are ignored in first-order linearization.
- Linearization gives local behavior only.
- If linearized eigenvalues are purely imaginary or zero, the indirect method is inconclusive.

---

## 12.11 Exam template

### Step 1: Write the nonlinear system

$$
\dot{x}=f(x)
$$

### Step 2: Find equilibrium

$$
f(x_e)=0
$$

### Step 3: Compute Jacobian

$$
J(x)=\frac{\partial f}{\partial x}
$$

### Step 4: Evaluate at equilibrium

$$
A=J(x_e)
$$

### Step 5: Write linearized system

If using deviation variables:

$$
\Delta \dot{x}=A\Delta x
$$

where:

$$
\Delta x=x-x_e
$$

If the equilibrium is the origin:

$$
\dot{x}=Ax
$$

### Step 6: Continue with stability analysis

Find eigenvalues:

$$
\det(\lambda I-A)=0
$$

Then apply indirect Lyapunov method.

---

## 12.12 Memory sentence

Taylor linearization means:

> Replace the nonlinear function by its best local straight-line approximation near the equilibrium.

For one variable:

$$
f(x)\approx f(x_0)+f'(x_0)(x-x_0)
$$

For systems:

$$
f(x)\approx f(x_e)+J(x_e)(x-x_e)
$$

At equilibrium:

$$
f(x_e)=0
$$

so:

$$
f(x)\approx J(x_e)(x-x_e)
$$

Therefore:

$$
\Delta \dot{x}=A\Delta x
$$

with:

$$
A=J(x_e)
$$
