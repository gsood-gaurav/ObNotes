**2.1 For a fixed number of observations in a data set, introducing more variables
	normally generates a model that has a better fit to the data. What may be the drawback
	of such a model fitting strategy**
	Ans: True for a fixed number of observations in a data set, introducing more variables normally generates a model that has better fit to the data. The drawback is it leads to overfitting i.e. the model performs well on training data set but fails to generalize beyond training examples.
 **2.2 What are odd's of succeess?**
	Ratio of probability of success over probability of failure. For example if prob of success is $0.8$ and prob of failure is $0.2$ then odds of success is $0.8/0.2=4$. if probability of success if $p$ then odds of success are $\frac{p}{1-p}$.

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

**2.3 Interaction Terms**

A statistical interaction occurs if relation between the predictor $X$ and the response variable $Y$ depends upon the another independent variable $Z$. An interaction represents a synergizing or multiplicative effect tested by **adding a product variable $XZ$ to the model implying a non additive effect** that is over and above the effect of the linear effects of X and Z. The regression coefficient for the product term represents the degree to which there is an interaction between the two variables. If the interaction coefficient $\beta_3$ is significant, we conclude that the association between $X$ and the probability that $Y = 1$ depends on the values of $Z$.

Above interaction terms can be expressed as follows

$$
log(\frac{p}{1-p}) = \alpha + \beta_1X+\beta_2 Z + \beta_3 XZ
$$

>[!todo] Statistical tests for Interaction terms are **Wald chi-squared** test or a **likelihood ratio test** between the model with and without interaction term.
>How does interaction term relates to information theory
>




## 3. Probabilistic Programming and Bayesian DL

Most important result in Bayesian Statistics that family of beta distribution is conjugate to a binomial likelilhood.

3.1 A bernoulli trial refers to experiment with two outcomes success(1) and failure(0)
3.2 A binomial random variable X = r specifies num of success r in n independent Bernoulli trials
3.3  $X \sim Binomial(n, p)$ 
