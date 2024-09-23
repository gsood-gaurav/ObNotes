- Sampling from a distribution known up to a certain constant called Normalization Constant.
- ![[Pasted image 20240909201208.png]]
Consider above probability density function given by the following analytical expression

$$
p(x) = \frac{(exp(-x^2) + (2+sin(5x) + sin(2x)))}{\int_{-\infty}^\infty exp(-u^2)(2+sin(5u)+sin(2u))du}
$$

Now either we don't know how to calculate the denominator or too lazy to calculate. So that means I only know the distribution up to a certain constant i.e.

$$
p(x) \propto (exp(-x^2) + (2+sin(5x) + sin(2x))
$$

Basic idea of MCMC is to define a markov chain over possible values of $x$ in such a way that stationary distribution of the Markov chain is infact $p(x)$. That is , what we're going to do is use a Markov chain to generate a sequence of $x$ values denoted $(x_0, x_1,x_2,x_3,x_4\cdots x_n)$, in such a way that as $n\to\infty$ we can gaurantee that $x_n\sim p(x)$. There are many different ways of setting up a Markov chain that has this property. The Metropolis Hasting is one of these.

x

