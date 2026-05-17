#mathematic #controlTheory 
Before you look in to this note please be familiar with [[Similarity Transformation]].

## Main idea
if we have some state space system:
![[State-space equations#State-space representation#Definition]]
then we want to find a $P$ such that:
$$
A = P^{-1}DP
$$
- $D$ - diagonal matrix
- $P$ - transformation matrix
## Diagonalize a matrix by differential method
we want to find $P$ to transform other matrixes like $B$ or $C$.
$P$ will be:
$$
P = \begin{bmatrix}\omega_1 & \omega_2 & ... & \omega_i \end{bmatrix}
$$
and $\omega_i$ is a vector that full fill this:
$$
\begin{aligned}
	A\omega_i &= \lambda_i\omega_i
	\\
	c &= (\lambda_iI - A)\omega_i
\end{aligned}
$$
### Find eigenvalues
we want to find $\lambda_i$ as eigenvalues by:
$$
\begin{aligned}
	det(\lambda I - A) = 0
\end{aligned}
$$
if $A$ is:
$$
A = \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix}
$$
then
$$
\begin{aligned}
	det(\lambda I - A) &= det
		\left(
			\begin{bmatrix}
			\lambda & 0
			\\
			0 & \lambda
			\end{bmatrix}
			-
			\begin{bmatrix} 
				a_{11} & a_{12} 
				\\ 
				a_{21} & a_{22} 
			\end{bmatrix}
		\right)
		= det
		\left(
			\begin{bmatrix}
			\lambda - a_{11} & -a_{12}
			\\
			-a_{21} & \lambda - a_{22}
			\end{bmatrix}
		\right) 
		=
	\\
	&= (\lambda^2 - (a_{11} + a_{22}) \lambda + a_{11} a_{22}) - a_{12} a_{21} =
	\\
	&= \lambda^2 - (a_{11} + a_{22}) \lambda + a_{11} a_{22} - a_{12} a_{21}
\end{aligned}
$$
this quadratic equation to solve after it solved for $\lambda_1$ and $\lambda_2$ (if it can not be solve then Diagonalization in imposible with this method)
### Value of $\omega_i$
now we can find $\omega_1$ and $\omega_2$
$$
\begin{gathered}
	A\omega_1 = \lambda_1 \omega_1
	\\
	\begin{bmatrix}
		a_{11} & a_{12}
		\\
		a_{21} & a_{22}
	\end{bmatrix}
	\begin{bmatrix}
		x_{11}
		\\
		x_{21}
	\end{bmatrix}
	=
	\lambda_1
	\begin{bmatrix}
		x_{11}
		\\
		x_{21}
	\end{bmatrix}
	\\
	\begin{cases}
		a_{11} x_{11} + a_{12} x_{21} = \lambda_1 x_{11}
		\\
		a_{21} x_{11} + a_{22} x_{21} = \lambda_1 x_{21}
	\end{cases}
	\\
	\begin{cases}
		a_{12} x_{21} = \lambda_1 x_{11} - a_{11} x_{11}
		\\
		a_{21} x_{11} = \lambda_1 x_{21} - a_{22} x_{21}
	\end{cases}
	\\
	c_1 = \frac{\lambda_1 - a_{22}}{a_{21}}
\end{gathered}
$$
form this we get $x_{11} = c_1 x_{21}$ and $c_1$ is constant. we get $\omega_1$ as:
$$
	\omega_1 =
	\begin{bmatrix}
		1 
		\\
		c_1
	\end{bmatrix}
$$
we do the same thing for $\omega_2$
$$
\begin{gathered}
	A\omega_2 = \lambda_2 \omega_2
	\\
	\begin{bmatrix}
		a_{11} & a_{12}
		\\
		a_{21} & a_{22}
	\end{bmatrix}
	\begin{bmatrix}
		x_{12}
		\\
		x_{22}
	\end{bmatrix}
	=
	\lambda_2
	\begin{bmatrix}
		x_{12}
		\\
		x_{22}
	\end{bmatrix}
	\\
	\begin{cases}
		a_{11} x_{12} + a_{12} x_{22} = \lambda_2 x_{12}
		\\
		a_{21} x_{12} + a_{22} x_{22} = \lambda_2 x_{22}
	\end{cases}
	\\
	\begin{cases}
		a_{12} x_{22} = \lambda_2 x_{11} - a_{11} x_{12}
		\\
		a_{21} x_{12} = \lambda_2 x_{22} - a_{22} x_{22}
	\end{cases}
	\\
	c_2 = \frac{\lambda_2 - a_{22}}{a_{21}}
\end{gathered}
$$
form this we get $x_{12} = c_2 x_{22}$ and $c_2$ is constant. we get $\omega_2$ as:
$$
	\omega_2 =
	\begin{bmatrix}
		1 
		\\
		c_2
	\end{bmatrix}
$$
### P Matrix
we know that $P$:
$$
P = \begin{bmatrix} \omega_1 & \omega_2 \end{bmatrix}
= 
\begin{bmatrix} 
1 & 1
\\
c_1 & c_2
\end{bmatrix}
$$