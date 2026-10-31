# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 31-10-2026


### AIM:
To develop a Python program to convert non-stationary time series data into stationary data using Regular Differencing, Seasonal Adjustment, and Log Transformation on the International Airline Passenger dataset.

# Dataset Name : AirPassengers

### ALGORITHM:
1. Import the required libraries such as Pandas, NumPy, Matplotlib, and Statsmodels.
2. Read the AirPassengers dataset using Pandas.
3. Convert the Month column into datetime format and set it as the index.
4. Perform Regular Differencing to remove the trend from the data.
5. Perform Seasonal Adjustment to remove seasonal variations.
6. Apply Log Transformation to stabilize the variance.
7. Perform Log Transformation with Regular Differencing.
8. Perform Log Transformation with Regular and Seasonal Differencing.
9. Plot the original data and all transformed data for comparison.
10. Display the graphs and observe the changes.

### PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

data = pd.read_csv("AirPassengers.csv")
data['Month'] = pd.to_datetime(data['Month'])
data.set_index('Month', inplace=True)

data = data.dropna(subset=['#Passengers'])
data['passenger_diff'] = data['#Passengers'].diff()

result = seasonal_decompose(
    data['#Passengers'],
    model='additive',
    period=12
)

data['passenger_seasonal_diff'] = result.resid
data['passenger_log'] = np.log(data['#Passengers'])

# Log + Regular Difference
data['passenger_log_diff'] = (
    data['passenger_log'] -
    data['passenger_log'].shift(1)
)

# Log + Seasonal Difference
result = seasonal_decompose(
    data['passenger_log_diff'].dropna(),
    model='additive',
    period=12
)

data['passenger_log_seasonal_diff'] = result.resid
plt.figure(figsize=(16,16))

# Original Data
plt.subplot(6,1,1)
plt.plot(data['#Passengers'], label='Original')
plt.legend(loc='best')
plt.title('Original Passenger Data')
plt.xlabel('Year')
plt.ylabel('Passengers')

# Regular Difference
plt.subplot(6,1,2)
plt.plot(data['passenger_diff'], label='Regular Difference')
plt.legend(loc='best')
plt.title('Regular Differencing')
plt.xlabel('Year')
plt.ylabel('Differenced Passengers')

# Seasonal Adjustment
plt.subplot(6,1,3)
plt.plot(data['passenger_seasonal_diff'],
         label='Seasonal Adjustment')
plt.legend(loc='best')
plt.title('Seasonal Adjustment')
plt.xlabel('Year')
plt.ylabel('Seasonally Adjusted Passengers')

# Log Transformation
plt.subplot(6,1,4)
plt.plot(data['passenger_log'],
         label='Log Transformation')
plt.legend(loc='best')
plt.title('Log Transformation')
plt.xlabel('Year')
plt.ylabel('Log(Passengers)')

# Log + Difference
plt.subplot(6,1,5)
plt.plot(data['passenger_log_diff'],
         label='Log + Difference')
plt.legend(loc='best')
plt.title('Log Transformation + Regular Difference')
plt.xlabel('Year')
plt.ylabel('Diff(Log(Passengers))')

# Log + Seasonal Difference
plt.subplot(6,1,6)
plt.plot(data['passenger_log_seasonal_diff'],
         label='Log + Regular + Seasonal Difference')
plt.legend(loc='best')
plt.title('Log + Regular + Seasonal Difference')
plt.xlabel('Year')
plt.ylabel('Seasonally Differenced Log(Passengers)')

plt.tight_layout()
plt.show()

# Plot all transformed columns
data.plot(figsize=(12,6))
plt.show()
```

### OUTPUT:
ORIGINAL DATA:
<img width="1145" height="227" alt="image" src="https://github.com/user-attachments/assets/9ef4610d-4182-460e-9261-68437a3ea567" />


REGULAR DIFFERENCING:
<img width="1157" height="186" alt="image" src="https://github.com/user-attachments/assets/d08e47a6-3422-4d84-8dd5-38d4bca71ed9" />


SEASONAL ADJUSTMENT:
<img width="1153" height="186" alt="image" src="https://github.com/user-attachments/assets/7c604f6a-341d-4fde-a4c1-e2c6d135b80b" />


LOG TRANSFORMATION:
<img width="1153" height="187" alt="image" src="https://github.com/user-attachments/assets/71d6d1aa-b301-4cdf-b46d-44a47703bb0f" />


LOG TRANSFORMATION + REGULAR DIFFERENCING:
<img width="1148" height="190" alt="image" src="https://github.com/user-attachments/assets/555b92a2-2e72-4b94-8fc9-b8487c85d5de" />


LOG TRANSFORMATION + REGULAR DIFFERENCE + SEASONAL DIFFERENCE:
<img width="1162" height="225" alt="image" src="https://github.com/user-attachments/assets/1c8934f7-c387-436f-9344-45288fde7a54" />

<img width="602" height="283" alt="image" src="https://github.com/user-attachments/assets/e0ca0828-ab45-403d-8fe9-4f1c22415f3f" />




### RESULT:
Thus, the Python program for converting non-stationary time series data into stationary data using Regular Differencing, Seasonal Adjustment, and Log Transformation on the International Airline Passenger dataset was successfully developed and executed.data.
