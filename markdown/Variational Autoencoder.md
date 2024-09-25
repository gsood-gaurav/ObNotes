
>VAEs provides a principled framework for learning deep latent variable models and corresponding inference models.

>Learning is, most commonly, the process of searching for a value of the parameters $\theta$ such that probability distribution function given by the model, $p_{\theta}(x)$, approximates the true distribution of the data, denoted by $p^*(x)$ such that for any observed variable x $$p_{\theta}(x) \approx p^*(x)$$

One major division in Machine Learning is **Discriminative** vs **Generative** Modelling. 
**Discriminative Modelling aims to learn a predictor given observation**
**Generative Modelling aims to learn joint distribution over all variables.**
<font style="color:green">Generative Model simulates how data is generated in real world.</font>
Modelling is understood in every science as unveiling this generative process by hypothesizing theories and testing these theories through observations.
<font style="color:blue">Modelling in science is always generative. For instance weather modelling, astronomy etc</font>
We can encode physical laws and constraints in a generative model, test them against observations, we can confirm or reject our theories about how world works.

<font style="color:red">We can express causal relations of the world. Causal relations have the great advantage, they generalize much better to new situations than mere correlations. For instance, once we understand the generative process of an earthquake, we can use knowledge both in California, and in Chile.</font> 

While generative models can learn efficiently from the data, they also tend to make stronger assumptions on the data than their purely discriminative counterparts. <font style="color:red">often leading to higher asymptotic bias when the model is wrong.</font>

<font style="color:red">No matter how much data is around it may be beneficial to study the generative process in order to guide the training of the discriminator. For instance one may have few labelled examples and more unlabeled examples. In this semi supervised setting  one can use generative model of the data to improve classification</font>

Generative modelling can also be used as an auxiliary task. For instance predicting the immediate future may help us build useful abstractions of the world that can be used for multiple prediction tasks downstream.

VAE can be viewed as coupled, but independently parameterized model: the encoder or recognition model and the decoder or generative model.

The encoder delivers a posterior over latent variables to the generative model, which the latter needs to update its parameters  <font style="color:red">inside an iteration of EM</font>. Reversely generative model is scaffolds of sorts for the recognition model to learn meaningful representations of the data, including possibly class labels.

One advantage of VAE framework relative to ordinary VI is that recognition model is now stochastic function of input variables. This is in contrast to VI where each data case has a separate Variational distribution which is inefficient for large data sets. The recognition uses one set of parameters to model the relation between input and latent variables and such is called "amortized inference"

Sampling induces sampling noise in the gradients required for learning. Perhaps greatest contribution of VAE framework is that we can counteract this variance by using what is known as the "reparameterization trick", a simple procedure to reorganize our gradient computation that reduces variance in gradients.

Conditional Models become more difficult to learn when predicted variables are very high dimensional such as images, videos or sound. One example is reverse of classification problem: prediction of distribution over images, conditioned on the class label.

The main difficulty in MLE in DLVM is marginal likelihood is intractable.

# Variational AutoEncoder Framework

We saw problem of estimating **log-likelihood and posterior distribution** in DLVMs. The framework of autoencoders  provides a **computationally efficient** way for optimizing DLVMs jointly with a corresponding inference model using SGD. To turn DLVMs intractable posterior inference and learning problems into tractable problems, we introduce a parametric inference model $q_\phi(z|x)$. This model is called encoder or recognition model. With $\phi$ we indicate the parameters of this inference model, also called **_variational parameters_**. We optimize the variational parameters $\phi$ such that $$q_{\phi}(z|x) \approx p_{\theta}(z|x)$$
><font style="color:blue">From AI summer: There are five basic terms:</font>
> - The **prior distribution** $p(z)$, models the behavior of latent variables
> - The **likelihood** $p(x|z)$ that defines how to map latent variables to the data points.
> - The **joint distribution** $p(x,z) = p(x|z)p(z)$ which is multiplication of likelihood and prior essentially describes our model.
> - The **marginal**  $p(x)$ is the distribution of original data and is ultimate goal of the model. The marginal tells you how possible is to generate a data point
> - The **_posterior distribution_** $p(z|x)$ which describes the latent variables that can be produced by specific data points.

<font style="color:red">The approximation to the posterior help us to optimize the marginal likelihood</font>

