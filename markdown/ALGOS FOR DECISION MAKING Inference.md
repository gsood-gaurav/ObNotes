In inference problems we want to infer distribution over query variables given some observed variables (evidence variables). The other nodes are referred to as hidden variables. We often refer to distribution over query variables given evidence variables as *posterior distribution.*

The process of using definition of conditional probability distribution, marginalisation and applying the chain rule can be used to perform exact inference in any Bayesian Network.

We can implement exact inference using factors.

# Sequential Decision Making

Discount factor makes it so that the rewards in the present are worth more than rewards in the future, a concept that also appears in economics.

_In an MDP, an optimal deterministic policy always exist._



>[!note] We focus on stationary MDPs where $P(S_{t+1}|S_t, A_t), P(R|S_t, A_t)$ don't vary with time. In infinite horizon problems with stationary transitions and rewards we can further restrict our attention to stationary policies, which donot depend upon time. We will write the action associated with stationary policy $\pi$ in state $s$ as $\pi(s)$, without the temporal subscript. In finite horizon problems, however it is benefical to select a different action depending upon how many time steps are remaining. For example while playing a basketball game, it is generally not a good stratgey to play a half-court shot unless there are only couple of seconds remaining in the game. We can make stationary policies account for time by incorporating time as state variable.




