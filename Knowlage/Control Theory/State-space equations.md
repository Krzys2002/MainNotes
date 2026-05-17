#matematic #controlTheory 
This note will introduce State Space equation and basic concepts connected to them.
## State-space representation
$$
\begin{cases}
\dot{\underline{x}} = \underline{f}(\underline{x}, \underline{u}, t) \quad \rightarrow \quad \text{state equation} \\
\underline{y} = \underline{h}(\underline{x}, \underline{u}, t) \quad \rightarrow \quad \text{output equation}
\end{cases}
$$
- $\underline{x}$ - state vector, $\underline{u}$ – control (input) vector, $\underline{y}$ – output (measurement) vector;
- $\underline{f}(\underline{x}, \underline{u}, t),\space \underline{h}(\underline{x}, \underline{u}, t)$ – set of transition and measurement functions, respectively;

### Equation for the linear plant
#### Definition
$$
\begin{cases}
\dot{\underline{x}} = A\underline{x} + B\underline{u} \\
\underline{y} = C\underline{x} + D\underline{u}
\end{cases}
$$
#### Expalnation
- $A$ - process matrix $\rightarrow$ system dynamics,
- $B$ - input matrix $\rightarrow$ impact of inputs on the system,
- $C$ - output matrix $\rightarrow$ transformation of state variables in to outputs,
- $D$ - transmission matrix $\rightarrow$ transferring the input directly to the output.
#### Diagram

![[State-space equations 2026-05-14 14.41.32.excalidraw|1200]]
## How to interpret a plant to State-space representation
To do this we need equation of the system form Newton's law or Kirchhoff's laws. Equation have to have the highest derivative on one side and the rest to the other side.
$$
\ddot{x} = a\dot{x} - bx + cu
$$
Then you point out what you liking for. Her we looking for position $x$.
Then we asine for $x_n$ derivative of variable.
$$
\begin{cases}
x_1 = x \\
x_2 = \dot{x} = \dot{x}_1
\end{cases}
$$
After that we are ready to create state space representation.
$$
\begin{cases}
\begin{bmatrix}
\dot{x}_1 \\
\dot{x}_2
\end{bmatrix}
=
\begin{bmatrix}
0 & 1 \\
-b & a
\end{bmatrix}
\begin{bmatrix}
x_1 \\
x_2
\end{bmatrix}
+
\begin{bmatrix}
0 \\
c
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
+
0 * u
\end{cases}
$$
$$
A = 
\begin{bmatrix}
0 & 1 \\
-b & a
\end{bmatrix}, \quad
B = 
\begin{bmatrix}
0 \\
c
\end{bmatrix}, \quad
C = 
\begin{bmatrix}
1 & 0
\end{bmatrix}, \quad
D = 0
$$
### Converting space state equation to diagram 

![[State-space equations 2026-05-14 18.01.48.excalidraw|1200]]
Full universal explanation in the note [[State-space to diagram]]
## System Examples
1. Mechanical
	- [[State-space mechanical position example|position]]
	- velocities
2. Electrical circuit
	- capacitor charge
	- capacitor voltage
	- currents in the circuit
3. Electro-mechnical system (DC motor) - 2DoF
	- general rules of the state variables selection
	- state variable possible in the different forms
4. Discrete system
	- modeling discrete form directly

