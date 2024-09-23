
When we want to predict a binary variable $y\in \{0, 1\}$ given some inputs $x\in X$, we need to use a conditional probability distribution of the form

$$ p(y|x) = \text{Ber}(y|f(x;\theta))\tag{1}$$ where $f(x;\theta)$ is some function that predicts the mean parameter of the output distribution. To avoid requirement that $0 \le f(x;\theta) \le 1$ we can let f be an unconstrained function and use the following model

$$p(y|x,\theta) = \text{Ber}(y|\sigma(f(x;\theta)))\tag{2}$$ Here $\sigma()$ is the sigmoid or logistic function is defined as follows:

$$\sigma(a) = {1 \over 1+e^{-a}} \tag{3}$$ where $a = f(x;\theta)$. we see it maps the whole real line to $[0,1]$ which is necessary to be interpreted as probability and hence a valid value of the Bernoulli parameter.

The quantity $a$ is log-odds, thus sigmoid maps log-odds to $p$. 
$$p = \sigma(a)$$
Similarly inverse of logistic is logit which maps p to log-odds
$$a = \sigma^{-1}(p)= logit(p) = log({p\over 1- p})$$
## Justification of Sigmoid
We fix the log of unnormalized probability of event 0 to be 0 and place the log unnormalized probability of the event 1 to be anywhere on the real line.

$$log \ \tilde{P}(y=1) = x\tag{5}$$
$$log\ \tilde{P}(y=0) = 0\tag{6}$$ $$\tilde{P}(y=1) = e^x\tag{7}$$
$$\tilde{P}(y=0) = e^0 = 1\tag{8}$$ $$p(y=1) = {\tilde{p}(y=1)\over\tilde{p}(y=1)+\tilde{p}(y=0)}= {e^x\over1+e^{x}} = {1\over1+e^{-x}}\tag{9}$$
## Derivative of Sigmoid
$${{d\sigma}\over dx} = \sigma(x)\ . (1-\sigma(x))\tag{10}$$ 
## Motivation of Sigmoid
A sigmoid output unit can be defined by 
$$y = \sigma(w^Th+b)$$ where $\sigma$ is the logistic sigmoid function.

$log \tilde{P}=yz$
$\tilde{P}(y)=exp(yz)$ 
$P(y) = {exp(yz)\over{\sum_{y^\acute = 0}^1} exp(y\acute z)}$ 
$P(y) = \sigma((2y-1)z)$

The approach to predicting probabilites in log space is natural to use with maximum likelihood learning. Because the cost function used with maximum likelihood is $-log P(y|x)$, the log in the cost function undoes the exp of the sigmoid. Without this effect the saturation of the sigmoid could prevent gradient based learning from making good progress. The loss function for maximum likelihood learning of a Bernoulli parmaterized by a sigmoid is 

$J(\theta) = -log P(y|x)$ 
       $=-log\sigma ((2y-1)z)$
        $=\zeta((1-2y)z)$

