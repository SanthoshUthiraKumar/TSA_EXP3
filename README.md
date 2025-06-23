## Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv('XAUUSD_2010-2023.csv')

time_series = data['close']

# Ensure the sales data is numeric (handling any formatting issues)
time_series = pd.to_numeric(time_series, errors='coerce').dropna()

# Calculate the number of data points and lags
n_data_points = len(time_series)
n_lags = min(35, n_data_points - 1)
acf_values = np.zeros(n_lags)

# Calculate the mean and variance of the time series data
mean = np.mean(time_series)
variance = np.var(time_series)
normalized_data = time_series - mean 

# Compute the ACF manually
for lag in range(n_lags):
    lagged_data = np.roll(normalized_data, -lag)
    acf_values[lag] = np.sum(normalized_data[:n_data_points-lag] * lagged_data[:n_data_points-lag]) / (variance * (n_data_points - lag))

# Plot the ACF results with blue stems and red markers
plt.figure(figsize=(10, 6))
plt.stem(range(n_lags), acf_values, linefmt='b-', markerfmt='ro', basefmt='k-', use_line_collection=True)
plt.title('ACF Plot for Close Prices')
plt.xlabel('Lag')
plt.ylabel('ACF')
plt.grid(True)
plt.show()

```
### OUTPUT:
![image](https://github.com/user-attachments/assets/81557d9f-623e-43a7-966d-904744f743c4)

### RESULT:
Thus we have successfully implemented the auto correlation function in python.
