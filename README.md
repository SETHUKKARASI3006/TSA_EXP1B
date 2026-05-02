# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 21.04.2026

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose
```

```
data = pd.read_csv('/content/education_vs_income_econometrics_samples.csv')
```

```
data.head()
```

```
data.set_index('x_education_years', inplace=True)
```

```
data['income_diff'] = data['y_income_thousands_usd'] - data['y_income_thousands_usd'].shift(1)
```

```
income_diff_cleaned = data['income_diff'].dropna()
result = seasonal_decompose(income_diff_cleaned, model='additive', period=7)
data['sea_diff'] = np.nan
mask = ~data['income_diff'].isna()
data.loc[mask, 'sea_diff'] = result.resid.values
```

```
data['income_log'] = np.log(data['y_income_thousands_usd'])
data['income_log_diff'] = data['income_log'] - data['income_log'].shift(1)
```

```
income_log_diff_cleaned = data['income_log_diff'].dropna()
result = seasonal_decompose(income_log_diff_cleaned, model='additive', period=7)
data['log_sea_diff'] = np.nan
mask = ~data['income_log_diff'].isna()
data.loc[mask, 'log_sea_diff'] = result.resid.values
```

```
plt.figure(figsize=(16, 16))
plt.subplot(6, 1, 1)
plt.plot(data['y_income_thousands_usd'], label='Original')
plt.legend(loc = 'best')
plt.title('Original data')
plt.xlabel('years')
plt.ylabel('Income')

plt.subplot(6, 1, 2)
plt.plot(data['income_diff'], label='Regular Differencing')
plt.legend(loc = 'best')
plt.title('Regular Differencing')
plt.xlabel('years')
plt.ylabel('Differenced Income')

plt.subplot(6, 1, 3)
plt.plot(data['sea_diff'], label='Seasonal Adjustment')
plt.legend(loc = 'best')
plt.title('Seasonal Adjustment')
plt.xlabel('years')
plt.ylabel('Seasonal Adjustment Income')

plt.subplot(6, 1, 4)
plt.plot(data['income_log'], label='Log Transformation')
plt.legend(loc = 'best')
plt.title('Log Transformation')
plt.xlabel('years')
plt.ylabel('Log(Income)')

plt.subplot(6, 1, 5)
plt.plot(data['income_log_diff'], label='Log Transformation and Regular Differencing')
plt.legend(loc = 'best')
plt.title('Log Transformation and Regular Differencing')
plt.xlabel('years')
plt.ylabel('RDiff(Log(Income))')

plt.subplot(6, 1, 6)
plt.plot(data['log_sea_diff'], label='Log Transformation and Regular Differencing and Seasonal Differncing')
plt.legend(loc = 'best')
plt.title('Log Transformation and Regular Differencing and Seasonal Differncing')
plt.xlabel('years')
plt.ylabel('SDiff(RDiff(Log(Income)))')

plt.tight_layout()
plt.show()
data.plot(kind = 'line')
```

### OUTPUT:


REGULAR DIFFERENCING:

<img width="1251" height="207" alt="image" src="https://github.com/user-attachments/assets/a8b1483e-2786-4dc0-9b76-ec68c42d777a" />

SEASONAL ADJUSTMENT:

<img width="1265" height="215" alt="image" src="https://github.com/user-attachments/assets/13360ed6-67c2-436c-ac2b-4e1b96868ec1" />

LOG TRANSFORMATION:

<img width="1253" height="203" alt="image" src="https://github.com/user-attachments/assets/e76a3c62-5746-4758-92b6-d61f464829d7" />

LOG TRANSFORMATION AND REGULAR DIFFERENCING:

<img width="1250" height="202" alt="image" src="https://github.com/user-attachments/assets/883ae1c4-dfaf-4d69-a1b8-57960ee763b1" />

LOG TRANSFORMATION AND REGULAR DIFFERENCING AND SEASONAL DIFFERENCING:

<img width="1257" height="210" alt="image" src="https://github.com/user-attachments/assets/8596a501-7d9d-4d82-a5d9-9f9cb861d0e1" />

### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
