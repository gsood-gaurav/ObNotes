>[!note] RL is Goal directed learning from interacting with environment.

 - produces Cause and effect 
- consequences of actions are known
- what to do in order to achieve goals

>[!note ] Distinction between state and observation

Two ways to find optimal policy/behavior
- Value based Methods
- Policy based methods

mapping situations to actions in order to maximize numerical reward signal.
Discover which actions yield more reward by trying them.
In most interesting and challenging cases current action may not only affect immediate reward, but also next situation and through that subsequent rewards.

>[!quote] Reinforcement Learning learns from batches of experience. The question is how do they collect it? In online reinforcement learning agent gathers data directly: it collects a batch of experience by interacting with the environment. Then, it uses the experience immediately (or via some replay buffer) to learn from it (update its policy). But this implies that either you train your agent directly in the real world or have a simulator. If you don't have one you need to build it which can be very complex. On the other hand, in offline reinforcement learning, the agent only uses data collected from other agents of human demonstrations it doesn't interact with the environment.



Can we say RL is computational approach to solving Sequential Decision Making which is formalized using Markov Decision Processes.

> [!note] Two most important characteristics of RL
> - Trial and Error
> - Delayed Reward


RL is simultaneously a problem, a class of solution methods that work well on the problem and the field that studies this problem and solution method.

The problem of RL is formalized using ideas from dynamical system theory, specifically, as the optimal control of incompletely known Markov Decision processes.

Trade off between exploitation and exploration.

>[!note] Four main subelements of the reinforcement learning
>- Policy
>- reward signal
>- value function
>- optionally model of the environment


**Policy** is mapping from perceived states of the environment to actions to be taken when in those states.

**Reward** signals are stochastic functions of the state of environment and the actions taken.

**Value** function specifies what is good in the long run whereas reward function specifies what is good in an immediate sense. Value of state is total amount of reward an agent can expect to accumulate over the future starting from that state. Whereas rewards determine the immediate, intrinsic desirability of environmental states, values indicate the long-term desirability of states after taking into account the states that are likely to follow and the rewards available in those states. For example a state might always yield a low immediate reward but still have a high value because it is regularly followed by other states that yield high rewards. Or the reverse could be true.

**Model of the environment, something that mimics the environment**
Models are used for planning which means deciding on a course of action by considering possible future situations before they are actually experienced.
Methods for solving reinforcement learning problems that use models and planning are called model based methods.

The central role of value estimation is arguably the most important thing.

We seek actions that bring about states of highest value not highest reward.

## Finite Markov Decision Processes (MDPs)

