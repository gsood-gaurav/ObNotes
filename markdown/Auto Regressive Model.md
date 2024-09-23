Contrary to moving average model , the AR model is not always stationary as it may contain unit root.

The notation of $AR(p)$ $$X_t = \sum_{i=1}^{p}\varphi_iX_{t-1}+\epsilon_t$$
where $\varphi_1, \varphi_2,...,\varphi_p$ are parameters of the model and $\epsilon_t$ is **white noise**
Some parameter constrains are necessary for the model to remain weak-sense stationary. For example,processes in the AR(1) model with $|\varphi_1|\ge1$ are not stationary.  More generally for an $AR(p)$ to be weak-sense stationary, the roots of the polynomial $\varphi(z):=1-\sum_{i=1}^p\varphi_iz^i$ must lie outside the unit circle, each complex root $z_i$ must statisfy $|z_i|\gt1$  