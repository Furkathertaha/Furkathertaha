$$
\begin{cases} 
		a_{11}x_1&+&a_{12}x_2&+&\cdots&+a_{1n}x_n&=&b_1\\
		&&&&\vdots\\
		a_{n1}x_1&+&a_{n2}x_2&+&\cdots&+a_{nn}x_n&=&b_n&			
\end{cases}
$$

$$
\begin{eqnarray}f(x,y)
		&=&2xy+(x-y)^2\\
		&=&x^2+y^2
\end{eqnarray}
$$

# GAMES 103 Notes:

## 1. Energy of Spring System (Matrix equation with chain manipulation)

$$E = \frac{1}{2} ([\frac{\partial \phi}{\partial x}] [x])^\mathsf{T} [K] ([\frac{\partial \phi}{\partial x}] [x]) = \frac{1}{2} [x]^\mathsf{T} ( [\frac{\partial \phi}{\partial x}] ^\mathsf{T} [K] [\frac{\partial \phi}{\partial x}] ) [x]$$

Note that $E$ is the total energy, a scalar. $[K]$ and $[ \frac{\partial \phi}{\partial x} ]$ are 2d matrices, while $[\phi]$, $[x]$ and $[F]$ are vectors.

$$[F] = \frac{\partial E}{\partial x} = ( [\frac{\partial \phi}{\partial x}]^\mathsf{T} [K] [\frac{\partial \phi}{\partial x}] )[x] = [\frac{\partial \phi}{\partial x}]^\mathsf{T} [K] [\phi] $$

## 2. Constrained Dynamics (P7: 58 min)

$$ 
\left[
    \begin{array}{cc}
      M & -\Delta t J^\mathsf{T}  \\
      \Delta t J & C 
    \end{array}
\right] 
\left[
    \begin{array}{c}
      v' \\
      \lambda '
    \end{array}
\right]=
\left[
    \begin{array}{c}
      Mv \\
      -\phi 
    \end{array}
\right]
\tag{dual variable}
$$

This gives 

$$
\begin{cases} 
		Mv' &-&\Delta t J^\mathsf{T} \lambda ' &= &Mv \\ 
		\Delta t J v' &+& C \lambda ' &= &-\phi
\end{cases},
$$

and further

$$
Mv' = Mv - \Delta t J^\mathsf{T} C^{-1} \phi - \Delta t^2 J^\mathsf{T} C^{-1} J v' = Mv + f \Delta t  - \Delta t^2 J^\mathsf{T} C^{-1} J v'.
$$ 

If implicit time integration,

$$
\begin{cases} 
		\Delta v = a' \Delta t \Rightarrow  Mv' = Mv + f' \Delta t\\ 
		\Delta x = v' \Delta t.
\end{cases}
$$

So

$$
\begin{aligned}
& f' \Delta t - f \Delta t ≟ - \Delta t^2 J^\mathsf{T} C^{-1} J v'\\
\Rightarrow & f'- f ≟ -J^\mathsf{T} C^{-1} J \Delta x \\
\Rightarrow & \frac{\partial f}{\partial x} ≟ -J^\mathsf{T} C^{-1} J
\end{aligned}
$$





