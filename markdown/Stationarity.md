Stationary time series is important because if a time series is non-stationary, we can study its behavior only for the time period under consideration. Each set of time series data will be a particular episode. As consequence it is not possible to generalize it to other time periods. Thus the purpose of forecasting such time series may be of little practical value.

If the series has a long running trend and tend to reverts to trend line following a disturbance it may be possible to stationarize it by de-trending (e.g. by fitting a trend line and subtracting it out prior to fitting a model or else by including the time index as an independent variable in a regression or ARIMA model.) Such a series is called **trend stationary**. However, sometimes even de-trending is not sufficient to make the series stationary, in which case it may be necessary to transform it into as series of period-to-period and/or season-to-season differences. If the mean, variance and autocorrelations of the original series are not constant in time, even after detredning, perhaps the statistics of the changes in the series between periods or between seasons will be constant. Such as series is said to be **difference stationary**. 

The first difference of a time series is the series of changes from one period to the next. if $Y_t$ denotes the value of time series $Y$ at period $t$, then the first difference of $Y$ at period $t$ is equal to $Y_t-Y_{t-1}$. If the first difference of $Y$ is stationary and also completely random (not autocorrelated) then Y is described by a random walk model. If the difference of $Y$ is stationary but not completely random i.e. the value at period $t$ is autocorrelated with its value at earlier periods then a more sophisticated forecasting model such as exponential smoothing or ARIMA may be appropriate.

## Strong Stationarity

$X$ is a strongly stationary process if its distributions satisfy the following properties

$$
\mathbb{P}(X_1,X_2,\cdots,X_T) = \mathbb{P}(X_{1+\tau},X_{2+\tau},\cdots,X_{T+\tau}) \forall T, \tau\in\mathbb{N}^*
$$
Stationarity means that the distribution of $X$ is the same over time or in other words that it is invariant to any time shift. **In particular any i.i.d stochastic process is strongly stationary.** In practice it is difficult to test above property. Thus a weak version of stationarity named **weak stationarity**  is introduced.

## Weak Stationarity

$X$ is weakly stationary (or mean covariance stationary) process if its mean and covariance verify the following properties

$$
\begin{align*}
\mathbb{E}[X_t] &= \mu \ (mean stationarity) \\
Cov(X_t, X_{t+h}) &= \gamma(h) \implies Var(X_t) = \gamma(0) \lt \infty (covariance\ stationarity)
\end{align*}
$$
## Test for Stationarity

- Graphical Methods
- Statistical Tests