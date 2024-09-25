Suppose that we have a function $f:\mathbb{R}^n\rightarrow\mathbb{R}^m$, which maps $n-$ dimensional input $x\in\mathbb{R}^n$ to $m-$dimensional output $y\in\mathbb{R}^m$.

One way to view this function is a column vector of $m$ scalar-valued functions stacked one on top of each other.
$$
f(x) 
= 
\begin{bmatrix}  
f_1(x_1,... ,x_n)\\  
f_2(x_1,...,x_n) \\
\vdots \\
f_m(x_1,...x_m)
\end{bmatrix}
$$
## Vector Jacobian Product(VJP)

Given a vector $\mathcal{u}\in\mathbb{R}^m$, the VJP is the following **_row vector_*
$$
\begin{align}
\mathcal{u}^T\mathcal{J}\in\mathbb{R}^n
\end{align}
$$
Being n dimensional we have one VJP element for each of the function inputs, $x$ (it is an input space concept)

**_It tells by how much must each of the inputs should change, in order to effect a change $u$ in the outputs._**

We might think of it as a sensitivity map over the inputs: if I want to increase the first output $y_1$ by $0.5$  (by setting $u_1=0.5$ and $u_{i\neq 1}=0$) then the resulting $n-$dimensional VJP will tell me how I ought to perturb $x$.

This is what we do during reverse-mode differentiation.
```python
def f2(x1, x2, x3):
	return jax.numpy.array(x1**2 + x2 + x3), jax.numpy.array(x1 - x2 + x3)
```

```python
# Vector Jacobian Product
y, vjp_fn = jax.vjp(f2, 2.0, 3.0, 1.0)
vjp_fn((1.0, 0.0))
```


## Jacobian Vector Product(JVP)

Given a vector $\mathcal{v}\in\mathbb{R}^n$, the JVP is
$$
Jv\in\mathcal{R}^m
$$
Being $m$ dimensional we have JVP for each of the function output, $y$ (it is an output space concept)

**_It tells us how much do the outputs of f change if I make a perturbation v to the inputs?_**

We might think of it as a **_directional derivative_** of $f$ in the direction of $v$. If I perturb the first input element $x_1$ by $0.5$ (by setting $v_1=0.5$ and $v_{i\neq 1}=0$) then the resulting $m-$dimensional JVP will tell me how much the output $y$ will change.

This is what happens during forward-mode differentiation.
```python
# Jacobian Vector Product
primals, tangents = jax.jvp(f2, (2.0, 3.0, 1.0), (1.0, 0.0, 0.0))
```


Note that the JVP really just corresponds to a first order Taylor approximation to the function $f$. If the function $f$ is differentiable at some point $x_0$ then we can approximate it as:
$$
f(x) = f(x_0) + J(x-x_0) + o(||x-x_0||)
$$
where $o(||x-x_0||)\rightarrow 0$   as $x-x_0\rightarrow 0$.
We often refer to this as the linearization of $f$.

