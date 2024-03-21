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

Git Bash on Windows: when running sh, it seems that I have to go to the same directory where the .sh script lies and sh xx.sh, but not call it by sh xx/xx.sh from an indirect path

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
 & f' \Delta t - f \Delta t & ≟ & - \Delta t^2 J^\mathsf{T} C^{-1} J v'\\
 \Rightarrow ~ & f'- f & ≟ & -J^\mathsf{T} C^{-1} J \Delta x \\
 \Rightarrow ~ & \frac{\partial f}{\partial x} & ≟ & -J^\mathsf{T} C^{-1} J
\end{aligned}
$$

but

$$
\begin{aligned}
f &= - J^\mathsf{T} C^{-1}  \phi , \\
\frac{\partial f}{\partial x} &= -\frac{\partial J^\mathsf{T}}{\partial x } C^{-1} \phi -J^\mathsf{T} C^{-1} \frac{\partial \phi}{\partial x} = \frac{\partial J^\mathsf{T}}{\partial x } \lambda -J^\mathsf{T} C^{-1}  J  .
\end{aligned}
$$

Therefore, it needs to add the extra term to let

$$
Mv' = Mv - \Delta t J^\mathsf{T} C^{-1} \phi - \Delta t^2 J^\mathsf{T} C^{-1} J v' + \Delta t^2 \frac{\partial J^\mathsf{T}}{\partial x } \lambda v',
$$

and this induces back to

$$ 
\left[
\begin{array}{cc}
M - \Delta t^2 \frac{\partial J^\mathsf{T}}{\partial x } \lambda & -\Delta t J^\mathsf{T}  \\
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
\right].
$$

Only in this way does it equal first-order implicit time integration.

# Math derivation for a CNN problem

Let's consider the CNN operation:

$$
\begin{aligned}
\sum_j f_1(x) =& \sum_j \alpha_j A_j(x,x_j) := \sum_j \alpha_j A_j \\
\sum_j f_2(x) =& \sum_j \beta_j B_j(x,x_j) := \sum_j \beta_j B_j   \\
&\dots
\end{aligned}
$$

Given intuition by:

$$
\begin{aligned}
\alpha_1 A_1 \beta_1 B_1  &= \alpha_1 A_1 \cdot \beta_1 B_1\\
\alpha_1 A_1 \beta_1 B_1 + \alpha_2 A_2 \beta_2 B_2 &\neq 
(\alpha_1 A_1+\alpha_2 A_2) \cdot (\beta_1 B_1+\beta_2 B_2) \\
but &= \\ 
\frac{1}{2}(\alpha_1 A_1+\alpha_2 A_2) \cdot (\beta_1 B_1+\beta_2 B_2)
&+\frac{1}{2}(\alpha_1 A_1-\alpha_2 A_2) \cdot (\beta_1 B_1-\beta_2 B_2),
\end{aligned}
$$

a more general equality is to be derived. 

As illustrated in the figure, the desired $\textbf{diagonal}$ product addition $\sum_{j=1}^n A_j B_j$ can be realized by alternating extra signs and weights. Normally, every combination unit $A_p B_q$ is added $n$ times which results in $n$-times magnitudes. However, every combination has two chances to change its sign, when each dimension ($A$ or $B$) alters the negative sign to index $p$ or $q$. Thus, there are only $n-2$ times simple addition and twice negative-sign additions. We further let $c=\frac{n-2}{2}$ be the weight when the addition sign is negative, so the final result for all non-diagonal addition is guaranteed 0. For diagonal terms, nonetheless, the net addition gives $(c^2+n-1)A_j B_j$. It should then be normalized by this amount. 

Therefore, we can formulate:

$$
\sum_{j=1}^n f_1(x) f_2(x) = \frac{1}{(\frac{n-2}{2})^2+n-1} \sum_{k=1}^n (C_k \circ F_1 )(x) \cdot  (C_k \circ F_2 )(x),
$$

where $C_k$ is the kernel representation of aforementioned sign-weight alternation. It is acted on basic CNN kernels $F_1$ and $F_2$, where originally:

$$
F_1(x) = \sum_j f_1(x),~ and ~
F_2(x) = \sum_j f_2(x)
$$




