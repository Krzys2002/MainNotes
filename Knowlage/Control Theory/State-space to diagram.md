This note will explain all about converting state space to diagram.

## Universal formula for conversion 
If state space equation for $x_1, x_2, \space ...,\space x_n$ and input $U = \begin{bmatrix} u_1 & u_2 & ... & u_m \end{bmatrix}$ and output $Y = \begin{bmatrix} y_1 & y_2 & ... & y_k \end{bmatrix}^T$:
$$
\begin{cases}
\begin{bmatrix}
\dot{x}_1 \\
\dot{x}_2 \\
... \\
\dot{x}_n
\end{bmatrix}
=
\begin{bmatrix}
a_{11} & a_{12} & ... & a_{1n} \\
a_{21} & a_{22} & ... & a_{2n} \\
... & ... & ... & ...\\
a_{n1} & a_{n2} & ... & a_{nn}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
... \\
x_n
\end{bmatrix}
+
\begin{bmatrix}
b_{11} & b_{12} & ... & b_{1m} \\
b_{21} & b_{22} & ... & b_{2m} \\
... & ... & ... & ... \\
b_{n1} & b_{n2} & ... & b_{nm}
\end{bmatrix}
U \\
Y = 
\begin{bmatrix}
c_{11} & c_{12} & ... & c_{1n} \\
c_{21} & c_{22} & ... & c_{2n} \\
... & ... & ... & ... \\
c_{k1} & c_{k2} & ... & c_{kn}
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2 \\
... \\
x_n
\end{bmatrix}
+
\begin{bmatrix}
d_{11} & d_{12} & ... & d_{1m} \\
d_{21} & d_{22} & ... & d_{2m} \\
... & ... & ... & ... \\
d_{k1} &d_{k2} & ... & d_{km}
\end{bmatrix}
* U
\end{cases}
$$
![[State-space to diagram 2026-05-16 12.12.52.excalidraw|1200]]
This scheme looks complicated but is very simple in essence. to understand it we need to point out two separate key points of state space equations.

### Connection of the matrixes in State-space
#### First property
Matrixes $A, B, C, D$ connect with weights $X, Y, U$. if we know with matrix connect X with Y and U with X and so on. We will expect for any $y_k$ to we equal to some sum of multiplication of coefficients in one matrix by vector X and another matrix coefficients by vector U to get vector Y. Form ![[State-space equations#State-space representation#Equation for the linear plant]] 
we know this dependence:
$$
\begin{cases}
U*D + X*C = Y \\
U*B + X*A = \dot{X}
\end{cases}
$$
from this we know some $u_{r}$ for $0<r\leq m$ is $u_r * d$ go to sum of different $u *d$ this go to sum with sum of c give y. we can se this on the diagram:
![[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^area=GnuP8KplvpAOhKcWhaWPL]]
and this go to:
![[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^area=KPODOVjH]]
we can see gain(multiplication of u by d) and it sum all u by d and it go to sum with c and this create $y_1$.

You can study the diagram and see this with other matrixes.

##### Summary
In the diagram:
1. All property of $D$: ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^GnuP8KplvpAOhKcWhaWPL|see on the diagram]])(you can skip 0 or 1 gains) 
	- all of the $u$ have to go to gain $d$. ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^fYO6M22m_RziMY-U2gKUz|see on the diagram]]).
	- the number of gains $d$ connected to one $u$ in equal to $k$ (number of outputs $y$).
	- the first sum of gains $d$ have amount of inputs from gains equal to $m$ 
	  (number of inputs $u$)
	- the number of first sums is equal to $k$. (number of outputs $y$).
	
2. All property of $B$: ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^xqXK_Os004I6Xp7f8SsLK|see on the diagram]])(you can skip 0 or 1 gains) 
	- all of the $u$ have to be connected to gain $b$. ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^gISg9Sd6|see on the diagram]])
	- the number of gains $b$ connected to one $u$ in equal to $n$ (number of $x$).
	- the first sum of gains $b$ have amount of inputs form gains equal to $m$ 
	  (number of inputs $u$).
	- the number of first sums is equal to $n$. (number of $x$).
	
3. All property of A: ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^MHYUwpTT|see on the diagram]])(you can skip 0 or 1 gains) 
	- all of $x$ have to be connected to gain $a$.
	-  the number of gains $a$ connected to one $x$ in equal to $n$ (number of $x$).
	- the first sum of gains $a$ have amount of inputs form gains equal to $n$ 
	  (number of $x$).
	-  the number of first sums is equal to $n$. (number of $x$).
	
4. All property of $C$: ([[Excalidraw/State-space to diagram 2026-05-16 12.12.52.excalidraw.md#^jlPiBkSO|see on the diagram]])(you can skip 0 or 1 gains)
	- all of $x$ have to be connected to gain $c$.
	- the number of gains $c$ connected to one $x$ in equal to $k$ (number of outputs $y$).
	- the first sum of gains $c$ have amount of inputs form gains equal to $n$ 
	  (number of $x$).
	-   the number of first sums is equal to $k$. (number of outputs $y$).

#### Second property

For $l_{gh}$ for $l$ is $a$ or $b$ or $c$ or $d$ then $h$ tells of number place in the of end vector of transformation and $g$ of the input number of transformation.

ex:
- $a_{13} \Rightarrow \underline{x_3 * a_{13}} + x_1 * a_{11} + ... + x_n * a_{1n} + b_1 = \underline{\dot{x}_1}$
	3 - input $x_3$,
	1 - output to sum to sum for $\dot{x}_1$
- $d_{3m} \Rightarrow \underline{u_m * d_{3m}} + ... + u_1 * d_{31} + c_1 = \underline{y_3}$
- m - input $u_m$,
- 3 - output to sum to sum for $y_3$