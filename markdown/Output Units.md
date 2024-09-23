- The choice of [[cost function]] is tightly coupled with the choice of output units. Most of the time we simply use the [[cross entropy]] between data distribution and model distribution. The choice of how to represent the output then determines the form of cross-entropy function

## Linear Units for [[Gaussian Output Distribution]]

^2557f2

Given feature $\mathcal{h}$, layer of linear output units produces a vector $\hat{\mathcal{y}} = \mathcal{W}^{\mathcal{T}}h + b$. Linear output layers are often used to produce the mean of a conditional Gaussian distribution.

$$\mathcal{p(y|x)} = \mathcal{N(y;\hat{y}},I)$$ Maximizing the log-likelihood ([[Maximum Likelihood]]) is equivalent to minimizing the mean squared error.

The maximum likelihood makes it straight forward to learn the [[covariance]] of the Gaussian too or to make the covariance of the Gaussian be a function of the input. However the covariane must be constrained to be a positive definite matrix for all inputs. It is difficult to satisfy such constraints with a linear output layer. so typically other output units are used to parametrize the [[covariance]]. 

Because linear units dont saturate they pose little difficulty for [[gradient based optimization]] algorithms and may be used with wide variety of optimization algorithms.

## Sigmoid Units for [[Bernoulli Output Distributions]]
The binary classfication task employs [[Bernoulli Distribution|Bernoulli Output Distributions]]. A [[Bernoulli Distribution|Bernoulli Output Distributions]] is defined by single number. The neural network needs to predict only $P(y=1|x)$. Suppose we were to use [[Output Units#^2557f2|linear Units]] and threshold its value to obtain a valid probability
$$P(y=1|x) = max\{0, min\{1, w^Th+b\}\}$$
This would indeed define a valid conditional distribution, but we would not be able to train it very effectively with gradient descent. Any time that $w^Th+b$ strayed outside the unit interval, the gradient of the output of the model with respect to its paramter would be $0$, which is problematic as learning alogrithm no longer has a guide for how to  improve the corresponding parameters.

Instead it is better to use different approach that ensures there is always a strong gradient whenver the model has the wrong answer The approach is based upon on using [[Sigmoid-Logistic Function|sigmoid output units]] combined with [[Maximum Likelihood|maximum likelihood]] 

## Other Output Types
The principle of [[Maximum Likelihood]] provides a guide for how to design a good cost function for nearly any kind of output layer. In general we define a condtional probability distribution $p(y|x;\theta)$, the principle of [[Maximum Likelihood]] suggests we use $-log\ p (y|x;\theta)$ as our cost function. In general, we can think of neural network as representing a function $f(x;\theta)$. The outputs of this function are not direct predictions of the value of $y$. Instead, $f(x;\theta)=\omega$  provides the parameters of the distribution over $y$. Our loss function can then be interpreted as $-log \ p(y;(\omega(x)))$ 