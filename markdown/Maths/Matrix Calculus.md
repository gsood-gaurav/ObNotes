
$$
\begin{align*}
df &= f(x+dx) - f(x) = f'(x) dx = \nabla{f}\cdot dx\\
f'(x) &= (\nabla f)^T
\end{align*}
$$
- Hilbert Space a continuous vector space with inner product.
- Banach space is continuous vector space with norm.
- Derivative $f'(x)$ is transpose of gradient $\nabla f$ .
## Product Rule
$$
\begin{align*}
f(x) &= xy \\
df &= dx\ y + x\ dy
\end{align*}
$$
Here x and y are objects in arbitrary real vector space, e.g. scalars, vectors, matrices or higher order arrays.
Below an example of a function which takes vector in and scalar out e.g. norm of a vector.
$$
\begin{align*}
f(x) &= \sqrt{(x^Tx)} \\
df &=  \frac{1}{\sqrt{x^Tx}}\ dx^T\ x + x^T\ dx \\
&= \frac{1}{\sqrt{x^Tx}}[2\ x^T\ dx] \\
f'(x) &=  \frac{1}{\sqrt{x^Tx}}[2\ x^T]\\
\nabla{f} &= f'(x)^T  \\
&= \frac{1}{\sqrt{x^Tx}}[2\ x]
\end{align*}
$$
### Another Example of product rule
- Takes a vector in and scalar out
$$
\begin{align*}
f(x) &= x^TAx \\
df &= f(x+dx) - f(x) \\
&= (x+dx)^TA(x+dx) - x^TAx\\
&= (x^T+dx^T)(Ax+Adx) - x^TAx\\
&= \cancel{x^TAx}+x^TAdx+dx^T(Ax)+\xcancel{dx^TAdx} - \cancel{x^TAx} \\
&= x^T(A+A^T)dx \\
f'(x) &= x^T(A+A^T) \\
\nabla{f} &= f'(x)^T = (A+A^T)x
\end{align*}
$$
## Derivative of $A^{-1}$ 
$$
\begin{align*}
AA^{-1} &= I \\
dA\ A^{-1} + A\ dA^{-1} &= 0 \\
A\ dA^{-1} &= - dA\ A^{-1} \\
dA^{-1} = -A^{-1}\ dA\ A^{-1}
\end{align*}
$$
## Calculus of Variation
$$
\begin{align*}
df = f(u+du) - f(u) = f'(u)[du]
\end{align*}
$$
where u $\in$ vector space of functions and usually $f(u) \in \mathbb{R}$ 