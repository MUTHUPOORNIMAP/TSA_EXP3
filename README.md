# Ex.No: 03   COMPUTE THE AUTO FUNCTION(ACF)
Date: 30-10-2026

### AIM:
To Compute the AutoCorrelation Function (ACF) of the data for the first 35 lags to determine the model
type to fit the data.
### DATASET USED:
BMW SALES DATASET.
### SOFTWARE USED:
GOOGLE NOTEBOOK
### ALGORITHM:
1. Import the necessary packages
2. Find the mean, variance and then implement normalization for the data.
3. Implement the correlation using necessary logic and obtain the results
4. Store the results in an array
5. Represent the result in graphical representation as given below.
### PROGRAM:
```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

# Load CSV dataset
data = pd.read_csv('/content/BMW_Car_Sales_Classification.csv')

# Get Sales Volume values
data = data['Sales_Volume'].dropna().values

N = len(data)

lags = range(35)

# Pre-allocate autocorrelation table
autocorr_values = []

# Mean
mean_data = np.mean(data)

# Variance
variance_data = np.var(data)

# Normalized data
normalized_data = (data - mean_data) / np.sqrt(variance_data)

# Go through lag components one-by-one
for lag in lags:
    if lag == 0:
        autocorr_values.append(1)
    else:
        auto_cov = np.sum(
            (data[:-lag] - mean_data) *
            (data[lag:] - mean_data)
        ) / N

        autocorr_values.append(auto_cov / variance_data)

# Display the graph
plt.figure(figsize=(10, 6))
plt.stem(lags, autocorr_values)

plt.title('Autocorrelation of BMW Sales Data')
plt.xlabel('Lag')
plt.ylabel('Autocorrelation')
plt.grid(True)

plt.show()
```

### OUTPUT:

<img width="1062" height="611" alt="image" src="https://github.com/user-attachments/assets/e6369e29-58ff-4e15-a57f-659e0cf3d95f" />


### RESULT:
        Thus we have successfully implemented the auto correlation function and has a sharp cuttoff.
