# Exploring Different Time Series Models

We explore different time series models using data from the National Oceanic and Atmospheric Administration (NOAA). The data shows records on snow depth, precipitation, snowfall etc  from one of the testing locations in South Dakota from 1990-01-01 to 2012-12-31. We chose the maximum temperature variable to perform a univariate time series analysis since that had a few missing records as compared to the other five numeric variables. Out of the 8035 days within this period, the data only has 7763 records. 

We examined the missing records and found the missigness to be due to randomness. To impute the missing records, we relied on the Missing Value Imputation by Kalman Smoothing and State Space Models (na_kalman) function within the imputeTS library. This is an algorithm for estimating a missing time series value based on available data up to time, t via the Kalman filter. The Kalman filter relies on a series of mathematical models to estimate the next missing series as $x_{t+1} = Ta_t + K_t(y_t - Za_t)$.  

We begin the analysis by looking at the time series plot of the maximum temperature series(has 8035 records now). The series reveals an erratic pattern throughout the years, a behavior that is common to temperature series. The erratic pattern is due to the seasonal effect in the series.  The time series plot does not reveal any increasing trend. The results can be seen in the decomposition plot. 
 
The first model we considered is the harmonic model. We fitted an initial harmonic model with 6 cycles to the series. A harmonic model is able to account for smooth variation in the seasonal effects. A t-ratio at an approximate 5% significant level was used to identify terms with significant coefficients. We defined significant coefficients as having magnitudes of the t-ratio to be at least 3. Eight terms were identified to have significant coefficients. We fitted a new model with only the significant terms. The new harmonic model had a lower Akaike information criterion(AIC) compared to the initial harmonic model. 

The next model we considered is the auto regressive moving average (ARMA) model.  The best-fitting ARMA$\Large{(p, q)}$ is chosen using the smallest AIC by trying a range of combinations of p and q in the arima function with the help of a for loop. The best ARMA model was identified to have $\Large{p, q= 2}$. The correlogram of the residuals of the ARMA $(2, 0, 2)$ model were identified to be a realization of white noise. The correlogram of the residuals squared showed similar results.


