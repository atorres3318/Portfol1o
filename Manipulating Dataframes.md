### Evaluating Data
I will downloaded Data about Covid exposures in Halifax, Nova Scotia from **Nov 19 - Nov 25**. I will:
- create a dataframe
- manipulate dataframe
    - delete columns
    - adding column titles
    - switch data to date-time
    - create new columns
- use a loop create a column of street names


```python
import pandas as pd
import matplotlib.pyplot as plt
import numpy as np
import seaborn as sns
```

### Reading in dataframe:


```python
data = pd.read_csv('covid_exposures.csv')

data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Fit4Less</th>
      <th>Wed, 11/25/2020 -18:00</th>
      <th>1535 Dresden Row, Halifax</th>
      <th>details</th>
      <th>Get tested immediately</th>
      <th>Central</th>
      <th>11/27/2020 - 20:35</th>
      <th>Gym</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fit4Less Sackville</td>
      <td>Wed, 11/25/2020 -15:30</td>
      <td>776 Sackville Dr, Lower Sackville</td>
      <td>details</td>
      <td>Get tested immediately</td>
      <td>Central</td>
      <td>12/03/2020 - 09:33</td>
      <td>Gym</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bluenose II Restaurant</td>
      <td>Wed, 11/25/2020 -08:30</td>
      <td>1824 Hollis St, Halifax</td>
      <td>details</td>
      <td>Get tested immediately</td>
      <td>Central</td>
      <td>11/30/2020 - 15:51</td>
      <td>Restaurant/Bar</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fit4Less Sackville</td>
      <td>Tue, 11/24/2020 - 17:00</td>
      <td>776 Sackville Dr, Lower Sackville</td>
      <td>details</td>
      <td>Get tested immediately</td>
      <td>Central</td>
      <td>12/03/2020 - 09:33</td>
      <td>Gym</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bluenose II Restaurant</td>
      <td>Tue, 11/24/2020 - 08:30</td>
      <td>1824 Hollis St, Halifax</td>
      <td>details</td>
      <td>Get tested immediately</td>
      <td>Central</td>
      <td>11/30/2020 - 15:50</td>
      <td>Restaurant/Bar</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Agricola Street Brasserie</td>
      <td>Mon, 11/23/2020 -18:00</td>
      <td>2540 Agricola St, Halifax</td>
      <td>details</td>
      <td>Get tested immediately</td>
      <td>Central</td>
      <td>12/03/2020 - 09:34</td>
      <td>Restaurant/Bar</td>
    </tr>
  </tbody>
</table>
</div>



### Manipulating dataframe:


```python
#accidentally forgot to copy the column heads so adding them back in
data.columns = ['where', 'date', 'address', 'details', 'advice', 'zone', 'last_updated', 'Establishment']
#removing the data we dont need
data = data.drop(columns = ['details', 'zone', 'last_updated'])
#converting to timedate
data['date']= pd.to_datetime(data['date'])
```

##### Create street name column:

Using a for loops to grab the second word in the 'address' column. Appending this to the dataframe.


```python
# Grabbing just street name
N = 2
streets = []
for val in data.address:
    street = val.split(' ')[1]
    streets.append(street)

np_streets = np.array(streets)
data['Street'] = np_streets
data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>where</th>
      <th>date</th>
      <th>address</th>
      <th>advice</th>
      <th>Establishment</th>
      <th>Street</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Fit4Less Sackville</td>
      <td>2020-11-25 15:30:00</td>
      <td>776 Sackville Dr, Lower Sackville</td>
      <td>Get tested immediately</td>
      <td>Gym</td>
      <td>Sackville</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Bluenose II Restaurant</td>
      <td>2020-11-25 08:30:00</td>
      <td>1824 Hollis St, Halifax</td>
      <td>Get tested immediately</td>
      <td>Restaurant/Bar</td>
      <td>Hollis</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Fit4Less Sackville</td>
      <td>2020-11-24 17:00:00</td>
      <td>776 Sackville Dr, Lower Sackville</td>
      <td>Get tested immediately</td>
      <td>Gym</td>
      <td>Sackville</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Bluenose II Restaurant</td>
      <td>2020-11-24 08:30:00</td>
      <td>1824 Hollis St, Halifax</td>
      <td>Get tested immediately</td>
      <td>Restaurant/Bar</td>
      <td>Hollis</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Agricola Street Brasserie</td>
      <td>2020-11-23 18:00:00</td>
      <td>2540 Agricola St, Halifax</td>
      <td>Get tested immediately</td>
      <td>Restaurant/Bar</td>
      <td>Agricola</td>
    </tr>
  </tbody>
</table>
</div>


