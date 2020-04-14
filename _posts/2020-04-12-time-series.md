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


# Correlation 

To compute the correlation between two time series, we can use the `.corr()` method of `pandas.Series`. 

To visualize the scatter plot of two time series: 

```python
def correlation_between_2_ts(s1, s2, figsize=(5, 5), plot_scatter=True):
    """
    Computes correlation between two time series
    
    s1, s2: named pandas.Series 
    """
    correlation = s1.corr(s2)
    if plot_scatter:
        plt.figure(figsize=figsize)
        plt.scatter(s1, s2)
        plt.grid()
        title = "Scatter plot of {} and {}".format(s1.name, s2.name) 
        title += "\ncorrelation = {:.4f}".format(correlation)
        plt.title(title) 
        plt.show()
    return correlation

correlation = correlation_between_2_ts(s1, s2)
```

# Autocorrelation function (ACF)

The autocorrelation as a function of the lag. It equals one at lag-zero. 

```python
from statsmodels.tsa.stattools import acf

acf(data)
```

```python
from statsmodels.graphics.tsaplots import plot_acf

plot_acf(data, alpha=0.05, lags=30)
plt.show()
```

To compute a single lag-N autocorrelation, we can also use the `.autocorr(lag=N)` method of `pandas.Series`. 




# Stationarity


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

```python
gaussian_white_noise = np.random.normal(loc=0.02, scale=0.05, size=1000)
```

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


```python
from statsmodels.tsa.stattools import adfuller

# p-value
adfuller(p1)[1]
```


# Autoregressive model (AR model)

AR model of order 1, or simply AR(1) model (there is only one lagged value on right hand side):

$$X_t = \mu + \phi X_{t-1} + \epsilon_t$$

If AR parameter $\phi = 1$, then this is a random walk. If $\phi = 0$, then this is white noise. 

In order for the process to be stable and stationary, $\phi$ has to be $- 1 < \phi < 1$. 

Interpretation of AR(1) parameter:

* negative $\phi$: mean reversion 
* positive $\phi$: momentum. 
* the autocorrelation function decays exponentially for an AR(1) time series at a rate of the AR(1) parameter $\phi$. 


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


# Moving average model (MA model)

MA model of order 1, or simply MA(1) model (there is only one lagged error on right hand side):

$$X_t = \mu + \epsilon_t + \theta \epsilon_{t-1}$$

If MA parameter $\theta = 0$, then this is white noise. 

MA models are stationary for all values of $\theta$. 

Interpretation of MA(1) parameter: 

* negative $\theta$: one-period mean reversion
* positive $\theta$: one-period momentum 
* one-period autocorrelation (lag-1 autocorrelation) is not $\theta$, it is $\frac{\theta}{1 + \theta^2}$. There is zero autocorrelation for an MA(1) beyond lag-1. 
* higher frequency stock data is well modeled by an MA(1) process. For example, one day's prices (on September 1, 2017) for Sprint stock (ticker symbol "S") sampled at a frequency of one minute. The stock market is open for 6.5 hours (390 minutes), from 9:30am to 4:00pm. Such data can be accessed via Google Finance [3]. Stocks trade at discrete one-cent increments (although a small percentage of trades occur in between the one-cent increments) rather than at continuous prices, and when we plot the data we should observe that there are long periods when the stock bounces back and forth over a one cent range. This is sometimes referred to as "bid/ask bounce". The bouncing of the stock price between bid and ask induces a negative first order autocorrelation, but no autocorrelations at lags higher than 1. 


The model can be extended to include more lagged errors and more $\theta$ parameters:

* AR(1): $X_t = \mu + \epsilon_t + \theta_1 \epsilon_{t-1}$
* AR(2): $X_t = \mu + \epsilon_t + \theta_1 \epsilon_{t-1} + \theta_2 \epsilon_{t-2}$
* etc. 

An MA(q) model has no autocorrelation beyond lag-q. 

To simulate MA time series, take care of the convention: we must include the zero-lag coefficient of 1. However, unlike with the AR simulation, we don't need to reverse the sign of $\theta$, its sign is what we have been using above. 

```python
from statsmodels.tsa.arima_process import ArmaProcess

# theta = + 0.9
ar = [1]
ma = [1, 0.9]
arma_process = ArmaProcess(ar, ma)
simulated_data = arma_process.generate_sample(nsample=1000)

# theta = - 0.9
ar = [1]
ma = [1, - 0.9]
arma_process = ArmaProcess(ar, ma)
simulated_data = arma_process.generate_sample(nsample=1000)
```

To estimate an MA model (estimate parameters from data):

