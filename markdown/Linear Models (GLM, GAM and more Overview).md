The biggest strength but also the biggest weakness of the [[Linear regression]] model is that the prediction  is modeled as a weighted sum of the features. In addition, the linear model comes with many other assumptions.
- The outcome given features might not have a non-Gaussian distribution.
- Features might interact
- Relationship between features and outcomes might be non linear.

We can extend linear models using extensions such as Generalized Linear Model (GLMs) and Generalized Additive Models (GAMs)

The formula for linear regression model

$y = \beta_{0} + \beta_{1}x_1 + \beta_{2}x_2+...+ \beta_{p}x_p+\epsilon$   

The linear regression model assumes that the outcome $y$ of an instance can be expressed as weighted sum of its features with an individual error $\epsilon$ that follows a Gaussian distribution. By forcing the data into this corset of a formula, we obtain a lot of model interpretability. The feature effects are additive, meaning no interactions, and the relationship is linear, meaning an increase of a feature by one unit can be directly translated into an increase/decrease of the predicted outcome.

>**The linear model allows us to compress the relationship between a feature and the expected outcome into a single number, namely the estimated weight.**

Three problems with Linear Regression Models
- Gaussian Distribution of the outcome given the features.
- Additivity
- Linear Relationship

## Non Gaussian Outcomes - GLMs

The linear regression model assumes that the outcome given the input features follows a Gaussian distribution. We can extend it for non  Gaussian Distributions using _Generalized Linear Models_

>**The core concept of any GLM is keep the weighted sum of the features, but allow non-Gaussian outcome distributions and connect the expected mean of this distribution and the weighted sum through a possibly non linear function. For example, the logistic regression model assumes Bernoulli distribution for the outcome and links the expected mean and the weighted sum using the logistic function**.

The GLM mathematically links the weighted sum of the features with the mean value of the assumed distribution using the link function $g$ which can be chosen flexibly depending upon the outcome.

$g(E_y(y|x)) = \beta_0 + \beta_1x_1+...+\beta_px_p$

GLM consist of three compnents: The link function g, the weighted sum $X^T\beta$ (sometimes called  linear predictor) and a probability distribution from the exponential family that defines $E_Y$ 

Let us consider the classic linear model as a special case of a GLM. The link function for the Gaussian Distribution in the classic linear model is simply the identity function. 

Under the GLM framework, this concpet generalizes to any distribution and arbitrary link functions. If $y$ is count of something, such as the number of coffees someone drinks on a certain day, we could model it with a GLM with a Possion Distribution and the natural logarithm as the link function:

$$ln(E_Y(y|x)) = x^T\beta$$
The logistic regression model is aslo a GLM that assumes a Bernoulli distribution and uses the logit function as link function. The mean of binomial distribution used in logistic regression is the probability that y is 1

$$P(y=1) = {1 \over 1+ exp(-x^T\beta)}$$  
Each distribution from the exponential family has a canonical link function that can be derived mathematically from the distribution. The GLM framework makes it possible to choose the link function independently of the distribution.

## Generalized Additive Model (GAMs) Non Linear Effects

The world in not linear. Linearity in linear models means no matter what value an instance has in a particular feature, increasing the value by one unit always has the same effect on the predicted outcome. Is it reasonable to assume that increasing the temprature by one deegre at 10 deegres Celsius has the same effect on the number of bike rentals as increasing the temprature when it already has 40 deegres. Intutively on expects that increasing the temprature from 10 to 11 deegres Celsius has a positive effect on bicycle rentals and from 40 to 41 a negative effect. The temprature feature has a linear, positive effect on the number of rental bikes but at some point  it flattens out and even has a negative effect a high temperatures. The linear model doesn't care.