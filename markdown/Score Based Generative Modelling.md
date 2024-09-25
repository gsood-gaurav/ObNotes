We can learn score functions (gradient of probability density functions) on large number of noise-perturbed data distributions, then generate samples with Langevin type sampling.

>The score function is the gradient $\nabla_x\ log\ p(x)$  of the log of the probability density function $p(x)$ of a probability distribution with respect to the distribution's support.

The advantage of score function estimation is it doesn't depend upon normalization constant $Z_{\theta}$. Infact any neural network which maps input vector $x \in \mathcal{R}^d$ to an output vector $y \in \mathcal{R}^d$ can be used as score based model as long as the output and input have same dimensionality.

Scores will arise when we will reverse the diffusion process for sample generation.

The idea of score function is to learn a model $s_\theta(x):\mathbb{R^d}\rightarrow\mathbb{R^d}$ of the score function from a dataset of sample points.
- We are given a dataset $\mathbb{D} = {x_1, x_2...,x_n}$ 
- Our task is to estimate $\nabla_x\ log\ p_{data}(x)$ 
- Our model is a parameterized function $s_{\theta}(x): \mathbb R^d\rightarrow \mathbb R^d$ 
- Our objective is that $\nabla_x\ log\ p_{data}(x) \approx s_{\theta}(x)$ 

A **diffusion process** is a stochastic process similar to **Brownian motion**.  Their paths are like trajectories of particle submerged in a flowing fluid, which moves with randomly due to unpredictable collisions with other particles. 

The score based estimation has two independent problems.
> [!bug] Problems to solve
> - Scalable estimation of score
> - Using score for generative modelling.

Diffusion Models, at its core, follow the exact same principle, but with a slightly clever design. For diffusion models, the transformation $f_\theta$ is rather complicated. It is a sequence of invocations of a neural function (denoted as $s_\theta$) along with some additional computation (denoted as g(⋅))
$$
	x = g_1(g_2(g_3(\cdots\ z \cdots, s_\theta),s_\theta),s_\theta), where\ z \sim \mathcal{N}(0, I)
$$

Creating noise from data is easy, creating data from noise is generative modelling.