```python
from statsmodels.tsa.arima_model import ARMA

# Fit an MA(1) model to the data, true theta = + 0.9
arma = ARMA(data, order=(0, 1))
arma_results = arma.fit()

print(arma_results.summary())
```

```
                              ARMA Model Results                              
==============================================================================
Dep. Variable:                      y   No. Observations:                 1000
Model:                     ARMA(0, 1)   Log Likelihood               -1404.378
Method:                       css-mle   S.D. of innovations              0.985
Date:                Mon, 13 Apr 2020   AIC                           2814.756
Time:                        16:10:50   BIC                           2829.479
Sample:                             0   HQIC                          2820.352
                                                                              
==============================================================================
                 coef    std err          z      P>|z|      [0.025      0.975]
------------------------------------------------------------------------------
const         -0.0664      0.060     -1.112      0.266      -0.184       0.051
ma.L1.y        0.9203      0.012     75.882      0.000       0.896       0.944
                                    Roots                                    
=============================================================================
                  Real          Imaginary           Modulus         Frequency
-----------------------------------------------------------------------------
MA.1           -1.0867           +0.0000j            1.0867            0.5000
-----------------------------------------------------------------------------
```

Just as with AR models, we can use MA models to do forecasting, both in-sample and out-of-sample using `statsmodels`. This can be done via either the `predict()` method if we want the forecasts in the form of a series of data, or the `plot_predict()` method if we want a plot of the forecasted data. One big difference between out-of-sample forecasts with an MA(1) model and an AR(1) model is that the MA(1) forecasts more than one period in the future are simply the mean of the sample. 


```python
# Plot the original series and the forecasted series
arma_results.plot_predict(start=0, end="2030")
plt.show()
```

# Autoregressive moving average model (ARMA model)


An ARMA model is a combination of an AR model and an MA model. 

ARMA(1, 1) model:

$$X_t = \mu + \phi X_{t-1} + \epsilon_t + \theta \epsilon_{t-1}$$

ARMA models are generally denoted ARMA(p, q) where parameters p and q are non-negative integers, p is the order of the AR model, q is the order of the MA model. 

ARMA models can be converted to pure AR or pure MA models. Here is an example of converting an AR(1) model into an an MA($\infty$): 

$$X_t = \mu + \phi X_{t-1} + \epsilon_t$$

$$X_t = \mu + \phi (\mu + \phi X_{t-2} + \epsilon_{t-1}) + \epsilon_t$$

$$X_t = \frac{\mu}{1-\phi} + \epsilon_t + \phi \epsilon_{t-1} + \phi^2 \epsilon_{t-2} + \phi^3 \epsilon_{t-3} + ...$$

This demonstrates that an AR(1) model is equivalent to an MA($\infty$) model with the appropriate parameters. 


# Cointegration model 

The idea behind cointegration (协整) is that even if the prices of two different assets both follow random walks, it is still possible that a linear combination of them is not a random walk. If that's true, then even though these two assets are not forecastable because they are random walks, the linear combination is forecastable. We say that these two assets are cointegrated. One analogy is that a dog owner walking his dog with a retractable leash. The position of the dog owner and the position of the dog may both follow random walks, but the distance between them may very well be mean reverting. Examples can be found by looking at economic substitutes: heating oil and natural gas, platinum and palladium, corn and wheat, corn and sugar, Bitcoin and Ethereum, etc. For stocks, a natural starting point for identifying cointegrated pairs are stocks in the same industry. However competitors are not necessarily economic substitutes, think of Apple and Blackberry. 

Two steps to test for cointegration:

* regress the level of one series $P_t$ on the level of the other series $Q_t$ to get the slope coefficient $c$ or the cointegration vector (coefficients of the linear combination). 
* run Augmented Dickey-Fuller test on $P_t - c Q_t$ or on the residuals of the regression. 

Alternatively, `statsmodels` has a function `coint` that combines both steps, its null hypothesis is no cointegration. 

```python
from statsmodels.tsa.stattools import coint

# p-value
coint(s1, s2)[1]
```

# Autoregressive integrated moving average model (ARIMA model)


An ARIMA model is a generalization of an ARMA model. ARIMA models are applied in some cases where data show evidence of non-stationarity, where an initial differencing step (corresponding to the "integrated" part of the model) can be applied one or more times to eliminate the non-stationarity. 

ARIMA models are generally denoted ARIMA(p, d, q) where parameters p, d, and q are non-negative integers, p is the order of the AR model, d is the degree of differencing, q is the order of the MA model. 


Using the ARIMA module on a random walk series is identical to using the ARMA module on the first-order difference of that series followed by taking cumulative sums of these differences to get the original series forecast. 


