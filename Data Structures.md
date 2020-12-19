# **Data Structures in Python**

***

There are many different ways to store data! Each has futional and behavioral nuances. Some key  structures are:
- lists
- arrays
    - 1D 
    - 2D
- dataframes



## **Lists** vs. **1D Arrays**
***

###### These structures are **very similar**. Both are:
- ordered
    - meaning they have an index number that tells thier position
- mutable
    - meaning you can add and remove elements after it is made
- can contain non unique values
    - meaning they can have the same value listed multiple times

###### Some **key differences**: 
- Lists can contain various data types while an array can only contain one at a time.
- Mathemcatical operations are applied value-wise in arrays and list-wise in lists.
- arrays are a more efficient and compact storage unit for data



```python
import numpy as np
import pandas as pd

# list
grades = [75, 88, 92, True]

#array
np_grades = np.array(grades)

print('List:', grades)
print('Array:', np_grades)
print(' ')
print('List multiplication:', grades * 2)
print('Array multiplication:', np_grades * 2)
```

    List: [75, 88, 92, True]
    Array: [75 88 92  1]
     
    List multiplication: [75, 88, 92, True, 75, 88, 92, True]
    Array multiplication: [150 176 184   2]


As we can see above, the list **grades** contains mixed values: integers and booleans. Multiplication on lists is applied to the whole list. This is why we see all of the values repeated twice.

The list **grades** was converted to an array and stored as **np_array**. During this conversion, the boolean value **True** was converted to an integer. This is because arrays are incapable of containing mixed values. The multiplication operation was applied element-wise, so each value is individually multiplied by 2.

## **1D Arrays** vs **2D Arrays**
***

##### 1D array
- stores data in one dimension
- a value's position is defined by its index number
- can be visualized as a single line:

<img src="attachment:screen%20shot%202020-11-07%20at%206.39.32%20pm.png" style="max-width:40%">

***

##### 2D array
- stores data in two dimensions
- a value's position is defined by its row and column number
- can be visualized as a table:

<img src="attachment:screen%20shot%202020-11-07%20at%206.34.32%20pm.png" style="max-width:100%">

## **2D Arrays** vs **Dataframes**
***

##### Similarities:
- have two dimensions
- are tabular

2D array:
![screen%20shot%202020-12-18%20at%203.06.56%20pm.png](attachment:screen%20shot%202020-12-18%20at%203.06.56%20pm.png)
DataFrame:
![screen%20shot%202020-12-18%20at%203.07.00%20pm.png](attachment:screen%20shot%202020-12-18%20at%203.07.00%20pm.png)

##### Differences:
- DataFrames have indices for rows AND columns
- DataFrames can contain different types of data

We can think of DataFrames as a 2D array with indices on the rows and columns. 

When you call *dataframe.values* we can see that a dataframe is really just made up of arrays:


```python
df = pd.DataFrame(np.random.randint(0, 100, size=(4, 4)), columns=['a', 'b', 'c', 'd'])

print(type(df))
df
```

    <class 'pandas.core.frame.DataFrame'>





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
      <th>a</th>
      <th>b</th>
      <th>c</th>
      <th>d</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>73</td>
      <td>53</td>
      <td>58</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>64</td>
      <td>81</td>
      <td>34</td>
      <td>40</td>
    </tr>
    <tr>
      <th>2</th>
      <td>35</td>
      <td>95</td>
      <td>65</td>
      <td>14</td>
    </tr>
    <tr>
      <th>3</th>
      <td>34</td>
      <td>57</td>
      <td>21</td>
      <td>82</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(type(df.values))
df.values
```

    <class 'numpy.ndarray'>





    array([[73, 53, 58, 12],
           [64, 81, 34, 40],
           [35, 95, 65, 14],
           [34, 57, 21, 82]])


