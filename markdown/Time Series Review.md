#arXiv

PaperId: 2104.00164v2

Time Series decomposition is major preprocessing task, to separate non-stationary effects (deterministic components) from the remaining stochastic constituents, assumed to be stationary. The deterministic components are predictable and contribute to prediction through estimation or extrapolation. Fitting most appropriate model to remaining stochastic component aims at capturing the relationship between past and future values, to allow prediction.

In any domain involving temporal measurements via sensors, censuses, transaction records, the capture of a sequence of observations indexed by time stamps first allow to provide insights on the past evolution of some measurable quantity. Beyond this goal, the pervasiveness of time series has generated an increasing demand for performing various tasks on time series data(visualization, discovery of recurrent patterns, correlation discovery, classification, clustering, outlier detection, segmentation, forecasting, data simulation)

Temporal visualization should be first step before starting with time series modelling, whatever the downstream task should be.

A time series is a sequence of data points (observations) ordered in time. A time series represents the temporal evolution of a dynamic system that one searches to describe, explain and predict. Correlation analysis allows to model how a time series is related to its delayed values. This analysis is crucial to design a forecasting procedure, a major aim of time series data processing. Forecasting is based on the following principle: knowing the past behaviors of a system, it is possible to make previsions on its nearby or long term behaviors.

Let $x=x_1,x_2,\cdots,x_T$ be a time series describing a dynamic system of interest; $x$ is realization of the stochastic process $X={X_1,X_2,\cdots}=\{X\}_{t=1}^\infty$. Prediction requires the modeling of the relationship between past and future values of the system
$$
X_t = f(t, X_{t-1},X{t-1},\cdots)+g(t, X_{t-1},X{t-1},\cdots)\epsilon_t
$$
where $\{\epsilon_t\}$ is a series of noises such that the $\epsilon_t$ 's are i.i.d with 0 mean and unit variance, and also independent of past values of $X_t$ and where $f$ and $g$ are respectively the conditional mean and variance of $X_t$(given the past values). The conditional mean and variance are possibly time-dependent. The key to prediction in time series is the ability to model the dependencies between current and lagged values (defined as autocorrelation)
**In what follows $h$ designates $f$ or $g$.** To model $h$ there are two main categories of approaches parametric and nonparametric models.
It is possible to use a parametric model for $f$ and non parametric model for $g$ and vice-versa.
This survey talks about **linear** and **nonlinear** parametric model. In this survey we will decrypt link between linearity and stationarity and under which conditions they hold for some of the linear models presented.

## Stationarity

