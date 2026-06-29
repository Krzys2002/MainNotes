## 1. Linearization of Nonlinear Systems

### What problems belong here?

- Use the First Lyapunov Method
- Linearize around equilibrium
- Find Jacobian
- Determine local stability
- Analyze behavior around equilibrium

### What is linearization?

A nonlinear system:

$$
\dot{x}=f(x)
$$

is approximated near an equilibrium point by:

$$
\dot{x}=Ax
$$

where:

$$
A=\left.\frac{\partial f}{\partial x}\right|_{x=x_e}
$$

This matrix is called the Jacobian.

### Typical Procedure

1. Find equilibrium point.
2. Build Jacobian.
3. Evaluate Jacobian at equilibrium.
4. Calculate eigenvalues.
5. Interpret stability.

### Special Cases

Purely imaginary eigenvalues:

$$
\lambda=\pm j
$$

Conclusion:

$$
\boxed{\text{First Lyapunov Method is inconclusive}}
$$

### Things to Pay Attention To

- Always find equilibrium before evaluating Jacobian.
- Purely imaginary eigenvalues do not prove stability.

---

## 2. System Properties (Controllability and Observability)

### Main Rule

Controller design uses:

$$
(A,B)
$$

Need controllability.

Observer design uses:

$$
(A,C)
$$

Need observability.

### Controllability

$$
\mathcal C=
\begin{bmatrix}
B & AB
\end{bmatrix}
$$

Condition:

$$
rank(\mathcal C)=n
$$

### Observability

$$
\mathcal O=
\begin{bmatrix}
C\\
CA
\end{bmatrix}
$$

Condition:

$$
rank(\mathcal O)=n
$$

### Things to Pay Attention To

Observer → observability.

Controller → controllability.

---

## 3. Stability Using the Indirect Lyapunov Method

### Procedure

1. Find equilibrium.
2. Compute Jacobian.
3. Evaluate Jacobian.
4. Find eigenvalues.
5. Use stability table.

### Stability Table

- All negative real parts → asymptotically stable.
- At least one positive real part → unstable.
- Purely imaginary → inconclusive.
- Zero eigenvalue → inconclusive.

---

## 4. Stability Using the Direct Lyapunov Method

### Idea

Use:

$$
V(x)
$$

instead of linearization.

### Conditions

Positive definite:

$$
V(x)>0
$$

Derivative:

$$
\dot V
$$

### Procedure

1. Write Lyapunov function.
2. Check positivity.
3. Compute:

$$
\dot V=
\frac{\partial V}{\partial x_1}\dot x_1+
\frac{\partial V}{\partial x_2}\dot x_2
$$

4. Simplify.
5. Interpret.

### LaSalle

If:

$$
\dot V\le0
$$

find largest invariant set.

If only origin remains:

$$
\boxed{\text{Asymptotically stable}}
$$

---

## 5. State Feedback

### Goal

Design:

$$
u=-Kx
$$

### Theory

$$
A_{cl}=A-BK
$$

### Procedure

1. Define K.
2. Compute A-BK.
3. Find characteristic polynomial.
4. Build desired polynomial.
5. Compare coefficients.

---

## 6. Observer Design

### Observer Equation

$$
\dot{\hat x}
=
A\hat x
+
Bu
+
L(y-C\hat x)
$$

### Typical Procedure

1. Write controller poles.
2. Make observer poles 5–10 times faster.
3. Write observer poles.
4. Write observer equation.
5. State observer role.

### Memorize

The observer estimates the state vector based on measured outputs and known inputs.

---

# Ultimate Exam Checklist

- Nonlinear + Jacobian → Linearization
- Equilibrium → Set derivatives to zero
- Estimator poles → Observability
- Controller poles → Controllability + State Feedback
- Lyapunov Function Given → Direct Lyapunov Method
- Eigenvalues after Jacobian → Indirect Lyapunov Method
- Observer → Place poles faster than controller
