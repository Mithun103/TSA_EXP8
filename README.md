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
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import warnings
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Suppress warnings
warnings.filterwarnings('ignore')

# Read the dataset from the uploaded CSV file
file_path = 'ECOMM DATA.csv'  # Path to the uploaded dataset
data = pd.read_csv(file_path)

# Display the shape and the first few rows of the dataset
print("Shape of the dataset:", data.shape)
print("First 20 rows of the dataset:")
print(data.head(20))

# Ensure the 'Date' column is in datetime format and set it as index
data['Order Date'] = pd.to_datetime(data['Order Date'])
data.set_index('Order Date', inplace=True)

# Plot Original
plt.figure(figsize=(12, 6))
plt.plot(data['Profit'], label='Profit', color='blue')
plt.title('Original Profit')
plt.xlabel('Date')
plt.ylabel('Profit')
plt.legend()
plt.grid()
plt.show()

# Moving Average
# Perform rolling average transformation with a window size of 3 (adjust as needed)
rolling_mean_3 = data['Profit'].rolling(window=3).mean()

# Plot Moving Average
plt.figure(figsize=(12, 6))
plt.plot(data['Profit'], label='Profit', color='blue')
plt.plot(rolling_mean_3, label='Moving Average (window=3)', color='orange')
plt.title('Moving Average of Profit')
plt.xlabel('Date')
plt.ylabel('Profit')
plt.legend()
plt.grid()
plt.show()

# Exponential Smoothing
model = ExponentialSmoothing(data['Profit'], trend='add', seasonal=None)
model_fit = model.fit()

# Make predictions for the next 5 periods (adjust as needed)
future_steps = 5
predictions = model_fit.predict(start=len(data), end=len(data) + future_steps - 1)

# Create a future index for the predicted dates
future_dates = pd.date_range(start=data.index[-1] + pd.Timedelta(days=1), periods=future_steps)

# Plot the original data and Exponential Smoothing predictions
plt.figure(figsize=(12, 6))
plt.plot(data['Profit'], label='Profit', color='blue')
plt.plot(future_dates, predictions, label='Exponential Smoothing Forecast', color='orange')
plt.title('Exponential Smoothing Predictions for profit')
plt.xlabel('Date')
plt.ylabel('profit')
plt.legend()
plt.xticks(rotation=45)
plt.grid(True)
plt.tight_layout()
plt.show()


```
### OUTPUT:
![image](https://github.com/user-attachments/assets/e2989f06-8516-4442-a20c-59ac037c46d3)
![image](https://github.com/user-attachments/assets/96ab6928-9179-455d-8bac-aaf18c4bd317)
![image](https://github.com/user-attachments/assets/c744395b-e761-42c4-ab16-1c086143114b)
![image](https://github.com/user-attachments/assets/aa37852f-6c7d-49a2-8f3f-e8865b1914d6)

### RESULT:
Thus we have successfully implemented the Moving Average Model and Exponential smoothing using python.
