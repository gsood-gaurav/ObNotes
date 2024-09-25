One of the problem in modern statistics is to approximate difficult to compute probability densities. **VI approximates probability densities through optimization**.

VI and MCMC are about approximating intractable densities and not only applies in Bayesian settings but other settings as well. In particular MCMC is about simulating from densities and VI is a tool for approximating densities.

**For decades dominant paradigm for approximate inference has been MCMC. In MCMC we construct an #erogodic markov chain on $z$ whose stationary distribution is the posterior $p(z|x)$. Then we sample from the chain to collect samples from the stationary distribution. Finally we approximate the posterior with an empirical estimate constructed from (a subset of) the collected samples. Important algorithms include Metropolis-Hastings algorithm and Gibbs Sampler**

However when we need an approximate conditional faster than a simple MCMC algorithm can produce, such as when data sets are large or models are very complex.

VI tends to be faster than classical methods like Markov chain Monte Carlo MCMC therefore an alternative to #MCMC. VI tends to be faster than MCMC and therefore easier to scale to large datasets.

In Bayesian Models latent variables help govern the distribution of the data. The idea behind VI is to first posit a family of densities, parameterized by free variational parameters, and then find the member of family i.e. setting of the parameters which is close to the target. Closeness is measured by #KLdivergence. $$q^*(z) = \mathop{\arg \min}\limits_{q(z) \in \mathbb{D}}KL ((q(z) || p(z|x))$$
MCMC and VI are different approaches to solving the same problem. MCMC samples a Markov Chain; variational algorithms solve an optimization problem. MCMC approximates the posterior with samples from the chain; VI approximates with result of the optimization.

MCMC tend to be more computationally intensive than VI, but they also provide guarantees of producing exact samples from the target density. VI doesn't enjoy such guarantees, it can only find a density close to the target but tends to be faster than MCMC.

Thus VI is suited for large datasets and scenarios where we quickly want to explore many models. MCMC is suited to smaller datasets where we are ready to pay a heavier computational cost for more precise samples.

Dataset size is not the only consideration. Another factor is geometry of the posterior distribution.
For example, the posterior of a mixture model admits multiple modes, each corresponding label permutations of the components. Gibbs sampling, if the model permits, is a powerful approach to sampling such target distributions; it quickly focuses on one the modes. For mixture models where Gibbs sampling is not an option variational inference perform much better than a more general MCMC technique.

> **Note we assume all unknown quantities are represented as latent random variables. This includes the parameter that might govern all the data, as found in Bayesian models, and latent variables that are local to individual points.****


Variational methods are used for inference and learning in graphical models (Bayesian Networks and Markov Random fields). <font style="color:red">Variational methods exploits the law of large numbers to transform the original graphical model in to simpler model in which inference is efficient. </font> Inference in simplified model provides bound on probabilities of interest in the original model.

The problem of probabilistic inference in graphical models is the problem of computing a conditional probability distribution over the values of some of the nodes. (the hidden or unobserved nodes) given the values of other nodes ("observed" nodes or "evidence")
Therefore $$P(H|E) = {\frac{P(H|E)}{P(E)}}$$
where H represents Hidden nodes and E represents Evidence.

