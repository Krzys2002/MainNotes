## Task 1

For arbitrary estimator pole placement, the pair $(A,C)$ must be
observable.

$$
A=\begin{bmatrix}5&2\\1&4\end{bmatrix},\quad
C=\begin{bmatrix}f&1\end{bmatrix}
$$

$$
\mathcal O=\begin{bmatrix}C\\CA\end{bmatrix}
=
\begin{bmatrix}
f & 1\\
5f+1 & 2f+4
\end{bmatrix}
$$

$$
\det(\mathcal O)=f(2f+4)-(5f+1)=2f^2-f-1=(2f+1)(f-1)
$$

Observable iff:

$$
(2f+1)(f-1)\neq 0
$$

Answer:

$$
e\in\mathbb R,\qquad f\neq -\frac12,\;f\neq 1
$$

## Task 2

Equilibria satisfy:

$$
x_2(1-x_2^2)=0,\qquad x_1=0
$$

Therefore:

$$
(0,0),\;(0,1),\;(0,-1)
$$

## Task 3

Jacobian:

$$
A=\begin{bmatrix}
0&1\\
-1+3x_1^2&0
\end{bmatrix}
$$

At $(0,0)$:

$$
A=\begin{bmatrix}
0&1\\
-1&0
\end{bmatrix}
$$

Characteristic equation:

$$
\lambda^2+1=0
$$

$$
\lambda_{1,2}=\pm j
$$

Conclusion: First Lyapunov method is inconclusive (purely imaginary
eigenvalues).

## Task 4

Lyapunov function:

$$
V=a\frac{x_1^4}{4}+\frac{x_2^2}{2}
$$

$$
\dot V=ax_1^3x_2+x_2(-ax_1^3-bx_2)
=-bx_2^2\le 0
$$

Using LaSalle's invariance principle, the only invariant set is the
origin.

Answer:

$$
\boxed{\text{Globally asymptotically stable}}
$$

## Task 5

$$
A=\begin{bmatrix}1&2\\0&3\end{bmatrix},
\quad
B=\begin{bmatrix}0\\1\end{bmatrix}
$$

Desired polynomial:

$$
(s+1)(s+2)=s^2+3s+2
$$

Let:

$$
K=\begin{bmatrix}k_1&k_2\end{bmatrix}
$$

Matching coefficients gives:

$$
k_1=3,\qquad k_2=7
$$

Answer:

$$
K=\begin{bmatrix}3&7\end{bmatrix}
$$

## Task 6

Controller poles:

$$
-5+j,\quad -5-j,\quad -1
$$

Observer 10 times faster:

$$
-50+10j,\quad -50-10j,\quad -10
$$

Observer role:

> It estimates the state vector based on measured outputs and known
> inputs.

## Task 7

Overshoot:

$$
M_p=20\%
$$

Settling time:

$$
T_s=2s
$$

From:

$$
M_p=e^{-\frac{\zeta\pi}{\sqrt{1-\zeta^2}}}
$$

obtain:

$$
\zeta\approx0.456
$$

Using:

$$
T_s=\frac{4}{\zeta\omega_n}
$$

gives:

$$
\omega_n\approx4.386
$$

Desired polynomial:

$$
s^2+2\zeta\omega_n s+\omega_n^2
$$

$$
\boxed{s^2+4s+19.24}
$$

## Task 8

$$
A=\begin{bmatrix}
-4&1\\
4&-5
\end{bmatrix}
$$

Characteristic polynomial:

$$
\lambda^2+9\lambda+16=0
$$

Eigenvalues:

$$
\lambda_{1,2}
=\frac{-9\pm\sqrt{17}}{2}
$$

Both eigenvalues are negative.

Answer:

$$
\boxed{\text{Asymptotically stable}}
$$

Lyapunov procedure:

1.  Choose $Q>0$.
2.  Solve:

$$
A^TP+PA=-Q
$$

3.  Verify $P>0$.
4.  Define:

$$
V=x^TPx
$$

5.  If:

$$
\dot V=-x^TQx<0
$$

then the system is asymptotically stable.
