- Using Squared loss in logistic regression as cost function makes optimization problem non-convex.
- We use Binary cross Entropy as loss function (cost function is average loss function) which is always convex
$$
\begin{align*}
\mathcal{L}(\hat{y}, y) &= -(y\ log(1-\hat{y}) + (1-y)\ log(1-\hat{y})) \\
\hat{y} &= \sigma(w^Tx + b),\ \ \ \ \ \ \ \sigma(z) = \frac{1}{1+e^{-z}}\\
\mathcal{J(w, b)} &= -\frac{1}{m} \sum\limits_{i=1}^m y^{(i)}log\ \hat{y}^{(i)} + (1-\hat{y}^{(i)})\ log(1-\hat{y}^{(i)})
\end{align*}
$$
## Why above loss function makes sense?

When $y=1$ loss function becomes $-log(\hat{y})$, which means we want   $-log(\hat{y})$ as low as possible, which means $log(\hat{y})$ should be as large as possible which means $\hat{y}$ should be as large as possible and since $\hat{y}$ cannot be greater that one it means we want it closer to 1.

When $y=0$ loss function becomes $-log(1-\hat{y})$ , which means we want $log(1-\hat{y})$ to be as large as possible, which means $1-\hat{y}$ should be as large as possible which means $\hat{y}$ should be as small as possible, as $\hat{y}$ cannot be negative we want $\hat{y}$ closer to $0$.

## Logistic Regression on m examples

$$
\begin{align*}
J = 0, dw_1=0, dw_2=0, b=0 \\

z^{(i)} = w^Tx^{(i)} + b \\
a^{(i)} = \sigma{(z^{(i)})} \\

J += -(y^{(i)}\ loga^{(i)} + (1-y^{(i)})\ log(1 - a^{(i)})) \\
dw_1 += x_1^{(i)}\ dz^{(i)} \\
dw_2 += x_2^{(i)}\ dz^{(i)} \\
db += dz^{(i)} \\

J /= m, dw_1 /= m, dw_2 /=m, db /= m \\

w_1 += -\alpha * dw_1 \\
w_2 += -\alpha * dw_2 \\
b += - \alpha * db
\end{align*}

$$
