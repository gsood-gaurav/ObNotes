The Monte Carlo Method is a computational method that consists in using computer generated sample from a given probability distribution to produce a **plugin estimate** of some feature of the given distribution (such as, for example, a moment or a quantile). Samples are independent as compared to Markov chain monte carlo where samples can be correlated.

Let $\mathcal{X}$ be a random variable with distribution function $F_X(x)$ and suppose that we can generate a sample (through computer)

$$
\zeta_n = [x_1,\cdots,x_n]
$$
of realisations of $n$ random variables $X_1,\cdots,X_n$ all having distribution function $F_X$
denote by
$$
T(F_X)
$$
a feature of the distribution $F_X$ (e.g. its mean, variance, or one of its quantiles)

Denote by $F_n(x)$ the empirical distribution of the sample $\zeta_n$ (i.e. probability distribution that assingns probability $\frac{1}{n}$ to each one of the values $x_1\dots,x_n$ )

The plugin estimate 
$$
T(F_n)
$$
is a Monte Carlo approximation of $T(F_X)$. In other words feature $T(F_X)$ of the original distribution is approximated by the same feature $T(F_n)$ of the empirical distribution of the computer generated sample.


