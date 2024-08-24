# Developed by : Divakar R
# Register number : 212222240026
# Date : 

# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA

### AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
### ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
### PROGRAM:
IMPORTING PACKAGES:
```python

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
%matplotlib inline
train = pd.read_csv('Electric_Production.csv')
train['DATE'] = pd.to_datetime(train['DATE'], format='%d/%m/%Y')
train.head()
```
REGULAR DIFFERENCING:

```python
from statsmodels.tsa.stattools import adfuller
def adf_test(timeseries):
    print ('Results of Dickey-Fuller Test:')
    dftest = adfuller(timeseries, autolag='AIC')
    dfoutput = pd.Series(dftest[0:4], index=['Test Statistic','p-value','#Lags Used'
               ,'Number of Observations Used'])
    for key,value in dftest[4].items():
       dfoutput['Critical Value (%s)'%key] = value
    print (dfoutput)
adf_test(train['IPG2211A2N'])
train['DATE'] = pd.to_datetime(train['DATE'], format='%d/%m/%Y')
train['Year'] = train['DATE'].dt.year
```
SEASONAL ADJUSTMENT:
```python
data=train
data['SeasonalAdjustment'] = data.iloc[:,1] - data.iloc[:,1].shift(12)
data['SeasonalAdjustment'].dropna()
x=data['Year']
y=data["SeasonalAdjustment"]
plt.plot(x,y,color='black')
plt.title("ElectroGraph")
plt.xlabel("<-----Year---->",color='blue')
plt.ylabel("<-----Usage---->",color='red')
plt.show()
```
LOG TRANSFORMATION:
```python
data1=train
data1['log']=np.log(data1['IPG2211A2N_diff']).dropna()
data1=data1.dropna()
x=data1['Year']
y=data1['log']
plt.xlabel('Year',color='blue')
plt.ylabel('Log Values',color='red')
```

### OUTPUT:


REGULAR DIFFERENCING:

![309486763-0ac0763a-5c24-4edf-a629-c0bca584620b](https://github.com/user-attachments/assets/2b2bb5cd-1225-4377-998e-312c8ee9cec2)


SEASONAL ADJUSTMENT:

![309489099-e121a175-edfc-4cdd-bddd-db6dca44f5d0](https://github.com/user-attachments/assets/cf3fcd6e-bcc3-48e3-a9e9-4d6d4d21d93e)


LOG TRANSFORMATION:

![309489135-dcfa8245-c1b6-4358-ba2f-44f5e029d38f](https://github.com/user-attachments/assets/f3157b83-a2a2-4485-848d-d2d6d2034896)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