```python
from statsmodels.tsa.arima_model import ARIMA

arima = ARIMA(data, order=(1,1,1))
arima_results = arima.fit()

arima_results.plot_predict(start="1872-01-01", end="2046-01-01")
plt.show()
```


In terms of forecasting, sometimes the estimate of the drift will have a much bigger impact on long range forecasts than the ARMA parameters. 


# Machine learning for time series

Unpivot a DataFrame from wide to long format (melt):

```python
df = data.melt(id_vars="Product_Code", var_name="Week", value_name="Sales")
```

```
              W0  W1  W2  W3  W4  W5  W6  W7  W8  W9  ...  W42  W43  W44  W45  \
Product_Code                                          ...                       
P1            11  12  10   8  13  12  14  21   6  14  ...    4    7    8   10   
P2             7   6   3   2   7   1   6   3   3   3  ...    2    4    5    1   
P3             7  11   8   9  10   8   7  13  12   6  ...    6   14    5    5   
```

```
                   Sales
Product_Code Week       
P1           0        11
             1        12
             2        10
             3         8
             4        13
...                  ...
P99          47        8
```

Adding lags as basic feature engineering:

```python
def add_lag(original_df, lag=3, groupby_col="Product_Code", col="Sales", diff=False, dropna=True):
    df = original_df.copy()
    columns = []
    for i in range(1, lag + 1):
        c = "lag_" + str(i)
        columns.append(c)
        df[c] = df.groupby(groupby_col)[col].shift(i)
    if diff: # pay attention for multicollinearity
        for i in range(1, lag + 1):
            c = "diff_" + str(i)
            columns.append(c)
            df[c] = df.groupby(groupby_col)["lag_" + str(i)].diff(1)
    if dropna:
        df.dropna(inplace=True, axis=0, how="any")
        df[columns] = df[columns].astype("int")
    return df
    
df = add_lag(df, 3)
```

Time series cross validation:

```python
from sklearn.model_selection import TimeSeriesSplit

def split_test_ts(X, y, test_size=1):
    """
    X: pd.DataFrame
    y: pd.Series
    
    reserves the last test_size elements of the time series dataset 
    as the test set of the time series problem. 
    """
    assert test_size > 0, "test_size must be larger than 0."
    X_tmp, X_test = X.iloc[: - test_size, :], X.iloc[- test_size :, :]
    y_tmp, y_test = y.iloc[: - test_size], y.iloc[- test_size :]
    return X_tmp, X_test, y_tmp, y_test 

def split_train_validation_ts(X, y, n_splits=3, max_train_size=None):
    """
    X: pd.DataFrame
    y: pd.Series
    
    returns a generator that generates training sets and 
    validation sets for time series cross validation. 
    
    If a separate test set is needed, call split_test_time_series() 
    before calling this function. 
    """
    tss = TimeSeriesSplit(n_splits=n_splits, max_train_size=max_train_size)
    for train_idx, validation_idx in tss.split(X):
        X_train, X_validation = X.iloc[train_idx, :], X.iloc[validation_idx, :]
        y_train, y_validation = y.iloc[train_idx], y.iloc[validation_idx]
        yield X_train, X_validation, y_train, y_validation 
        
def get_dataset_with_specific_lag(df, lag, target="Sales", test_size=3600):
    df = add_lag(df, lag)
    y = df.loc[:, target]
    X = df.drop(target, axis=1)
    X_train, X_test, y_train, y_test = split_test_ts(X, y, test_size=test_size)
    return X_train, X_test, y_train, y_test
```

```python
X, X_test, y, y_test = split_test_ts(X, y, test_size=3600)

train_validation_generator = split_train_validation_ts(X, y, n_splits=10)
for X_train, X_validation, y_train, y_validation in train_validation_generator:
    pass 
```







# References


[1] Https://plus.google.com/u/0/+Datacamp/. (n.d.). Sign in. DataCamp. https://learn.datacamp.com/courses/time-series-analysis-in-python 

[2] E. E. Holmes, M. D. Scheuerell, and E. J. Ward. (2020, February 3). 5.3 Dickey-Fuller and augmented Dickey-Fuller tests - Applied time series analysis for fisheries and environmental sciences. NWFSC Time-Series Analysis. https://nwfsc-timeseries.github.io/atsa-labs/sec-boxjenkins-aug-dickey-fuller.html 

[3] 6 ways to download free intraday and tick data for the U.S. stock market. (n.d.). QuantShare Trading Software. https://www.quantshare.com/sa-426-6-ways-to-download-free-intraday-and-tick-data-for-the-us-stock-market 

[4] Autoregressive integrated moving average. (2005, February 15). Wikipedia, the free encyclopedia. Retrieved April 14, 2020, from https://en.wikipedia.org/wiki/Autoregressive_integrated_moving_average 



































