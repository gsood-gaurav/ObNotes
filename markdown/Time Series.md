A time series model for the observed data ${x_t}$ is a specification of the joint distributions (or possibly only the means and covariances) of a sequence of random variables ${X_t}$ of which ${x_t}$ is postulated to be the realization.

>In general we shall lose a certian amount of information by looking at time series "through second order (mean and covraiance) spectacles", but the theory of mean squared error linear prediction depends only on the second order properties.

Smoothness of time series graph is generally indicative of the existence of some form of dependence among observation.
**Dependence is quantified using autocorrelation and stationary processes is a family of useful models exhibiting wide variety of dependence structures.**

## Stationary Models and the autocorrelation function
Loosely speaking a time series is said to be stationary if it has statistical properties similar to to those of time-shifted series. Restricting attention to those properties that depend only on the first and second order moments of generating distribution

>Definition Let ${\{X_t\}}$ be a time series with $E(X^2) < \infty$  The mean function of ${\{X_t\}}$ is $$\mu_X(t) = E(X_t)$$
>The covariance function of ${\{X_t\}}$ is $$\gamma_X(r, s) = Cov(X_r, X_s) = E[(X_r - \mu_X(r))(X_s - \mu_X(s))]$$ for all integers r and s


> ${\{X_t\}}$ is weakly stationary if
> (i) $\mu_X(t)$ is independent of $t$,
> and
> (ii) $\gamma_X(t+h, t)$ is independent of t for each h
> 

**Opinion: The term strict stationarity is used when all the random variables has same joint distributions. It is not restricted to first and second order moments only. Skewness and Kurtosis also comes into picture
**_Opinion: The idea behing weakly stationarity might be required for many purposes in time series analysis. In forecasting if we are trying to predict point forecast from a lagged point makes sense only if covarince depends only on lag not on actual t._**

Whenever we use the term covariance function with reference to a stationary time series $X_t$ we shall mean function $\gamma_X$ of one variable, defined by $$\gamma_X(h):=\gamma_X(h, 0) = \gamma_X(t+h, t)$$
The function $\gamma_X(.)$ will be referred to as the autocovariance function and $\gamma_X(h)$ as its value at lag _h_.
> Definition: Let ${\{X_t\}}$  be a stationary time series. The autocovariance function (ACVF) of ${\{X_t\}}$ at lag h is $$\gamma_X(h) = Cov(X_{t+h}, X_t)$$
> The autocorrelation function (ACF) of ${\{X_t\}}$ at lag h is $$\rho_X(h) \equiv \frac{\gamma_X(h)}{\gamma_x(0)} = Cor(X_{t+h}, X_t)$$

Time Series Analysis is to study the techniques for drawing inferences from such series. Before we can do this, however it is necessary to setup a hypothetical probability model to represent the data. After an appropiate family of models has been chosen, it is then possible to estimate parameters, check for goodness of fit to the data, and possibly to use the fitted model to enhance our understanding of the mechanism generating the series.

## Application of Time Series
- The model may be used simply to provide a compact description of the data in terms of trend, seasonality and random terms. For the interpretation of economic statistics such as unemployment figures, it is important to recognize the presence of seasonal component and to remove them so as not to confuse them with long-term trends. The process is known as seasonal adjustment.
- Filtering of noise from signals
- Prediction of future values
- Simulation studies
- Testing Hypothesis.

A Univariate time series is a ordered sequence of measurements of the same  variable collected over time. Most often measurements are made over regular intervals.
One difference from standard linear regression is that the data are not necessarily independent and not necessarily identically distributed.

There are various objectives for studying time series. They include understanding and description of the generating mechanism, the forecasting of future values and optimal control of a system. The intrinsic nature of time series is that its observations are dependent or correlated and order of observations is therefor important.

## Structural Time Series Models

A univariate economic time series model can be formulated directly in terms of the traditional components of **trends, seasonal, cycle and irregular**. A model if this kind is called structural time series model. The essence of structural models is that it is formulated in terms of independent components which have a direct interpretation in terms of quantities of interest.

