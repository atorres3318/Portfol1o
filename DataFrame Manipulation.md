### Evaluating Data
I will downloaded Data about Covid exposures in Halifax, Nova Scotia from **Nov 19 - Nov 25**. I will:
- create a dataframe
- manipulate dataframe
    - delete columns
    - adding column titles
    - switch data to date-time
    - create new columns
- use a loop create a column of street names
- create bar plots
- create heat maps


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



### Visualizations:
Bargraphs:


```python
np_type = np.array(data['Establishment'])

#organizing locations by top covid cases
type_, counts = np.unique(np_type, return_counts=True)
a = dict(sorted((dict(zip(type_, counts))).items(), key=lambda item: item[1], reverse = True))
print(a)

#creating bargraph
df = pd.DataFrame(a.items(), columns=['Establishment', 'Num_exposures'])
df = df.iloc[:8]
plt.bar(df.Establishment, df.Num_exposures)
plt.title('Top Establishments with Covid Exposures in Halifax')
plt.xlabel('Establishment')
plt.ylabel('Number of Exposures')
```

    {' Restaurant/Bar': 56, ' Gym': 13, ' Grocery Store': 4, ' School': 4, ' Mall': 3, ' Salon': 3, ' Cinema': 2, ' Coffee Shop': 2}





    Text(0, 0.5, 'Number of Exposures')






    
![png](covid%20code%20%281%29_files/covid%20code%20%281%29_9_2.png)
    




```python
#dictionary of street name number of times that street has had an exposure
street, counts = np.unique(np_streets, return_counts=True)
d = dict(sorted((dict(zip(street, counts))).items(), key=lambda item: item[1], reverse = True))

#converting to df to plot
df = pd.DataFrame(d.items(), columns=['Street_name', 'Num_exposures'])
df = df.iloc[:8]
plt.bar(df.Street_name, df.Num_exposures)
plt.title('Top Streets with Covid Exposures in Halifax')
plt.xlabel('Street Name')
plt.ylabel('Number of Exposures')
```




    Text(0, 0.5, 'Number of Exposures')






    
![png](covid%20code%20%281%29_files/covid%20code%20%281%29_10_1.png)
    






```python
heat = data.loc[:, ['Street', 'Establishment']]
heat = heat.pivot_table(index = ['Street'], columns = ['Establishment'], aggfunc = len, fill_value=0)
heat.head()
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
      <th>Establishment</th>
      <th>Cinema</th>
      <th>Coffee Shop</th>
      <th>Grocery Store</th>
      <th>Gym</th>
      <th>Mall</th>
      <th>Restaurant/Bar</th>
      <th>Salon</th>
      <th>School</th>
    </tr>
    <tr>
      <th>Street</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Agricola</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Argyle</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>4</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Barrington</th>
      <td>0</td>
      <td>0</td>
      <td>2</td>
      <td>0</td>
      <td>0</td>
      <td>9</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Bedford</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>1</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Brunswick</th>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
a4_dims = (8, 8)
fig, ax = plt.subplots(figsize=a4_dims)
ax = sns.heatmap(heat)
ax.set_title('Top Covid Exposures Locations in Halifax')
```




    Text(0.5, 1.0, 'Top Covid Exposures Locations in Halifax')






    
![png](covid%20code%20%281%29_files/covid%20code%20%281%29_13_1.png)
    


