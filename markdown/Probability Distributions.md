## Discrete Probability Distribution

A discrete probability distribution specifies distribution over discrete set of values.
We can represent such a distribution as <span style="color:rgb(146, 208, 80)">_probability mass function</span>_, which assigns probability to every possible assignment of its input variable to a value.

$$
\sum_{i=1}^nP(X=i) = 1
$$

>[!note] The parameters of a distribution governs the probability associated with different assignments

## Continuous Probability Distributions

It is a distribution over a continuous set of values. For many continuous distributions the probability that a variables takes a particular value is infinitesimally small. One way to represent continuous probability distribution is to use a probability density function. if $p(x)$ is probability density function over $X$, then $p(x)d(x)$ is the probability that $X$ falls within interval $(x, x+dx)$ as $dx\rightarrow 0$. Similar to probability mass function, probability density functions should sum to $1$

$$
\int_{-\infty}^{\infty}p(x) dx = 1
$$

Another way to represent a continuous distribution is with a<span style="color:rgb(146, 208, 80)"> _cumulative distribution function</span>_ which specifies the probability mass associated with values below some threshold. If we have a cumulative distribution function $P$ associated with variable $X$, then $P(x)$ represents the probability mass associated with $X$ taking on a value less than or equal to $x$. A cumulative distribution function can be defined in terms of a probability density function $p$ as follows

$$
cdf_X(x) = P(X=x) = \int_{-\infty}^xp(x') dx'
$$
Related to cumulative distribution function is the _quantile function_, also called the _inverse cumulative distribution function_. The value of $quantile_X(\alpha)$ is the value $x$ such that $P(X\le x)=\alpha$. In other words quantile function returns the minimum value of $x$ whose cumulative distribution value is greater than or equal to $\alpha$. Of course, we have $0\le\alpha\le 1$.

## Gaussian Distribution

The Gaussian Distribution is parameterized by mean $\mu$, variance $\sigma^2$.

$$
p(x) = \mathcal{N}(x;\mu, \sigma^2)
$$
probability density at $x$ is given by 

$$
\mathcal{N}(x|\mu, \sigma^2) = \frac{1}{\sigma}\phi\left(\frac{x-\mu}{\sigma}\right)
$$
where $\phi$ is standard normal density function:

$$
\phi(x) = \frac{1}{\sqrt{2\pi}} exp(-\frac{x^2}{2})
$$
## Joint Distributions

A distribution over multiple variables is called<span style="color:rgb(146, 208, 80)"> multivariate distribution</span>. 
From joint we can compute marginal using law of total probability
$$
\begin{align*}
P(x) &= \sum_y P(x,y)\\
p(x) &= \int_yp(x,y)dy
\end{align*}
$$
Independence can greatly simplify the representation of joint distribution of parameters. For example if we have $n$ binary variables complete specification of joint distribution requires $2^n-1$ parameters. Instead we assume independence among variables we require only $n$ parameters.