The inference model can be any directed graphical model and the distribution $q_{\phi}(z|x)$ can be parameterized using neural network. In this case the variational parameters include weights and biases of neural network. $$(\mu, log\sigma) = EncoderNeuralNet_{\phi}(x)$$ $$q_{\phi}(z|x) = N(z;\mu, diag(\phi))$$
Typically in VAE single encoder neural network is used to perform posterior inference over all data points in our dataset. This can be contrasted with traditional Variational inference methods where variational parameters are not shared, but instead separately and iteratively optimized per data point. The strategy of VAE of sharing variational parameters across data points is called amortized inference. With amortized inference per data point  optimization loop is avoided and we leverage the efficiency of SGD.

In VAE we directly maximize `ELBO`. This approach is variational, because we optimize for best $q_{\phi}(z|x)$ amongst family of potential posterior distributions parameterized by $\phi$. It is called autoencoder because it is reminiscent of a traditional autoencoder model, where input data is trained to predict itself after undergoing an intermediate bottlenecking representation step.

## Evidence Lower Bound (ELBO)

`ELBO` is lower bound on the log likelihood of the data..
We can start with random values of $\phi$ and $\theta$ and stochastically optimize their values until convergence.

Maximizing the lower bound helps in 
- It will approximately maximize the marginal likelihood $p_\theta(x)$ also called **model evidence**, this means our generative model will be better
- It will minimize the KL divergence between the approximation $q_\phi(z|x)$ and true posterior $p_\theta(z|x)$, so $q_\phi(z|x)$ becomes better.
- Note that in the below equation $log\ p_{\theta}(x)$ doesn't depend upon variational parameter $\phi$. So any tuning of $\phi$ which increases ELBO will decrease KL divergence between actual and approximate posterior since $p_{\theta}(x)$ as both the term sum to constant.
- ELBO can be used to estimate the likelihood of the data.
̥$$log p_\theta(x) = \int q_\phi(z|x) logp_\theta(x) dz$$
$$  = \int q_\phi(z|x) log \left[\frac{p_\theta(z,x)}{p_\theta(z|x)} \right] dz $$
$$= \int q_\phi(z|x) log \left[ \frac{p_\theta(z, x)}{q_\phi(z|x)} \right] \left[ \frac{q_\phi(z|x)}{p_\theta(z|x)} \right] dz$$
$$= \int q_\phi(z|x) log \left[\frac{p_\theta(z,x)}{q_\phi(z|x)}\right]dz \ + \ \int q_\phi(z|x) log \left[\frac{q_\phi(z|x)}{p_\theta(z|x)}\right]dz $$
$$= \underbrace{E_{q_\phi(z|x)}\left[logp_\theta(z,x)]-logq_\phi(z|x)\right]}_{\mathscr{L_{\theta, \phi(x)}}(\text{ELBO})} \ + \ \underbrace{E_{q_\phi(z|x)} \left[\frac{q_\phi(z|x)}{p_\theta(z|x)} \right]}_{\text{KL\ Divergence}} $$

>[!info] Using  Jensen's Equality
> $$
> \begin{align*}
> log\ p_{\theta}(x) &= \int p(x,z) dz \\
> &= log\ \int \frac{p(x, z)q_{\phi}(z|x)}{q_{\phi}(z|x)} dz \\
> &= log\ \mathbb{E}_{q_{\phi}(z|x)}\left [\frac{p(x, z)}{q_{\phi}(z|x)}\right] \\
> &\ge \mathbb{E}_{q_{\phi}(z|x)}\left[log \frac{p(x, z)}{q_{\phi}(z|x)}\right]
> \end{align*}
> $$

The ELBO equation can be further simplified as
$$\mathcal{L} = E_{q_\phi(z|x)}[logp_\theta(x, z)- logq_\phi(z|x)]$$
$$= E_{q_\phi(z|x)}[logp_\theta(x| z) + logp_\theta(z)- logq_\phi(z|x)]$$
$$= E_{q_\phi(z|x)}[logp_\theta(x| z) + logp_\theta(z)- logq_\phi(z|x)]$$
$$= E_{q_\phi(z|x)}[logp_\theta(x| z)] \ - \underbrace{E_{q_\phi(z|x)}\left( \left[\frac{log\ q_\phi(z|x)}{log\ p_\theta(z)}\right]\right)}_{\displaylines{KL\ Divergence\ between\\ variational\ posterior\ latent\ and\ prior}}$$
Given an i.i.d dataset , the ELBO objective is sum of individual data point ELBO
$$\mathcal{L}_{\theta, \phi}(\mathscr{D}) = \sum \limits_{x \in \mathscr{D}} \mathscr{L}_{\theta, \phi}(x)$$
Therefore in maximizing ELBO we will reduce KL divergence between variational distribution and actual distribution and also maximize the marginal likelihood.

