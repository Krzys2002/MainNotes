#controlTheory #mathematic 
This note will solve example of state space modeling of mechanical system. to solve we have Mass-spring-damping system

## System introduction
![[State-space mechanical position example 2026-05-14 18.29.38.excalidraw|1200]]
- input - u (force)
- output - y (position)

### Create equation of the system
To do this we will use second Newton's law:
$$
m\ddot{y}+b\dot{y}+ky=u
$$
form this we get:
$$
\ddot{y} = \frac{-b}{m}\dot{y} + \frac{-k}{m}y + \frac{u}{m}
$$
and this our equation of this system

## Converting System Equation to State-space
Form system equation:
$$
\ddot{y} = \frac{-b}{m}\dot{y} + \frac{-k}{m}y + \frac{u}{m}
$$
first we need our $x_n$ for the state space
$$
\begin{cases}
x_1 = y \\
x_2 = \dot{y} = \dot{x}_1
\end{cases}
$$
system equation using new notation
$$
\dot{x}_2 = \frac{-b}{m}x_2 + \frac{-k}{m}x_1 + u
$$
we can get matrix A first row form $\dot{x}_1=x_2$ and second row for system equation:
$$
A = 
\begin{bmatrix}
0(0 * x_1) & 1(1 * x_2) \\
\frac{-k}{m}(*x_1) & \frac{-b}{m}(*x_2)
\end{bmatrix}
$$
now we know that $u$ in a component of only $\dot{x}_2$ form system equation:
$$
B =
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
$$
for C we know that output is position than position is x than $y = x = x_1$
$$
C =
\begin{bmatrix}
1 & 0
\end{bmatrix}
$$
and output is now directly influence by u, then D is:
$$
D = 0
$$
### Final State-space equations
$$
\begin{cases}
\begin{bmatrix}
\dot{x}_1 \\
\dot{x}_2
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
\frac{-k}{m} & \frac{-b}{m}
\end{bmatrix}

\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
+
\begin{bmatrix}
0 \\
\frac{1}{m}
\end{bmatrix}
u \\

y = 
\begin{bmatrix}
1 & 0
\end{bmatrix}

\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
\end{cases}
$$
## Diagram form State space equation
![[State-space mechanical position example 2026-05-14 19.10.22.excalidraw|1200]]