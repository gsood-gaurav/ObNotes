
$$
\begin{align*}
f_i &= y_i + \epsilon\\
(f-\hat{f})^2 &= (y-\hat{f})^2 -n\sigma^2 + 2\sigma^2\sum_{i=1}^n\frac{\partial{\hat{f_i}}}{\partial{y_i}}\\
(f-\hat{f})^2 &= (y-\hat{f})^2 -m\sigma^2 
\end{align*}
$$
Empirical error $\hat{f}-y$ 
True error $\hat{f}-f$ 

$m$ are test examples and $n$ are training examples

So we can arbitrarily minimize empirical training error during training because overfitting will start happening.
We can arbitrarily minimize empirical test error because that is good estimate of true test error 