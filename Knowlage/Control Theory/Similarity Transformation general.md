#matematic #controlTheory
If we have state space equation:
$$
\begin{gathered}
	\dot{x} = Ax + Bu 
	\\
	y = Cx + Du
\end{gathered}
$$
And 
$$
\begin{aligned}
	z &= P^{-1}x
	\\
	x &= Pz
\end{aligned}
$$
Then we can transform to:
$$
\begin{aligned}
	\dot{z} &= (P^{-1}A)(Px) + (P^{-1}B)u 
	\\
	y &= C(Px) + Du
\end{aligned}
$$
now we can mark:
$$
\begin{aligned}
	\hat{A} &= (P^{-1}A)
	\\
	\hat{B} &= (P^{-1}B)
\end{aligned}
$$
then we gat final form:
$$
\begin{aligned}
	\dot{z} &= \hat{A}z + \hat{B}u 
	\\
	y &= Cz + Du
\end{aligned}
$$