The individual-datapoint ELBO and its gradient $\nabla_{\theta, \phi}\mathcal{L}_{\theta, \phi}(x)$ is in general intractable. However good unbiased estimators exists such that we can still perform minibatch SGD.

## ELBO Gradient

Unbiased estimates w.r.t to generative model parameters $\theta$ are easier to obtain.

$$
\begin{align*}
\nabla_{\theta}\mathcal{L}_{\theta, \phi} &= \nabla_\theta[{E_{q_\phi(z|x)}\left[logp_\theta(z,x)]-logq_\phi(z|x)\right]}]\tag{1}\\
&= {E_{q_\phi(z|x)}[\nabla_\theta\left(logp_\theta(z,x)-logq_\phi(z|x)\right)}]\tag{2}\\
& \approx \nabla_\theta\left(logp_\theta(z,x)-logq_\phi(z|x)\right)\tag{3}\\
&= \nabla_\theta(logp_\theta(z,x))\tag{4}\\
\end{align*}
$$
The last line is simple monte carlo estimator of the second line where $z$ in last two equations is a random sample from $q_\phi(z|x)$. 

But unbiased gradients wrt to $\phi$ are more difficult to obtain, since ELBO's expectation is wrt to $q_\phi(z|x)$ which is function of $\phi$ itself.

$$
\begin{align*}
\nabla_{\theta}\mathcal{L}_{\theta, \phi} &= \nabla_\theta[{E_{q_\phi(z|x)}\left[logp_\theta(z,x)]-logq_\phi(z|x)\right]}]\tag{5}\\
& \ne {E_{q_\phi(z|x)}[\nabla_\phi\left(logp_\theta(z,x)-logq_\phi(z|x)\right)}]\tag{6}\\
\end{align*}
$$
In case of continuous variables we can use reparameterization trick to get unbiased estimates.

## Reparameterization Trick

For continuous latent variables, differentiable encoder and decoder, the ELBO can be differentiated wrt to $\theta$ and $\phi$ through change of variables also called the reparameterization trick.

First we express $z$ as some differentiable and invertible transformation of another random variable $\epsilon$ given $z$ and $\phi$ .

$$z = g(\epsilon,z,\phi)$$
where the distribution of $\epsilon$ is independent of $x$ and $\phi$. 

### Gradient of expectation under change of variable

$$
\begin{align*}
\mathbb{E}_{q_\phi(z|x)}[f(z)] & = \mathbb{E}_{p(\epsilon)}[f(z)]\\
\nabla_\phi[\mathbb{E}_{p(\epsilon)}[f(z)]] & = \mathbb{E}_{p(\epsilon)}[\nabla_\phi f(z)]\\
& \approx  \nabla_\phi f(z)
\end{align*}
$$
Here $z = g(\epsilon, \phi, x)$

## Gradient of ELBO

Under the reparameterization, we can replace an expectation w.r.t $q_\phi(z|x)$ with one w.r.t $p(\epsilon)$. The ELBO can be rewritten as

$$
E_{q_\phi(z|x)}[logp_\theta(z,x)]-logq_\phi(z|x)] = E_{p(\epsilon)}[logp_\theta(z,x)]-logq_\phi(z|x)]
$$
where $z=g(\epsilon, \phi, x)$ 

Therefor we can form a simple MonteCarlo estimator $\mathcal{L}_{\theta, \phi}(x)$ of the individual data point ELBO where we use a single noise sample $\epsilon$ from $p(\epsilon)$.

$$
\begin{align*}
\epsilon &\sim p(\epsilon) \\
z &= g(\epsilon, \phi, x)  \\
\mathcal{L}_{\theta, \phi}&= E_{q_\phi(z|x)}[logp_\theta(z,x)-logq_\phi(z|x)]
\end{align*}
$$

This series of operations can be expressed as a symbolic graph in software like TensorFlow, and effortlessly differentiated w.r.t. the parameters $\theta$ and $\phi$. The resulting gradient $\nabla_{\theta}\mathcal{L}_{\theta, \phi}$  is used to optimize the ELBO using minibatch SGD.

## Marginal Likelihood

After training VAE, we can estimate the probability of data under the model using an importance sampling.

$$
\begin{align*}
logp_{\theta}(x) &= log\ E_{q_\phi(z|x)}\left[\frac{p_{\theta}(x, z)}{q_\phi(z|x)}\right] \\
&\approx log \frac{1}{L}\ \sum\limits_{i=1}^L \frac{p_\theta(x, z^{(l)})}{q_\phi(z^{(l)}|x)}
 \\
\end{align*}
$$
where $z^{(l)} \sim q_\phi(z|x)$ is a random sample from inference model.