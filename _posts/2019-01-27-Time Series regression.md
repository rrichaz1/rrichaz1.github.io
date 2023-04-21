The Linear regression models assume that experimental units and the error terms are independent of each other. In real life there are a lot of phenomena that are not truly independent. Stock market indexes, job data, sales data etc have experimental units that are time dependent. If an experimental unit is measured repeatedly over time, the units will show a pattern. The lecture referred to a few papers that describe the impact of time on health care data. It was fascinating to read about a study of the fetal health rate data collected as different stages of gestation. The heart rate at one instant of time is compared with the rate 6 seconds before. Starting at 24 weeks the correlation becomes more pronounced. 
Linear regression assumes that the data is independent and stationary i.e. the mean, variance etc. does not change over time. In order to model time series data, it is visualized as consistent of trend, seasonal and error components. When the seasonal and trend components are removed the dependency of past and present with future can be derived from the residual.

To run regression on time series data, we can find the auto-correlation, i.e. take measurement of the experimental unit at different points in time and then compare these to see if they are correlated. If we use only certain number of lags and find the correlation, it is called partial autocorrelation. Just like other probability distributions, time series data has a Durbin-Watson distribution that is used to do hypothesis testing.

Some other models are
1.	AutoRegressive (AR) – The autoregressive model specifies that the output variable depends linearly on its previous values and on a stochastic term
2.	Moving Average (MA) - The moving average model specifies that the output variable depends linearly on the current and various past values of a stochastic (imperfectly predictable) term. Rather than using the past values of the forecast variable in a regression, a moving average model uses past forecast errors in a regression-like model.
The descriptions sound very similar, so some searching on the internet gave the following 
“The primary difference between an AR and MA model is based on the correlation between time series objects at different time points. The covariance between x(t) and x(t-n) is zero for MA models. However, the correlation of x(t) and x(t-n) gradually declines with n becoming larger in the AR model. This means that the moving average(MA) model does not uses the past forecasts to predict the future values whereas it uses the errors from the past forecasts. While, the autoregressive model(AR) uses the past forecasts to predict future values.”

In real world a combination of these models are used. Some examples are ARMA and ARIMA . The Box Jenkins methodology uses a combination of the two. 
 





[https://en.wikipedia.org/wiki/Ergodic_process](https://en.wikipedia.org/wiki/Ergodic_process)
[https://pdfs.semanticscholar.org/4a00/ef846786fca7353ad00a4395fd9e1d5f87bf.pdf](https://pdfs.semanticscholar.org/4a00/ef846786fca7353ad00a4395fd9e1d5f87bf.pdf)
[https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4941839/](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC4941839/)
[https://discuss.analyticsvidhya.com/t/what-is-the-difference-between-ar-and-ma-time-series-models/2131/3](https://discuss.analyticsvidhya.com/t/what-is-the-difference-between-ar-and-ma-time-series-models/2131/3)
