#DiffusionModels #GenerativeModelling #sampling

A diffusion process is a stochastic process similar to Brownian motion. Their path are like the trajectory of a particle submerged in a flowing fluid, which moves randomly due to unpredictable collisions with other particles. Let $\{x(t)\in\mathbb{R}\}_{t=0}^T$ be a diffusion process, indexed by continuous time variable $t\in[0,T]$. A diffusion process is governed by a stochastic differential equation (SDE) in the following form

$$dx = f(x,t)dt+ g(t)dw$$

where $f(\cdot, t):\mathbb{R}^d\rightarrow\mathbb{R}^d$ is called the _drift coefficient_ of the SDE, $g(t)\in\mathbb{R}$  is called the _diffusion coefficient_, and $w$ represent the standard Brownian motion. You can understand SDE as a stochastic generalization to ODE. Particles moving according to SDE not only follows the deterministic drift $f(x,t)$, but are also affected by the random noise coming from $g(t)dw$. From now on, we use $p_t(x)$ to denote the distribution of $x(t)$.

For score based generative modelling we will choose a diffusion process such that $x(0)\sim p_0$ and $x(T) \sim p_T$. Here $p_0$ is the data distribution where we have a dataset of i.i.d samples, and $p_T$ is the prior distribution that has a tractable for and easy to sample from. The noise perturbation by the diffusion process is large enough to ensure $p_T$ does not depend on $p_0$.

## Reversing the diffusion process

By starting from a sample from the prior distribution $p_T$ and reversing the diffusion process, we will be able to obtain a sample from the data distribution $p_0$. Crucially, the reverse process is a diffusion process running backward in time. It is given by the following reverse-time SDE

$$
dx = [f(x,t)-g^2\nabla_xlogp_t(x)dt] + g(t)d\tilde{w}
$$
where $\tilde{w}$ is a Brownian motion in the reverse direction, and $dt$ represents an infinitesimal negative time step. This reverse SDE can be computed once we know the drift and diffusion coefficients of the forward SDE as well as the score of $p_t(x)$  for each $t\in[0,T]$.

## Score Estimation

Based on above intuition we can construct time dependent score function $\nabla_xp_t(x)$ to construct the reverse-time SDE, and then solve it numerically to obtain samples from $p_0$ using samples from a prior distribution $p_T$. We can train a time-dependent score-based model $s_\theta(x,t)$  to approximate $\nabla_xlogp_t(x)$, using the following weighted sum of denoising score matching objectives.

$$
\underset{\theta}{min}\underset{t\sim\mathbb{U}(0,T)}{E}[\lambda(t)\underset{x(0)\sim p_0}{E}\ \ \underset{x(t)\sim p_t(x(t)|x(0))}{E}[\lVert s_\theta(x_t, t)-\nabla_{x(t)}logp_t(x(t)|x(0)) \rVert_2^2]]
$$
