#mathematic #controlTheory 
Before you look in to this note please be familiar with [[Similarity Transformation]].

## Main idea
if we have some state space system:
![[State-space equations#State-space representation#Definition]]
then we want to find a $P$ such that:
$$
A = PDP^{-1}
$$
- $D$ - diagonal matrix
- $P$ - transformation matrix

The diagonal matrix is obtained from:
$$
D=P^{-1}AP
$$
## Diagonalize a matrix by differential method
We want to find eigenvalues $\lambda_i$ and eigenvectors $\omega_i$, where:
$$
\begin{aligned}
	A\omega_i &= \lambda_i\omega_i
	\\
	c &= (\lambda_iI - A)\omega_i
\end{aligned}
$$
Equivalently:
$$
(\lambda_i I-A)\omega_i=0
$$
or:
$$
(A-\lambda_i I)\omega_i=0
$$

### Find eigenvalues
Eigenvalues are found from:
$$
\det(\lambda I-A)=0
$$
For
$$
A = \begin{bmatrix} a_{11} & a_{12} \\ a_{21} & a_{22} \end{bmatrix}
$$
we get:
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
Solve:
$$
\det(\lambda I-A)=0
$$
to obtain $\lambda_1,\lambda_2$.
### Find eigenvectors
For each eigenvalue $\lambda_i$, solve:
$$
A\omega_i=\lambda_i\omega_i
$$
Let:
$$
\omega_i=
\begin{bmatrix}
x_1\\
x_2
\end{bmatrix}
$$
Then:
$$
a_{21}x_1+a_{22}x_2=\lambda_i x_2
$$
so:
$$
a_{21}x_1=(\lambda_i-a_{22})x_2
$$
$$
x_1=\frac{\lambda_i-a_{22}}{a_{21}}x_2
$$
Define:
$$
c_i=\frac{\lambda_i-a_{22}}{a_{21}}
$$
If we choose $x_2=1$, then:
$$
\omega_i=
\begin{bmatrix}
	c_i\\
	1
\end{bmatrix}
$$
### P Matrix
The matrix $P$ is built from eigenvectors:
$$
P=
\begin{bmatrix}
	\omega_1 & \omega_2
\end{bmatrix}
$$
so:
$$
P=
\begin{bmatrix}
	c_1 & c_2
	\\
	1 & 1
\end{bmatrix}
$$
Then:
$$
D=P^{-1}AP
$$
and:
$$
A=PDP^{-1}
$$