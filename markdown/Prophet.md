# Introduction
Completely automated techniques can be hard to tune and are often inflexible to incorporate useful assumptions or heuristics.

## Prophet Features

- Multiple Seasonality
- Changing growth rates
- Ability to model special days

## Introduction

We use a decomposable time series model with three main components trend, seasonality, holidays. They are combined in the following equation

$$y(t) = g(t) + s(t) + h(t) + \epsilon_t$$
$g(t)$ represents trend function which models non-preodic changes
$s(t)$ represents periodic changes
$h(t)$ represents the effects of holidays
$\epsilon_t$ represents any idiosyncratic changes which are not accomodated by model, **later we will make the parametric assumption that $\epsilon_t$ is normally distributed**. This specification is similar to GAM a class of regression models with potentially non-linear smoothers applied to the regressors. Here we use only time as regressor but possibly several linear and non-linear functions of time as components. **Modelling seasonality as an additive component is the same approach taken by exponential smoothing**. Multiplicative seasonality where the seasonal effect is a factor that multiplies $g(t )$, can be accomplished by a log transform.

> The GAM formulation has advantage that it decomposes easily and accomodates new components as necessary, for instance when a new source of seasonality is identified. GAMs also fit very quickly either using backfitting or L-BFGS so that users can interactively change parameters

We are in effect framing the forecasting problem as curve fitting exercise which is inherently different from time series models that explicitly account for the temporal dependence structure in the data.  While giving up some important inferential advantages of using generative model such as an ARIMA this formulation provides a number of practical advantages.

- Flexibility: We can easily accomodate seasonality with multiple periods and let analyst make different assumption about trends.
- Unlike ARIMA, the measurements do not need to be regulary spaced, and we do not need to interpolate missing values e.g. removing outliers.
- Fitting is very fast
- Forecasting model has easily interpretable parameters that can be changed by the analyst to impose assumptions on the forecast.

## Trend Model

We have implemented two trend models **satrurating growth model and piecewise linear model**

### Non Linear Saturating Growth

$$g(t) =  \frac{C}{1 + exp(-k(t-m))}$$
There are two important aspects that has not been captured in above equation.

- Carrying capacity is not constant
- Carrying capacity is time varying.
- 