## Basic Objective of Analysis

The basic objective to model a time series is as follows
- To describe important featuers of time series pattern
- To explain how past affects the future or how two time series can interact
- To forecast future value of the time series
## Types of Models
Two basic types of time domain models
- ARIMA
- Ordinary Regression Models
## Imp Characterstics to Consider First
- Is there a **Trend**
- Is there **Seasonality**
- Are there outliers
- Is there a long run cycle
- Is there constant variance over time
- Are there any abrupt changes to either the level of the series or the variance
If the data is collected annualy, by definition, there is no seasonality.
	
The predictability of an event or a quantity depends on several factors including

1. how well we understand the factors that contribute to it
2. how much data is available
3. how similar the future is to past
4. whether the forecasts can affect the thing we are trying to forecast

**Often in forecasting, a key step is knowing when someting can be forecast accurately and when forecasts will be no better than tossing a coin.**

**Many people wrongly assume that forecasts are not possible in a changing environment. Every environment is changing, and a good forecasting model captures the way in which things are changing. Forecasts rarely assume the environment is unchanging. What is normally assumed is that the way in which the environment is changing will continue into the future.**

## The statistical perspective

We will use the subscript $t$ for time. For example, $y_t$ will denote the observation at time $t$. Suppose we denote all the information we have observed as $I$ and we want to forecast $y_t$. We then write $y_t|I$ meaning "the random variable $y_t$ given what we know in $I$." The set of values that this random variable could take, along with their relative probabilites is knwos as the probability distribution of $y_t|I$ . In forecasting, we call this forecast distribution.

Since we are doing sampling with adjacent points in time we naturally introduce correlation into the system.

## Time Plots
First step in time series analysis is time plot.
We can see some trends.
Seasonal Effect on time series.
**If there are trends or sesonal effects in different parts of time series, it violates the stationarity principle.**

## Trend

A trend exists when there is a long-term increase or decrease in the data. It does not have to be linear. Sometimes we will refer to a trend as changing direction, when it might go from an increasing trend to a decreasing trend. 

## Seasonal

A seasonal pattern occurs when a time series is affected by seasonal factors such as _time of the year or day of the week_. Seasonality is always of a fixed and known period.

## Cycle

A _cycle_ occurs when the data exhibit rises and falls that are nof of a fixed frequency. These fluctuations are usually due to economic conditions and are often related to the "business cycle" The duration of these fluctuations is usually $2$ years.

> Many people confuse cyclic behavior with seasonal behavior, but they are really quite different. If the fluctuations are not of fixed frequency then they are cyclic; if the frequency in unchanging and associated with some aspect of the calendar, then the pattern is seasonal. In general average length of cycles is longer than the length of seasonal pattern, and the maginitudes of cycles tend to be more variable than the magnitudes of seasonal patterns.


## Stationary Time Series

A Time Series(TS) is said to be stationary if its statistical properties such as mean, variance remain constant over time.
- constant mean
- constant variance
- an autocovariance that doesnot depend upon time
makes a TS stationary. There are two major reasons behind non-stationarity of a TS
- **Trend**  varying mean over time.e.g we saw that on average, the number of passangers were growing over time.
- **Seasonality**  variations at specific time frames. people might have tendency to buy cars in a particular month because of pay increments or festivals.
- 
## Weak Stationarity Time Series
what we want in time series is stationarity i.e. we dont want to see a trend or systematic change. We dont want any peroidic fluctuations. The properties of one section of data are much like properties of other sections of the data.

For an non-stationary time series, we will do some transformations to get stationary series.

in weak stationarity time series there is no
- systematic change in mean (no trend)
- systematic change in variance
- periodic variations

## Autocovariance Functions

Time Series as a realization of a stochastic process.
Autocovarinace function depends on the time difference only. It is the outcome of our assumption of stationarity.

## Autocovariance Coefficients

## Random Walk

## Feature Engineering
- Time-step features model time dependence
- Lag features model serial dependence.

Adapting machine learning algorithms to time series problems is largely about feature engineering with the time index and lags.


