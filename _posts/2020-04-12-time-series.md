---
layout: post
category: Mathematics
title: Time series 
tagline: by SunHaozhe
tags: 
  - Mathematics
  - Machine learning
  - Python
  - Pandas
  - API
mathjax: true
comments: true
published: true
---


# Autocorrelation function (ACF)

The autocorrelation as a function of the lag. It equals one at lag-zero. 



# Stationarity

There are different ways to define stationarity:

* **Strong stationarity**: joint distribution of the observations is time-invariant.
* **Weak stationarity**: mean, variance and autocorrelation of the observations are time-invariant. For autocorrelation, $\text{corr}(X_t, X_{t-\tau})$ is only a function of $\tau$, not $t$. 
* Weak stationarity is easier to test than strong stationarity. 
* If a process is not stationary, it becomes difficult to model. Modeling involves estimating a set of parameters. If a process is not stationary and the parameters are different at each point in time, then there are too many parameters to estimate (maybe more parameters than data). 
* A random walk is a common type of non-stationary series, its variance grows with time. Seasonal series are also non-stationary, for example, its mean varies with time. A white noise series with varying mean is non-stationary.  
* A white noise series (with constant mean and variance) is stationary. 
* Many non-stationary series can be made stationary through a simple transformation. For example, if we take the differences (with a lag of 1) of a random walk series, we get a white noise series. A seasonal series can be made stationary by seasonal adjustments (taking the difference with a lag corresponding to the periodicity). Most economic data published by the government is seasonally adjusted. Sometimes, we may need more than one transformations, for a series that grows exponentially and shows a strong seasonal pattern, we can first take the log of the series to eliminate the exponential growth and then a seasonal difference. 

### White noise 

White noise is a series with:

* constant mean
* constant variance
* zero autocorrelations at all lags
* special case: if data has normal distribution, then Gaussian white noise

### Random walk

$$X_t = X_{t-1} + \epsilon_t$$

In other words, the change is white noise:

$$X_t - X_{t-1} = \epsilon_t$$

One cannot forecast a random walk, the best forecast for the next value is the current value. 

An extension, random walk with drift:

$$X_t = \mu + X_{t-1} + \epsilon_t$$

$$X_t - X_{t-1} = \mu + \epsilon_t$$ 


# Augmented Dickey-Fuller test


The Dickey-Fuller test is the following: 

$$X_t = \mu + \phi X_{t-1} + \epsilon_t$$

Null hypothesis: $H_0 : \phi = 1$

This is equivalent to:

$$X_t - X_{t-1} = \mu + \phi X_{t-1} + \epsilon_t$$ 

Null hypothesis: $H_0 : \phi = 0$

If we add more lagged changes on the right hand side, it's the Augmented Dickey-Fuller test.

The null hypothesis for both Dickey-Fuller test and Augmented Dickey-Fuller test is that the data are non-stationary. 

If we use 5% as the threshold, a p-value less than 5% indicates that:

* we can reject the null hypothesis that the series is non-stationary with 95% confidence.
* this series is stationary.

If we use 5% as the threshold, a p-value larger than 5% indicates that:

* we cannot reject the null hypothesis. 
* this series is non-stationary. 


# Autoregressive model (AR model)

AR model of order 1, or simply AR(1) model (there is only one lagged value on right hand side):

$$X_t = \mu + \phi X_{t-1} + \epsilon_t$$

If AR parameter $\phi = 1$, then this is a random walk. If $\phi = 0$, then this is white noise. 

In order for the process to be stable and stationary, $\phi$ has to be $- 1 < \phi < 1$. 

Negative $\phi$: mean reversion. Positive $\phi$: momentum. The autocorrelation function decays exponentially for an AR time series at a rate of the AR parameter $\phi$. 


The model can be extended to include more lagged values and more $\phi$ parameters:

* AR(1): $X_t = \mu + \phi_1 X_{t-1} + \epsilon_t$
* AR(2): $X_t = \mu + \phi_1 X_{t-1} + \phi_2 X_{t-2} + \epsilon_t$
* etc. 

