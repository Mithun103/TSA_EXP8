# Ex.No: 08     MOVINTG AVERAGE MODEL AND EXPONENTIAL SMOOTHING
### Date: 


### AIM:
To implement Moving Average Model and Exponential smoothing Using Python.
### ALGORITHM:
1. Import necessary libraries
2. Read the electricity time series data from a CSV file,Display the shape and the first 20 rows of
the dataset
3. Set the figure size for plots
4. Suppress warnings
5. Plot the first 50 values of the 'Value' column
6. Perform rolling average transformation with a window size of 5
7. Display the first 10 values of the rolling mean
8. Perform rolling average transformation with a window size of 10
9. Create a new figure for plotting,Plot the original data and fitted value
10. Show the plot
11. Also perform exponential smoothing and plot the graph
### PROGRAM:
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
from statsmodels.tsa.ar_model import AutoReg
from sklearn.metrics import mean_squared_error

# Load the dataset
file_path = 'ECOMM DATA.csv'  # Replace with your actual file path
data = pd.read_csv(file_path)

# Display dataset information
print("Shape of the dataset:", data.shape)
print("First 50 rows of the dataset:")
print(data.head(50))

# Replace 'Profit' with the actual column name you want to analyze
plt.plot(data['Profit'].head(50))  # Adjust the column name if it's different
plt.title('First 50 values of the "Profit" column')
plt.xlabel('Index')
plt.ylabel('Profit')
plt.show()

# Calculate rolling mean with window size 5
rolling_mean_5 = data['Profit'].rolling(window=5).mean()

print("First 10 values of the rolling mean with window size 5:")
print(rolling_mean_5.head(10))

# Calculate rolling mean with window size 10
rolling_mean_10 = data['Profit'].rolling(window=10).mean()

# Plot original data and fitted value using rolling mean
plt.plot(data['Profit'], label='Original Data')
plt.plot(rolling_mean_10, label='Rolling Mean (window=10)', color='orange')
plt.title('Original Data and Fitted Value (Rolling Mean)')
plt.xlabel('Index')
plt.ylabel('Profit')
plt.legend()
plt.show()

# AutoRegressive (AR) model with lag order of 13
lag_order = 13
model = AutoReg(data['Profit'].dropna(), lags=lag_order)  # Ensure no NaN values
model_fit = model.fit()

# Plot ACF and PACF
plot_acf(data['Profit'].dropna())
plt.title('Autocorrelation Function (ACF)')
plt.show()

plot_pacf(data['Profit'].dropna())
plt.title('Partial Autocorrelation Function (PACF)')
plt.show()

# Generate predictions
predictions = model_fit.predict(start=lag_order, end=len(data)-1)

# Calculate and print Mean Squared Error (MSE)
mse = mean_squared_error(data['Profit'].dropna()[lag_order:], predictions)
print('Mean Squared Error (MSE):', mse)

# Plot predictions vs original data
plt.plot(data['Profit'][lag_order:], label='Original Data')
plt.plot(predictions, label='Predictions', color='red')
plt.title('AR Model Predictions vs Original Data')
plt.xlabel('Index')
plt.ylabel('Profit')
plt.legend()
plt.show()
```
### OUTPUT:
![image](https://github.com/user-attachments/assets/945076f3-66e9-49a2-8b2f-74769f58ce43)


![image](https://github.com/user-attachments/assets/08d6f889-3429-47ce-a0df-31ff9d0575cd)

![image](https://github.com/user-attachments/assets/29e0e003-b67b-4111-a81f-aba9c8ca677f)

![image](https://github.com/user-attachments/assets/2b66f3ef-3b25-4eab-ab13-a8a204d959f9)

![image](https://github.com/user-attachments/assets/3d4b243a-0127-4c71-91ee-bede37f14091)

### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
