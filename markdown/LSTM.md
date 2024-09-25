- Parameter Sharing
- Recursive structure

$$
\begin{align*}
h^{(t)} &= g^{(t)}(x^{(t)}, x^{(t-1)}...x^{(1)})\tag{1}\\
&= f(h^{(t-1)}, x^{(t)}; \theta)\tag{2}
\end{align*}
$$

- $1$ formulates the unrolled recurrence with separate functions `g(t)` learnt for each time steps
- $2$ formulates the unrolled recurrence with parameter sharing, a common function parameterized by $\theta$   applied at each time step.
- Each layer of LSTM introduces a set of parameters $W$, $U$, $V$, specifying hidden to hidden connection, hidden to input connection and hidden to output connection 
$$
\begin{align*}
a^{(t)} &= b+Wh^{(t-1)} + Ux^{(t)}\\
h^{(t)} &= tanh(a^{(t)})\\
o^{(t)} &= c + Vh^{(t)}
\end{align*}
$$
$$
\begin{align*} \  
i_t = \sigma(W_{ii} x_t + b_{ii} + W_{hi} h_{t-1} + b_{hi}) \\  
f_t = \sigma(W_{if} x_t + b_{if} + W_{hf} h_{t-1} + b_{hf}) \\ 
g_t = \tanh(W_{ig} x_t + b_{ig} + W_{hg} h_{t-1} + b_{hg}) \\
o_t = \sigma(W_{io} x_t + b_{io} + W_{ho} h_{t-1} + b_{ho}) \\  
c_t = f_t \odot c_{t-1} + i_t \odot g_t \\
h_t = o_t \odot \tanh(c_t) \\
\end{align*}
$$
