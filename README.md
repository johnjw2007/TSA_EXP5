# Ex.No: 05  IMPLEMENTATION OF TIME SERIES ANALYSIS AND DECOMPOSITION
### Date: 


### AIM:
To Illustrates how to perform time series analysis and decomposition on the monthly average temperature of a city/country and for airline passengers.

### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the decomposition process for the required data.
4. Plot the data according to need, either seasonal_decomposition or trend plot.
5. Display the overall results.

### PROGRAM:
```
import pandas as pd
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
import matplotlib.dates as mdates

# Load the dataset
data = pd.read_csv('XAUUSD_2010-2023.csv')

# Parse the 'time' column as dates and set it as the index
data['Date'] = pd.to_datetime(data['time'], format='%d-%m-%Y %H:%M')
data.set_index('Date', inplace=True)

# Resample to monthly frequency and interpolate missing data
monthly_data = data['close'].resample('M').mean().interpolate()

# Plot the original monthly resampled data
plt.figure(figsize=(7, 4))
plt.plot(monthly_data, label='Monthly Average Close (Interpolated)')
plt.title('XAUUSD Time Series Data (Monthly Average)', fontsize=10)
plt.xlabel('Date', fontsize=14)
plt.ylabel('Price (USD)', fontsize=14)
plt.grid(True)
plt.legend()
plt.xticks(fontsize=10)
plt.yticks(fontsize=10)
plt.tight_layout()
plt.show()

# Perform seasonal decomposition
decomposition = seasonal_decompose(monthly_data.dropna(), model='multiplicative', period=3)

# Plot the decomposition results
fig = decomposition.plot()
fig.set_size_inches(7, 4)

# Format the x-axis labels for each plot
for ax in fig.axes:
    ax.xaxis.set_major_locator(mdates.YearLocator())
    ax.xaxis.set_major_formatter(mdates.DateFormatter('%Y'))
    ax.tick_params(axis='x', rotation=45, labelsize=10)
    ax.tick_params(axis='y', labelsize=10)

plt.tight_layout()
plt.show()

```
### OUTPUT:
FIRST FIVE ROWS:
<img width="806" height="283" alt="image" src="https://github.com/user-attachments/assets/d621439b-6576-4990-8826-d2dc2e2e606c" />

PLOTTING THE DATA:
<img width="897" height="474" alt="image" src="https://github.com/user-attachments/assets/ff725aaa-3827-4f7d-bf75-d58c3b459670" />

SEASONAL PLOT REPRESENTATION :
<img width="868" height="477" alt="image" src="https://github.com/user-attachments/assets/35390892-e3d6-496f-a9c5-8b97ac8c6408" />

### RESULT:
Thus we have created the python code for the time series analysis and decomposition.