Introduce the formal problem of finite MDPs which we try to solve in rest of the book.
The problem involves <span style="color:rgb(146, 208, 80)">evaluative feedback</span> as in bandits but also and <span style="color:rgb(146, 208, 80)">associative aspect</span>----- choosing different actions in different situations. MDPs are classical formalization of <span style="color:rgb(146, 208, 80)">Sequential Decision Making</span>, where actions not only influence immediate rewards but also subsequent states and through those future rewards. Thus MDPs involve <span style="color:rgb(0, 112, 192)"><span style="color:rgb(0, 112, 192)">delayed reward</span></span> and the need to tradeoff immediate and delayed reward. (<span style="color:rgb(255, 0, 0)">The rewards are delayed as we are accounting for rewards which we are going to receive in future and hasn't got yet, so it has been delayed in a way?. In sequential decision making delyaed rewards becomes important.</span>)

>[!note] Bandits vs RL
>In bandits we estimate $q_*(a)$ for each action $a$, in MDPs we estimate $q_*(s, a)$ for each action is state s or we estimate value $v_*(s)$ for each state given optimal action selections.

<span style="color:rgb(146, 208, 80)">MDPs are mathematically idealized form of Reinforcement Learning problem for which precise theoretical statements can be made.</span>

`Environment `give rise to `reward`. Rewards are not in control of `agent.`

>[!note] Key elements of MDPs
>- Returns: is the function of future rewards that the agent seeks to maximize.
>- value functions: assign to each state or state-action pair, the expected return achievable from that state or state-action pair
>- optimal value functions: assigns to each state or state-action pair the largest expected return achievable by any policy.
>- Bellman Equations

At each time step $t$ agent receives some representation of the `environment.`

The MDP and agent give rise to following trajectory

$$
S_0, A_0, R_1, S_1, A_1, R_2, S_2, A_2, R_3,\cdots
$$

In Finite MDPs, the set of states, actions, rewards $\mathcal{S}, \mathcal{A}, \mathcal{R}$  all have finite number of elements. In this case random variables $R_t, S_t$ has well defined discrete probability distributions depending only upon the previous state and action.

$$
\begin{align*}
p(s', r|s, a) &= Pr(S_t=s', R_t=r|S_{t-1}=s, A_{t-1}=a)\\
\sum_{s'\in\mathcal{S}}\sum_{r\in\mathcal{R}}p(s',r|s, a) &=1\ \forall s\in\mathcal{S}, a\in\mathcal{A(s)}\\
p(s'|s,a) &= \sum_rp(s',r|s, a) \\
r(s, a) &= \sum_r r p(r|s, a) \\
&= \sum_r r \sum_{s'} p(s',r|s, a) \\
r(s', a, s) &= \sum_r r p(r|s',a,s) \\
&= \sum_r r \frac{p(r, s'|s, a)}{p(s'|s,a)}
\end{align*}
$$

The general rule we follow is that anything that cannot be changed arbitrarily by the agent is considered to be part of environment.

It is typical in reinforcement learning tasks to have states and actions with such structured representation like vector or list of numbers. Rewards on the other hand are always list of numbers. 
## Reward and Returns

Goal of the agent is formalized in terms of `rewards`. 

>[!note] That all of what we mean by goals and purposes can be well thought of as the maximization of the expected value of cumulative sum of  received scalar signal(called reward).

The sequence of rewards after time $t$ is denoted by $R_{t+1},R_{t+2},R_{t+3}\cdots$ then return is defined as any **function of this reward sequence**. One common choice of function is take the sum so return  becomes the cumulative sum of reward sequence and goal is to maximize the expectation of this cumulative sum.
$$
G_t = R_{t+1}+R_{t+2}+R_{t+3}+ \cdots + R_T
$$
The additional idea of discounting can also be applied so return becomes
$$
\begin{align*}
G_t &= R_{t+1}+\gamma R_{t+2}+\gamma^2 R_{t+3}+ \cdots \\
G_t &= R_{t+1} + \gamma G_{t+1}\\
where\ 0\le\gamma\le1
\end{align*}
$$
## Policies and Value Functions

Almost all RL algorithms involve <span style="color:rgb(255, 0, 0)">estimating</span> <span style="color:rgb(255, 0, 0)">value functions</span>--functions of states $v_\pi$(or of state-action pairs $q_\pi$) that estimate how good it is for the agent to be in a given state (or how good it is to perform a given action in  a given state). The notion of "how good" here is defined in terms of future rewards that can be expected or to be precise, in terms of <span style="color:rgb(146, 208, 80)">expected return</span>. Of course the rewards the agent can expect to receive in the future depend on what actions it will take. Accordingly value functions are defined with respect to particular ways of acting called <span style="color:rgb(255, 0, 0)">policies</span>.

$$
v_\pi(s) = \mathbb{E}_\pi[G_t|S_t=s] = \mathbb{E}\bigg[\sum_{k=0}^\infty\gamma^kR_{t+k+1}|S_t=s\bigg] \forall s \in S
$$
Similarly we define the value of taking action $a$ in state $s$ under a policy $\pi$, denoted by $q_\pi(s, a)$ as the expected return starting from $s$ taking the action $a$ and thereafter following the policy $\pi$

$$
q_\pi(s, a) = \mathbb{E}_\pi[G_t|S_t=s, A_t=a] = \mathbb{E}\bigg[\sum_{k=0}^\infty\gamma^kR_{t+k+1}|S_t=s, A_t=a\bigg] \forall s \in S, a\in A
$$
where $\mathbb{E}_\pi[\cdot]$  is expected value of random variable given that the agent follows policy $\pi$.

The value functions $v_\pi$ and $q_\pi$ can be estimated from experience. For example, if an agent follows policy $\pi$ and maintains average, for each state encountered, of the actual returns that have followed that state, then the average will converge to the state's value, $v_\pi(s)$, as the number of times that state is encountered approaches infinity. If separate averages are kept for each action taken in each state, then these averages will similarly converge to the action values, $q_\pi(s, a)$. We call estimation methods of this kind <span style="color:rgb(255, 0, 0)">Monte Carlo Methods</span> because they involve averaging over many random samples of actual returns. Of course, if there are very many states, then it may not be practical to keep separate averages for each state individually, Instead, the agent would have to maintain $v_\pi$ and $q_\pi$ as parameterized functions (with fewer parameters than states) and adjust the parameters to better match the observed returns.

RL methods specify how the agent's policy is changed as a result of its experience.

A fundamental property of value functions used throughout RL and dynamic programming is that they <span style="color:rgb(255, 0, 0)">satisfy recursive relationships</span> similar to what we have established for returns.

The value of state $s$ under a policy $\pi$, denoted by $v_\pi(s)$ is the expected return when starting in $s$ and following $\pi$ thereafter. For MDPs we can define $v_\pi(s)$ formally by

$$
\begin{align*}
v_\pi(s) &= \mathbb{E}_\pi[G_t|S_t=s] \\
&= \mathbb{E}_\pi[R_t+\gamma G_{t+1}|S_t =s]\\
&= \mathbb{E}_\pi[R_t]+\mathbb{E}_\pi[\gamma G_{t+1}|S_t =s]\\
&= \mathbb{E}_\pi[R_t] + \gamma\mathbb{E}_\pi[\mathbb{E}_\pi[G_{t+1}|S_{t+1}, S_t=s]|S_t=s](Law  \ of \ total\ expecation)\\
&= \\
&= \sum_a\pi(a|s)\sum_{s'}\sum_rp(s', r|s, a)[r + v_\pi(s')]
\end{align*}
$$
$v_\pi(s)$ is called state value function. This can re read as expected value. For every triple $a,s,r$ we compute the probability $\pi(a|s)\ p(s',r|s,a)$  weight the quantity in brackets by that probability then sum over all possibilities to get an expected value.

The value function $v_\pi$ is the unique solution to its Bellman Equation. We show in subsequent chapters how this Bellman Equation forms the basis of number of ways to compute, approximate and learn $v_\pi$ 

>[!note] The existence and uniqueness of $v_\pi$ is guaranteed as long as either $\gamma <1$ or eventual termination is guaranteed from all states under the policy $\pi.$



Similarly $q-function$ can be defined as
$$
\begin{align*}
q(s, a) &= E_\pi[G_t|S_t=s, A_t=a]\\
q(s, a) &= \sum_{s'}\sum_rp(s', r|s, a)[r + v_\pi(s')]
\end{align*}
$$

## Return

$$
\begin{align*}
G_t &= R_{t+1}+R_{t+2}\cdots \infty
&= \sum_{k=0}^\infty R_{t+k+1}
\end{align*}
$$


## Optimal Value Functions

Objective is to find the optimal policy, there can be many on them and let's denote all of them by $\pi_*$ 
All optimal policies share same optimal state-value function $v_*(s)$ which is defined as follows
$$
v_*(s) = \underset{\pi}{max}\ v_\pi(s)\ \forall s \in \mathcal{S}
$$

Similarly all optimal policies share same optimal action-value function which is defined as

$$
q_*(s, a) = \underset{\pi}{max}\ q_\pi(s, a)\ \forall s\in\mathcal{S}, a\in\mathcal{A(s)}
$$

$$
v_\pi(s) = \sum_a\pi(a|s)\ q_\pi(s, a)
$$

Many different decision-making methods can be viewed as ways of approximately solving the Bellman optimality equation. Many RL methods can be clearly understood as approximately solving the Bellman optimality equations using actual experienced transitions in place of knowledge of the expected transitions.

>[!note] Whereas the optimal value functions for states and state-actions pairs are unique for given MDP, there can be many optimal policies. Any policy that is greedy w.r.t the optimal value functions must be an optimal policy. The Bellman optimality conditions are special consistency conditions that the optimal value functions must satisfy and that can be solved for the optimal value functions for which an optimal policy can be determined with relative ease.



The on-line nature of reinforcement learning makes it possible to approximate optimal policies in ways that put more effort into learning to make good decisions for frequently encountered states, at the expense of less effort for infrequently encountered states. This is one key property that distinguishes RL from other approaches to approximately solving MDPs.

>[!note] Actions are making choices
States are the basis on which choices are made
Rewards are the basis on which choices are evaluated.


## Dynamic Programming

Can compute optimal policies given perfect model of the environment.
Provides essential foundations for the understanding of the methods presented in the rest of this book.
In fact, all of these methods can be viewed as attempts to achieve much the same effect as DP, with less computation and without assuming a perfect model of the environment.

>[!note] The key idea of DP, and of reinforcement learning generally, is the use of value functions to organize and structure the search for good policies.

We can easily obtain optimal policies once we have found the optimal value functions $v*$, $q*$.

$$
\begin{align*}
v_*(s) &= \underset{a}{max}\ \mathbb{E}\big[R_t + \gamma v_*(S_{t+1})\ |S_t=s, A_t=a\big] \\
&= \underset{a}{max} \sum_{s',r}p(s',r|s,a) [r+\gamma v_*(s')] \\

q_*(s, a) &=  \mathbb{E}\big[R_t + \underset{a}{max}\ \gamma q_*(S_{t+1}, a')\ |S_t=s, A_t=a\big] \\
&= \underset{a}{max} \sum_{s',r}p(s',r|s,a) [r+\gamma v_*(s')]

\end{align*}
$$
## Policy Evaluation

Policy evaluation for an arbitrary policy $\pi$ is computing its state-value function.

>[!quote] Numerical fixed-point iteration is a method of computing fixed points of a function. A fixed point is a value that doesn't change under transformation. Specifically for functions a fixed point is mapped to itself by the function.

We evaluate policy using iterative methods. We construct a sequence of approximations to value function starting at $v_0$ (chosen arbitrarily except any terminal state, if any, is given zero value ) and using Bellman Equation as an <span style="color:rgb(255, 0, 0)">update rule</span> to arrive at next element in the sequence.

$$
\begin{align*}
v_{k+1}(s) &= \mathbb{E}_\pi[R_{t+1} + \gamma v_k(S_{t+1})|S_t=s]\\
&= \sum_a\pi(a|s)\sum_{s',r}p(s',r|s, a)(r + \gamma v_{k}(s'))\\
\forall s \in S
\end{align*}
$$

>[!quote] Clearly $v_k = v_\pi$ is the fixed point for this update rule because Bellman equation for $v_\pi$ ensures the equality in this case.

The update done via above update rule is called expected update because it is expectation over all states.

Indeed the sequence $\{v_k\}$  can be shown in general to converge to $v_\pi$ as $k\rightarrow\infty$ under the same conditions that guarantee the existence of $v_\pi$. This algorithm is called <span style="color:rgb(255, 0, 0)">iterative policy evaluation.</span>

## Policy Improvement

Our reason for computing value function is to help find better policies. Suppose we have determined value function $v_\pi$ for an arbitrary policy $\pi$. For some state $s$ we want to know whether or not we should change the policy to deterministically choose an action $a\ne\pi(s)$. We know how good it is to follow current policy from $s$ that is $v_\pi$, but would it be better or worse to change to the new policy. One way to answer this question is to consider selecting $a$ in $s$ and thereafter following the existing policy $\pi$. The value of this way of behaving is

$$
\begin{align*}
q_\pi(s, a) &= \mathbb{E}_\pi[R_{t+1} + v_\pi(S_{t+1})|S_t=s, A_t=a]\\
&= \sum_{s,r}p(s',r|s,a)[r + \gamma v_\pi(s')]
\end{align*}
$$
The key criterion is whether it is greater than or less than $v_\pi(s)$. If it is greater--that is it is better to select $a$ once in $s$ then to follow $\pi$ every time, then it is better still to select $a$ every time we encounter $s$. 

That this is true is special case of a general result called<span style="color:rgb(146, 208, 80)"> policy improvement theorem</span>. Let $\pi$ and $\pi'$ be any pair of deterministic policies such that for all $s\in\mathcal{S}$ 

$$
q_\pi(s, \pi'(s)) \ge v_\pi(s)
$$
then 
$$
v_{\pi'}(s) \ge v_\pi(s) 
$$

Proof: We know that 
$$
q_\pi(s, \pi'(s)) = \mathbb{E}_\pi[R_{t+1} + \gamma v_{\pi}(s')]
$$

## Policy Iteration

## Value Iteration

## Asynchronous Dynamic Programming

## Generalized Policy Iteration

In GPI, one maintains both an approximate value function and approximate policy. The value function is repeatedly altered to more closely approximate the value function of current policy (policy evaluation)  and the policy is repeatedly improved (policy improvement) w.r.t current value function.
# Monte Carlo Methods

First learning method for estimating value functions and discovering optimal policies. Unlike DP we do not assume complete knowledge of the environment. Monte Carlo methods require only _experience_, sample sequences of states, actions and rewards from actual or simulated environment it doesn't require complete probability distributions of all possible transitions that is required for dynamic programming (DP)

Monte Carlo Methods are ways of solving reinforcement learning problem based on averaging sample returns.

>[!question] To ensure well defined returns are available, here we define Monte Carlo methods only for episodic tasks. That is we assume experience is divided into episodes, and that all episodes eventually terminate no matter what actions are selected.

Only on completion of episodes are value estimates and policies changed. Monte Carlo methods can thus be incremental in an episode by episode sense but not in step-by-step(online) case. 

Monte Carlo methods sample and average returns of each state-action pair.

>[!quote] Because all action selections are undergoing learning, the problem becomes non-stationary from the point of view of the earlier state. 

An important fact of MonteCarlo methods is that the estimates for each state are independent. The estimate for one state does not build upon the estimate of any other state. In other words, Monte Carlo methods do not bootstrap. In particular computational expense of estimating the value of a single state is independent of the number of states.

If model of the environment is not available then it is particular useful to estimate action values rather than state values. 

>[!quote] On-policy methods attempt to evaluate or improve policy that is used to make decisions where as off-policy methods evaluate or improve a policy different from that used to generate the data. 

The monte carlo methods discussed above is an example of an on-policy method. In on-policy control methods the policy is generally soft, meaning that $\pi(a|s)>0$ for all $s\in\mathcal{S}$ and all $a\in\mathcal{A}$, but gradually shifted closer and closer to deterministic optimal policy . 

$\epsilon$-greedy policies