To simulate AR time series, take care of the convention: we must include the zero-lag coefficient of 1 and the sign of the other coefficients is opposite what we have been using above. 

```python
from statsmodels.tsa.arima_process import ArmaProcess

# phi = + 0.9
ar = [1, - 0.9]
ma = [1]
arma_process = ArmaProcess(ar, ma)
simulated_data = arma_process.generate_sample(nsample=1000)

# phi = - 0.9
ar = [1, 0.9]
ma = [1]
arma_process = ArmaProcess(ar, ma)
simulated_data = arma_process.generate_sample(nsample=1000)
```


To estimate an AR model (estimate parameters from data):

```python
from statsmodels.tsa.arima_model import ARMA

# Fit an AR(1) model to the data, true phi = + 0.9
arma = ARMA(data, order=(1, 0))
arma_results = arma.fit()

print(arma_results.summary())
```

```
                              ARMA Model Results                              
==============================================================================
Dep. Variable:                      y   No. Observations:                 1000
Model:                     ARMA(1, 0)   Log Likelihood               -1455.318
Method:                       css-mle   S.D. of innovations              1.036
Date:                Sun, 12 Apr 2020   AIC                           2916.636
Time:                        20:45:48   BIC                           2931.360
Sample:                             0   HQIC                          2922.232
                                                                              
==============================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------
const         -0.0938      0.323     -0.290      0.772      -0.727       0.540
ar.L1.y        0.8995      0.014     65.170      0.000       0.872       0.927
                                    Roots                                    
=============================================================================
                  Real          Imaginary           Modulus         Frequency
-----------------------------------------------------------------------------
AR.1            1.1117           +0.0000j            1.1117            0.0000
-----------------------------------------------------------------------------

```

We can do forecasting, both in-sample and out-of-sample using `statsmodels`. The in-sample is a forecast of the next data point using the data up to that point, and the out-of-sample forecasts any number of data points in the future. These forecasts can be made using either the `predict()` method if we want the forecasts in the form of a series of data, or using the `plot_predict()` method if we want a plot of the forecasted data. We supply the starting point for forecasting and the ending point, which can be any number of data points after the data set ends. `plot_predict()` also gives confidence intervals around the out-of-sample forecasts. 


```python
# Plot the original series and the forecasted series
arma_results.plot_predict(start=0, end="2030")
plt.show()
```


To identify the order of an AR model:

* **Partial autocorrelation function (PACF)** meansures the incremental benefit of adding another lag. Each coefficient of PACF represents how significant adding the corresponding lag when we already have all the previous lags included. 
* **Information criteria** computes the goodness-of-fit with the estimated parameters, but apply a penalty function on the number of parameters in the model. In general, the more parameters in a model, the better the model will fit the data. But this can lead to overfitting. There are two popular information criteria: 
    * AIC (Akaike Information Criterion)
    * BIC (Bayesian Information Criterion)

In practice, the way to use the information criteria is to fit several models, each with a different number of parameters, and choose the one with the lowest information criteria.

```python
from statsmodels.graphics.tsaplots import plot_pacf

plot_pacf(data, lags=20)
plt.show()
```

```python
from statsmodels.tsa.arima_model import ARMA

bic = []
range_ = range(1, 7)
for p in range_:
    arma = ARMA(simulated_data, order=(p, 0))
    arma_results = arma.fit()  
    bic.append(arma_results.bic)

plt.plot(range_, bic, marker="o")
plt.xlabel("Order of AR Model")
plt.ylabel("BIC")
plt.show()
```








# References


[1] Https://plus.google.com/u/0/+Datacamp/. (n.d.). Sign in. DataCamp. https://learn.datacamp.com/courses/time-series-analysis-in-python 

[2] E. E. Holmes, M. D. Scheuerell, and E. J. Ward. (2020, February 3). 5.3 Dickey-Fuller and augmented Dickey-Fuller tests | Applied time series analysis for fisheries and environmental sciences. NWFSC Time-Series Analysis. https://nwfsc-timeseries.github.io/atsa-labs/sec-boxjenkins-aug-dickey-fuller.html 



































