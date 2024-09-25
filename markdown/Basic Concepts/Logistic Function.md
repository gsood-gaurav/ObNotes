## Basic Derivation
- It is used in binary classification also known as sigmoid.
- The input to this function are sometimes known as logits which are logarithm of odds (log-odds)
- These unnormalized log probabilities are exponentiated to get unnormalized probabilities
- Finally normalization procedure reveals actual probabilities.

We start with log unnormalized probability of $y=0$ equal to 0.
$$
\begin{align*}
log \tilde{P}(y=0) &= 0  \\
\tilde{P}(y=1) &= 1 \\
log \tilde{P}(y=1) &= -0.4 \\
\tilde{P}(y=1) &= e^{-0.4} \\
P(y=1) &=  \frac{e^{-0.4}}{1 + e^{-0.4}} = 0.413 \\
P(y=1) &= \frac{1}{1 + e^{0.4}} \\
P(y=0) &= \frac{1}{1 + e^{-0.4}} = 0.598 \\
\end{align*}
$$

![[sigmoids.png]]
## Derivation of Sigmoid
- The derivative of sigmoid is continuously differentiable over whole input domain
-$$
\frac{d\sigma}{dx} = \sigma(x)(1-\sigma(x))
$$
