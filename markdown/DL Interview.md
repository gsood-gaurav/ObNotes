 **What are odd's of suceess?**
	Ratio of probability of success over probability of failure. For example if prob of success is $0.8$ and prob of failure is $0.2$ then odds of success is $0.8/0.2=4$

## Logistic Regression

In Logistic Regression we model data using Bernoulli Distribution parameterized by $0\le\theta\le 1$ . $\theta$ is learnt from the data as linear combination of weights and features i.e. $w^Tx+b$ which should be restricted to $1$ as parameter $\theta$ is always between $0$ and $1$ for which we use sigmoid function $\sigma(x)$ 

>[!question] Why we use sigmoid function?
>- It is easier to take derivates 
>- Numerical methods for learning parameters are faster with sigmoid function



$$
\begin{align*}
\sigma(x) &= \frac{1}{1+e^{-x}} \\
\theta &= \frac{1}{1+e^{-a}}; a = {(w^tx+b)} \\
1+e^{-a} &= \frac{1}{\theta}\\
e^{-a} &= \frac{1}{\theta} -1\\
a &= log(\frac{p}{1-p})
\end{align*} 
$$

$a$ is called log-odds, logits, or pre-activations.


Statistical tests for Interaction terms are **Wald chi-squared** test or a **likelihood ratio test**.


