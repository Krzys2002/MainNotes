## Task 1
Diagonalize the matrix $A$:
$$
A = 
\begin{bmatrix}
4 & 1
\\
2 & 3
\end{bmatrix}
$$
Provide the transformation matrix $P$ such that $A= PDP^{-1}$, where $D$ is a diagonal matrix. (2 points)
### Solution
Calculate eigenvalues by
![[Diagonalization#Find eigenvalues]]
$$
\begin{aligned}
	0 &= det 
	\left(
		\begin{bmatrix}
			\lambda - 4 & -1
			\\
			-2 & \lambda -3
		\end{bmatrix}
	\right)
	=
	\lambda^2 - 7\lambda + 12 - 2
	\\
	&= \lambda^2 -7\lambda + 10
	\\
	\\
	\Delta &= 49 - 4 \cdot 10 = 9 \Rightarrow \sqrt{\Delta}= 3
	\\
	\\
	&\lambda_1 = 2 \quad \lambda_2 = 5
\end{aligned} 
$$
now we can calculate $\omega_1$ and $\omega_2$ form this:
![[Diagonalization#Find eigenvectors]]
for my values:
$$
\begin{aligned}
	c_1 = \frac{2 - 3}{2} = -\frac{1}{2}
	\\
	c_2 = \frac{5 - 3}{2} = 1
\end{aligned}
$$
with we get $\omega_1^T = \begin{bmatrix} -1 & 2 \end{bmatrix}$ and $\omega_2^T = \begin{bmatrix} 1 & 1 \end{bmatrix}$.
then $P$ is
$$
P = 
\begin{bmatrix}
	\omega_1 & \omega_2
\end{bmatrix}
=
\begin{bmatrix}
	-1 & 1
	\\
	2 & 1
\end{bmatrix}
$$
and 
$$
P^{-1} = 
\frac{1}{det(P)}
\begin{bmatrix}
	1 & -1
	\\
	-2 & -1
\end{bmatrix}
=
\frac{1}{3}
\begin{bmatrix}
	-1 & 1
	\\
	2 & 1
\end{bmatrix}
$$
now we calculate $D$
#### Answer
$$
\begin{aligned}
	D &= P^{-1}AP = \frac{1}{3}
		\begin{bmatrix}
			-1 & 1
			\\
			2 & 1
		\end{bmatrix}
		\begin{bmatrix}
			4 & 1
			\\
			2 & 3
		\end{bmatrix}
		\begin{bmatrix}
			-1 & 1
			\\
			2 & 1
		\end{bmatrix}
		=
		\\
		&= 
		\begin{bmatrix}
			2 & 0 
			\\
			0 & 5
		\end{bmatrix}
\end{aligned}
$$
$D$ is now Diagonalize $A$
## Task 2
 Find the state-space representation of the block diagram given in the Fig. 1 (1 point)
 ![[Pasted image 20260514192432.png]]
### Solution
#### Answer
$$
\begin{cases}
	\dot{\underline{x}} =
	\begin{bmatrix}
		0 & 1 & 0 \\
		0 & 0 & 1 \\
		-24 & -26 & -9
	\end{bmatrix}
	\underline{x} + 
	\begin{bmatrix}
		0 \\
		0 \\
		24
	\end{bmatrix} r \\
	y = 
	\begin{bmatrix}
		1 & 0 & 0
	\end{bmatrix} \underline{x}
\end{cases}
$$
## Task 3
Find the state-space representation of the given transfer function. (2 points)
$$
G(s)= \frac{10}{(s + 1)(s + 2)(s + 3)}
$$
### Solution 1

$$
\begin{aligned}
	G(s) &= \frac{10}{(s + 1)(s + 2)(s + 3)} \\
	 &= \frac{10}{s^3 + (1+2+3)s^2 + (2+3+6)s + 6} \\
	 &= \frac{10}{s^3 + 6s^2 + 11s + 6}
\end{aligned}
$$
form $G(s)=\frac{Y(S)}{U(S)}$ we get:
$$
\begin{aligned}
	(s^3 + 6s^2 + 11s + 6)Y(s) &= 10U(s) \\
	(s^3 + 6s^2 + 11s + 6)10X(s) &= 10U(s) \\
	
\end{aligned}
$$
we get:
$$
\begin{cases}
	(s^3 + 6s^2 + 11s + 6)X(s) = U(s) \\
	Y(s) = 10X(s)
\end{cases}
$$
now we convert it to system equations
$$
\begin{cases}
	x^{(3)} + 6\ddot{x} + 11\dot{x} + 6x = u \\
	y = 10x
\end{cases}
$$
form with we get:
$$
x^{(3)} = -6\ddot{x} - 11 \dot{x} - 6x + u
$$
now we create $x_n$ for state space
$$
\begin{cases}
x_1 = x \\
x_2 = \dot{x} = \dot{x}_1 \\
x_3 = \ddot{x} = \dot{x}_2 = \ddot{x}_1
\end{cases}
$$
after substitutions:
$$
\begin{cases}
	\dot{x}_3 = -6x_3 - 11x_2 - 6x_1 + u \\
	y=10x_1
\end{cases}
$$
now we can create state space representation
#### Answer
$$
\begin{cases}
	\dot{\underline{x}} =
	\begin{bmatrix}
		0 & 1 & 0 \\
		0 & 0 & 1 \\
		-6 & -11 & -6
	\end{bmatrix}
	\underline{x} + 
	\begin{bmatrix}
		0 \\
		0 \\
		1
	\end{bmatrix} u \\
	y = 
	\begin{bmatrix}
		10 & 0 & 0
	\end{bmatrix} \underline{x}
\end{cases}
$$

### Solution 2
$$
\begin{aligned}
	G(s) &= \frac{10}{(s + 1)(s + 2)(s + 3)} \\
	 &= \frac{10}{s^3 + (1+2+3)s^2 + (2+3+6)s + 6} \\
	 &= \frac{10}{s^3 + 6s^2 + 11s + 6} = G_1(s)*G_2(2)s \\\\
	G_1(s) &= \frac{1}{s^3 + 6s^2 + 11s + 6} = \frac{X(s)}{U(s)}\\ 
	G_2(s) &= 10 = \frac{Y(s)}{X(s)} \\
	U(s) &= X(s)*(s^3 + 6s^2 + 11s + 6) \\
	Y(s) &= 10X(s)
\end{aligned}
$$
using inverse Laplace:
$$
\begin{aligned}
	u(t) &= x^{(3)} + 6\ddot{x} + 11\dot{x} + 6x \\
	y(t) &= 10x
\end{aligned}
$$
now we create $x_n$ for state space:
$$
\begin{cases}
x_1 = x \\
x_2 = \dot{x} = \dot{x}_1 \\
x_3 = \ddot{x} = \dot{x}_2 = \ddot{x}_1
\end{cases}
$$
after substitutions:
$$
\begin{cases}
	\dot{x}_3 = -6x_3 - 11x_2 - 6x_1 + u \\
	y=10x_1
\end{cases}
$$
now we can create state space representation
#### Answer
$$
\begin{cases}
	\dot{\underline{x}} =
	\begin{bmatrix}
		0 & 1 & 0 \\
		0 & 0 & 1 \\
		-6 & -11 & -6
	\end{bmatrix}
	\underline{x} + 
	\begin{bmatrix}
		0 \\
		0 \\
		1
	\end{bmatrix} u \\
	y = 
	\begin{bmatrix}
		10 & 0 & 0
	\end{bmatrix} \underline{x}
\end{cases}
$$
## Task 4
Find the transfer function representation of a given state-space system. (2 points)
$$
\begin{cases}
	\dot{\underline{x}} &= 
	\begin{bmatrix}
		0 & 1 \\
		-1 & -2
	\end{bmatrix}
	\underline{x} + 
	\begin{bmatrix}
		0 \\ 1
	\end{bmatrix}
	u \\

	y &= 
	\begin{bmatrix}
		1 & 0
	\end{bmatrix}
	\underline{x}
\end{cases}
$$

### Solution 1
we go to system equation:
$$
\begin{cases}
	\dot{x}_2 &= -2x_2 -x_1 + u \\
	\dot{x}_1 &= x_2 \\
	y &= x_1  \\
	x &= x_1
\end{cases}
$$

we return to $x$
$$
\begin{cases}
	\ddot{x} &= -2\dot{x} -x + u \\
	y &= x  
\end{cases}
$$
we try to find $G(s) = \frac{Y(s)}{U(s)}$ then we sort the equation:
$$
\begin{cases}
	u &= \ddot{x} + 2\dot{x} + x \\
	y &= x  
\end{cases}
$$
now we use inverse Laplace
$$
\begin{aligned}
	\begin{cases}
		U(s) &= X(s)(s^2 + 2s + 1) \\
		Y(s) &= X(S)  
	\end{cases}&
	\Rightarrow &
	U(s) &= Y(s)(s^2 + 2s + 1) \\
	&&\frac{Y(s)}{U(s)} &= \frac{1}{s^2 + 2s + 1} = G(s)
\end{aligned}
$$
And we have our $G(S)$
#### Answer
$$
G(s) = \frac{1}{s^2 + 2s + 1}
$$

### Solution 2
$$
\begin{cases}
	\dot{\underline{x}} &= 
	\begin{bmatrix}
		0 & 1 \\
		-1 & -2
	\end{bmatrix}
	\underline{x} + 
	\begin{bmatrix}
		0 \\ 1
	\end{bmatrix}
	u \\

	y &= 
	\begin{bmatrix}
		1 & 0
	\end{bmatrix}
	\underline{x}
\end{cases}
$$
$$
\begin{aligned}
	A &= 
	\begin{bmatrix}
		0 & 1 \\
		-1 & -2
	\end{bmatrix}
	\\
	B &= 
	\begin{bmatrix}
		0 \\ 1 
	\end{bmatrix}
	\\
	C &=
	\begin{bmatrix}
		1 & 0
	\end{bmatrix}
	\\
	D &= 0
\end{aligned}
$$
formula for $G(s)$
$$
G(s) = C(sI - A)^{-1}B + D
$$
first we calculate
$$
\begin{aligned}
	(sI - A)^{-1} &= 
		\left(\begin{bmatrix}s & 0 \\ 0 & s\end{bmatrix}
			- \begin{bmatrix} 0 & 1 \\ -1 & -2\end{bmatrix}
		\right)^{-1} 
		=
			\left(\begin{bmatrix}s & -1 \\
			 1 & s + 2\end{bmatrix}
			\right)^{-1} 
	\\ \\
	&= \frac{1}{det\left(\begin{bmatrix}
					s & -1 \\
					1 & s + 2 
				\end{bmatrix}
			\right)}
		\cdot \begin{bmatrix}
				s + 2 & 1 \\
				-1 & s
			 \end{bmatrix}
	 \\ \\
	&= \frac{1}{(s^2 + 2s +1)}
		\begin{bmatrix}
			s + 2 & 1 \\
			-1 & s
		 \end{bmatrix}
\end{aligned}
$$
then we calculate rest
$$
\begin{aligned}
	G(s) &= \frac{1}{s^2 + 2s + 1}
			\begin{bmatrix}
				1 & 0
			\end{bmatrix}
			\begin{bmatrix}
				s + 2 & 1 \\
				-1 & s
			 \end{bmatrix}
			 \begin{bmatrix}
				 0 \\ 1
			 \end{bmatrix} 
		 \\
		 &= \frac{1}{s^2 + 2s + 1}
			\begin{bmatrix}
				s + 2 & 1
			\end{bmatrix}
			\begin{bmatrix}
				 0 \\ 1
			\end{bmatrix} \\
		 &= \frac{1}{s^2 + 2s + 1}
\end{aligned}
$$
and we have solution:
#### Answer
$$
G(s) = \frac{1}{s^2 + 2s + 1}
$$

## Task 5
Consider the following DC motor model:
$$
\begin{gathered}
	\dot{x} = 
			\begin{bmatrix}
				-1 & 1 \\
				-1 & -\frac{1}{10}
			\end{bmatrix}x
			+
			\begin{bmatrix}
				0 \\
				10
			\end{bmatrix}u
	 \\
	 y = \begin{bmatrix} 1 & 0 \end{bmatrix}x
	
\end{gathered}
$$
Find another system realization (only A matrix). Based on the following state transformation (2 points):
$$
\bar{x}_1 = x_1, \quad \bar{x}_2 = -x_1 + x_2
$$
### Solution
First we write equation for $\dot{x}_1$ and $\dot{x}_2$:
$$
\begin{gathered}
	\dot{x}_1 = -x_1 + x_2 \\
	\dot{x}_2 = -x_1 - \frac{1}{10} x_2 + 10u
\end{gathered}
$$
then we see that:
$$
\dot{x}_1 = -x_1 + x_2 = \bar{x}_2
$$
then we see similarity $\dot{x}_2$ to $\bar{x}_2$:
$$
\begin{aligned}
	x_2 &= \bar{x}_2 + x_1 \\
	\dot{\bar{x}}_2 &= -x_1 - \frac{1}{10}(\bar{x}_2 + x_1) + 10u \\
	\dot{\bar{x}}_2 &= -\frac{11}{10}x_1 - \frac{1}{10}\bar{x}_2 + 10u \\
	\dot{\bar{x}}_2 &= -\frac{11}{10}\bar{x}_1 - \frac{1}{10}\bar{x}_2 + 10u
\end{aligned}
$$
then we get A:
#### Answer
$$
A = 
	\begin{bmatrix}
	0 & 1 \\
	-\frac{11}{10} & - \frac{1}{10}
	\end{bmatrix}
$$
## Task 6
Find differential equations that describe the system in the Fig. 2 (2 points)
![[Pasted image 20260516184525.png]]

### Solution
Equation from second Newton's law:
#### Answer
$$
\begin{aligned}
	&\begin{cases}
		m_1 \ddot{x}_1 &= u - k_1 x_1 + k_2(x_2 - x_1) + b(\dot{x}_2 - \dot{x}_1) \\
		m_2 \ddot{x}_2 &= -k_2(x_2 - x_1) - k_3 x_2 - b(\dot{x}_2 - \dot{x}_1)
	\end{cases}
	\\
	&\begin{cases}
		\ddot{x}_1 &= \frac{u}{m_1} -\frac{k_1}{m_1} x_1 + \frac{k_2}{m_1}(x_2 - x_1) - \frac{b}{m_1}(\dot{x}_2 - \dot{x}_1)
		\\
		\ddot{x}_2 &= - \frac{k_2}{m_2}(x_2 - x_1) - \frac{k_3}{m_2} x_2 + \frac{b}{m_2}(\dot{x}_2 - \dot{x}_1)
	\end{cases}
\end{aligned}
$$
## Task 7
Find differential equations that describe the system in the Fig. 3 (2 points)
![[Pasted image 20260516190442.png]]
Form Kirchhoff's laws:
$$
\begin{gathered}
	i_1 = C_1\dot{U}_{C1} \\
	i_2 = C_2\dot{U}_{c2} \\
	\begin{cases}
		C_1\dot{U}_{C1} &= \frac{e_i - U_{C1}}{R_1} - \frac{U_{C1} - U_{C2}}{R_2}
		\\
		C_2\dot{U}_{c2} &= \frac{U_{C1} - U_{C2}}{R_2}
	\end{cases}
\end{gathered}
$$
now we create $x_1 = U_{C1}$ and $x_2 = U_{C2}$ and substitute:
#### Answer
$$
\begin{aligned}
	&\begin{cases}
		C_1\dot{x}_1 = \frac{e_i - x_1}{R_1} - \frac{x_1 - x_2}{R_2} \\
		C_2\dot{x}_2 = \frac{x_1 - x_2}{R_2}
	\end{cases}
	\\
	\\
	&\begin{cases}
	\dot{x}_1 = -\frac{R_1 + R_2}{R_1 R_2 C_1}x_1 + \frac{1}{R_2 C_1}x_2 + \frac{1}{R_1 C_1}e_i
	\\
	\dot{x}_2 = \frac{1}{R_2 C_2}x_1 - \frac{1}{R_2 C_2}x_2
	\end{cases}
\end{aligned}
$$
## Task 8
Derive the state-space representation of the DC motor system shown below. The motor converts electrical energy into rotational mechanical energy. The input is the voltage $V$ applied to the motor’s armature, and the output is the angular velocity $\dot{\theta}$. (2 points)
![[Pasted image 20260517163226.png]]
### Solution 
System equations:
$$
\begin{aligned}
	0 &= V - K \dot{\theta} - L\frac{di}{dt} - Ri
	\\
	J \ddot{\theta} &= Ki - b \dot{\theta}
\end{aligned}
$$
so:
$$
\begin{aligned}
	L\frac{di}{dt} &= V - K \dot{\theta} - Ri
	\\
	J \ddot{\theta} &= Ki - b \dot{\theta}
\end{aligned}
$$
then:
$$
\begin{aligned}
	x_1 &= i
	\\
	x_2 &= \dot{\theta}
\end{aligned}
$$
after substitution:
$$
\begin{aligned}
	L \dot{x}_1 &= V - K x_2 - R x_1
	\\
	J \dot{x}_2 &= K x_1 - b x_2
\end{aligned}
$$
so:
$$
\begin{aligned}
	\dot{x}_1 &= \frac{V}{L} - \frac{K}{L} x_2 - \frac{R}{L} x_1
	\\
	\dot{x}_2 &= \frac{K}{J} x_1 - \frac{b}{J} x_2
\end{aligned}
$$
State space representation of the system:
$$
\begin{aligned}
	\dot{x} &= 
		\begin{bmatrix}
			-\frac{R}{L} & -\frac{K}{L}
			\\
			\frac{K}{J} & - \frac{b}{J}
		\end{bmatrix}
		x + 
		\begin{bmatrix}
			\frac{1}{L} 
			\\
			0
		\end{bmatrix}
		u
	\\
	y &= \begin{bmatrix} 0 & 1 \end{bmatrix} x 
\end{aligned}
$$