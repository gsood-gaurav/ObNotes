---
aliases: [Bernoulli Output Distributions]
---
- The simplest probability distribution is the Bernoulli distribution which can be used to model binary events
## Definition
Consider tossing a coin where the probability of event that it lands heads is given by $0 \le \theta \le 1$. Let $Y = 1$  denotes this event and let $Y=0$ denote the event that coin lands tails. Thus we are assuming that $p(Y=1)=\theta$  and $p(Y=0) = 1-\theta$. This is called Bernoulli distribution and can be written as follows $$Y \sim Ber(\theta)$$
where the symbol $\sim$ means "is sampled from" or "is distribute as" and Ber refers to Bernoulli. 
$$
Ber(y|\theta)=
    \begin{cases}
      1-\theta & \text{if}\ y=0 \\
      \theta & \text{if}\ y = 1
    \end{cases}
$$  
More concisely

$$Ber(y|\theta) \; {\buildrel\rm \triangle\over=}\;\theta{^y} \ (1-\theta)^{1-y}$$
Bernoulli is special case of Binomial Distribution. Let's suppose we observe $N$ coin tosses and $s$ is number of heads. Then distribution of s is given by
$$Bin(s|N,\theta) \; {\buildrel\rm \triangle\over=}\; {N\choose s} \ \theta^s (1-\theta)^{N-s}$$

