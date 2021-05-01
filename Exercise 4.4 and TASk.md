```python
# import libraries
import pandas as pd
import numpy as np
import os
```


```python
# import orders_csv
df_ords = pd.read_csv(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Original Data/orders.csv', index_col = False)
```


```python
# import products_csv
df_prods = pd.read_csv(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Original Data/products.csv', index_col = False)
```


```python
# import departments_csv
df_dep = pd.read_csv(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Original Data/departments.csv', index_col = False)
```


```python
path = r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3'
```


```python
path
```




    '/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3'




```python
df_dep.head()
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
      <th>department_id</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>department</td>
      <td>frozen</td>
      <td>other</td>
      <td>bakery</td>
      <td>produce</td>
      <td>alcohol</td>
      <td>international</td>
      <td>beverages</td>
      <td>pets</td>
      <td>dry goods pasta</td>
      <td>...</td>
      <td>meat seafood</td>
      <td>pantry</td>
      <td>breakfast</td>
      <td>canned goods</td>
      <td>dairy eggs</td>
      <td>household</td>
      <td>babies</td>
      <td>snacks</td>
      <td>deli</td>
      <td>missing</td>
    </tr>
  </tbody>
</table>
<p>1 rows × 22 columns</p>
</div>




```python
# transposing df_dep
df_dep.T
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>department_id</th>
      <td>department</td>
    </tr>
    <tr>
      <th>1</th>
      <td>frozen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>other</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bakery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>produce</td>
    </tr>
    <tr>
      <th>5</th>
      <td>alcohol</td>
    </tr>
    <tr>
      <th>6</th>
      <td>international</td>
    </tr>
    <tr>
      <th>7</th>
      <td>beverages</td>
    </tr>
    <tr>
      <th>8</th>
      <td>pets</td>
    </tr>
    <tr>
      <th>9</th>
      <td>dry goods pasta</td>
    </tr>
    <tr>
      <th>10</th>
      <td>bulk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>personal care</td>
    </tr>
    <tr>
      <th>12</th>
      <td>meat seafood</td>
    </tr>
    <tr>
      <th>13</th>
      <td>pantry</td>
    </tr>
    <tr>
      <th>14</th>
      <td>breakfast</td>
    </tr>
    <tr>
      <th>15</th>
      <td>canned goods</td>
    </tr>
    <tr>
      <th>16</th>
      <td>dairy eggs</td>
    </tr>
    <tr>
      <th>17</th>
      <td>household</td>
    </tr>
    <tr>
      <th>18</th>
      <td>babies</td>
    </tr>
    <tr>
      <th>19</th>
      <td>snacks</td>
    </tr>
    <tr>
      <th>20</th>
      <td>deli</td>
    </tr>
    <tr>
      <th>21</th>
      <td>missing</td>
    </tr>
  </tbody>
</table>
</div>




```python
# create new dataframe from the transposed version
df_dep_t = df_dep.T
```


```python
df_dep_t
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>department_id</th>
      <td>department</td>
    </tr>
    <tr>
      <th>1</th>
      <td>frozen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>other</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bakery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>produce</td>
    </tr>
    <tr>
      <th>5</th>
      <td>alcohol</td>
    </tr>
    <tr>
      <th>6</th>
      <td>international</td>
    </tr>
    <tr>
      <th>7</th>
      <td>beverages</td>
    </tr>
    <tr>
      <th>8</th>
      <td>pets</td>
    </tr>
    <tr>
      <th>9</th>
      <td>dry goods pasta</td>
    </tr>
    <tr>
      <th>10</th>
      <td>bulk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>personal care</td>
    </tr>
    <tr>
      <th>12</th>
      <td>meat seafood</td>
    </tr>
    <tr>
      <th>13</th>
      <td>pantry</td>
    </tr>
    <tr>
      <th>14</th>
      <td>breakfast</td>
    </tr>
    <tr>
      <th>15</th>
      <td>canned goods</td>
    </tr>
    <tr>
      <th>16</th>
      <td>dairy eggs</td>
    </tr>
    <tr>
      <th>17</th>
      <td>household</td>
    </tr>
    <tr>
      <th>18</th>
      <td>babies</td>
    </tr>
    <tr>
      <th>19</th>
      <td>snacks</td>
    </tr>
    <tr>
      <th>20</th>
      <td>deli</td>
    </tr>
    <tr>
      <th>21</th>
      <td>missing</td>
    </tr>
  </tbody>
</table>
</div>




```python
df_dep_t.reset_index()
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
      <th>index</th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>department_id</td>
      <td>department</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>frozen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>other</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>bakery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>produce</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>alcohol</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>international</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>beverages</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>pets</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>dry goods pasta</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>bulk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>personal care</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>meat seafood</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>pantry</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>breakfast</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>canned goods</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>dairy eggs</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>household</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>babies</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>snacks</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>deli</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>missing</td>
    </tr>
  </tbody>
</table>
</div>




```python
# take the first row of df_dep_t for the header
new_header = df_dep_t.iloc[0]
```


```python
new_header
```




    0    department
    Name: department_id, dtype: object




```python
# take the data under the header row for a new df
df_dep_t_new = df_dep_t[1:]
```


```python
df_dep_t_new
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
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>frozen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>other</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bakery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>produce</td>
    </tr>
    <tr>
      <th>5</th>
      <td>alcohol</td>
    </tr>
    <tr>
      <th>6</th>
      <td>international</td>
    </tr>
    <tr>
      <th>7</th>
      <td>beverages</td>
    </tr>
    <tr>
      <th>8</th>
      <td>pets</td>
    </tr>
    <tr>
      <th>9</th>
      <td>dry goods pasta</td>
    </tr>
    <tr>
      <th>10</th>
      <td>bulk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>personal care</td>
    </tr>
    <tr>
      <th>12</th>
      <td>meat seafood</td>
    </tr>
    <tr>
      <th>13</th>
      <td>pantry</td>
    </tr>
    <tr>
      <th>14</th>
      <td>breakfast</td>
    </tr>
    <tr>
      <th>15</th>
      <td>canned goods</td>
    </tr>
    <tr>
      <th>16</th>
      <td>dairy eggs</td>
    </tr>
    <tr>
      <th>17</th>
      <td>household</td>
    </tr>
    <tr>
      <th>18</th>
      <td>babies</td>
    </tr>
    <tr>
      <th>19</th>
      <td>snacks</td>
    </tr>
    <tr>
      <th>20</th>
      <td>deli</td>
    </tr>
    <tr>
      <th>21</th>
      <td>missing</td>
    </tr>
  </tbody>
</table>
</div>




```python
# set the header row as the df header
df_dep_t_new.columns = new_header
```


```python
df_dep_t_new
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
      <th>department_id</th>
      <th>department</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>frozen</td>
    </tr>
    <tr>
      <th>2</th>
      <td>other</td>
    </tr>
    <tr>
      <th>3</th>
      <td>bakery</td>
    </tr>
    <tr>
      <th>4</th>
      <td>produce</td>
    </tr>
    <tr>
      <th>5</th>
      <td>alcohol</td>
    </tr>
    <tr>
      <th>6</th>
      <td>international</td>
    </tr>
    <tr>
      <th>7</th>
      <td>beverages</td>
    </tr>
    <tr>
      <th>8</th>
      <td>pets</td>
    </tr>
    <tr>
      <th>9</th>
      <td>dry goods pasta</td>
    </tr>
    <tr>
      <th>10</th>
      <td>bulk</td>
    </tr>
    <tr>
      <th>11</th>
      <td>personal care</td>
    </tr>
    <tr>
      <th>12</th>
      <td>meat seafood</td>
    </tr>
    <tr>
      <th>13</th>
      <td>pantry</td>
    </tr>
    <tr>
      <th>14</th>
      <td>breakfast</td>
    </tr>
    <tr>
      <th>15</th>
      <td>canned goods</td>
    </tr>
    <tr>
      <th>16</th>
      <td>dairy eggs</td>
    </tr>
    <tr>
      <th>17</th>
      <td>household</td>
    </tr>
    <tr>
      <th>18</th>
      <td>babies</td>
    </tr>
    <tr>
      <th>19</th>
      <td>snacks</td>
    </tr>
    <tr>
      <th>20</th>
      <td>deli</td>
    </tr>
    <tr>
      <th>21</th>
      <td>missing</td>
    </tr>
  </tbody>
</table>
</div>




```python
# turn dataframe into data dictionary
data_dict = df_dep_t_new.to_dict('index')
```


```python
data_dict
```




    {'1': {'department': 'frozen'},
     '2': {'department': 'other'},
     '3': {'department': 'bakery'},
     '4': {'department': 'produce'},
     '5': {'department': 'alcohol'},
     '6': {'department': 'international'},
     '7': {'department': 'beverages'},
     '8': {'department': 'pets'},
     '9': {'department': 'dry goods pasta'},
     '10': {'department': 'bulk'},
     '11': {'department': 'personal care'},
     '12': {'department': 'meat seafood'},
     '13': {'department': 'pantry'},
     '14': {'department': 'breakfast'},
     '15': {'department': 'canned goods'},
     '16': {'department': 'dairy eggs'},
     '17': {'department': 'household'},
     '18': {'department': 'babies'},
     '19': {'department': 'snacks'},
     '20': {'department': 'deli'},
     '21': {'department': 'missing'}}




```python
df_prods.head()
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
      <th>product_id</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Chocolate Sandwich Cookies</td>
      <td>61</td>
      <td>19</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>All-Seasons Salt</td>
      <td>104</td>
      <td>13</td>
      <td>9.3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Robust Golden Unsweetened Oolong Tea</td>
      <td>94</td>
      <td>7</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>4</td>
      <td>Smart Ones Classic Favorites Mini Rigatoni Wit...</td>
      <td>38</td>
      <td>1</td>
      <td>10.5</td>
    </tr>
    <tr>
      <th>4</th>
      <td>5</td>
      <td>Green Chile Anytime Sauce</td>
      <td>5</td>
      <td>13</td>
      <td>4.3</td>
    </tr>
  </tbody>
</table>
</div>




```python
print(data_dict.get('19'))
```

    {'department': 'snacks'}



```python
df_snacks =  df_prods[df_prods['department_id']==19]
```


```python
df_prods['department_id']==19
```




    0         True
    1        False
    2        False
    3        False
    4        False
             ...  
    49688    False
    49689    False
    49690    False
    49691    False
    49692    False
    Name: department_id, Length: 49693, dtype: bool




```python
df_snacks =  df_prods[df_prods['department_id']==19]
```


```python
df_snacks.head()
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
      <th>product_id</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>Chocolate Sandwich Cookies</td>
      <td>61</td>
      <td>19</td>
      <td>5.8</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16</td>
      <td>Mint Chocolate Flavored Syrup</td>
      <td>103</td>
      <td>19</td>
      <td>5.2</td>
    </tr>
    <tr>
      <th>24</th>
      <td>25</td>
      <td>Salted Caramel Lean Protein &amp; Fiber Bar</td>
      <td>3</td>
      <td>19</td>
      <td>1.9</td>
    </tr>
    <tr>
      <th>31</th>
      <td>32</td>
      <td>Nacho Cheese White Bean Chips</td>
      <td>107</td>
      <td>19</td>
      <td>4.9</td>
    </tr>
    <tr>
      <th>40</th>
      <td>41</td>
      <td>Organic Sourdough Einkorn Crackers Rosemary</td>
      <td>78</td>
      <td>19</td>
      <td>6.5</td>
    </tr>
  </tbody>
</table>
</div>



# Beginning of Task for exercise 4.4


```python
df_ords.head()
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
      <th>order_id</th>
      <th>user_id</th>
      <th>eval_set</th>
      <th>order_number</th>
      <th>order_dow</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2539329</td>
      <td>1</td>
      <td>prior</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2398795</td>
      <td>1</td>
      <td>prior</td>
      <td>2</td>
      <td>3</td>
      <td>7</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>473747</td>
      <td>1</td>
      <td>prior</td>
      <td>3</td>
      <td>3</td>
      <td>12</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2254736</td>
      <td>1</td>
      <td>prior</td>
      <td>4</td>
      <td>4</td>
      <td>7</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>431534</td>
      <td>1</td>
      <td>prior</td>
      <td>5</td>
      <td>4</td>
      <td>15</td>
      <td>28.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 2. change a variable which doesnt need to be identified as numeric variable into a suitable format
df_ords['order_id'] = df_ords['order_id'].astype('str')
```


```python
# check order_id new data type (object)
df_ords['order_id'].dtype
```




    dtype('O')




```python
# 3. change unintuitive name for variable order_dow
df_ords.rename(columns = {'order_dow' : 'orders_day_of_the_week'}, inplace = True)
```


```python
# check name has been changed
df_ords.head()
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
      <th>order_id</th>
      <th>user_id</th>
      <th>eval_set</th>
      <th>order_number</th>
      <th>orders_day_of_the_week</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2539329</td>
      <td>1</td>
      <td>prior</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2398795</td>
      <td>1</td>
      <td>prior</td>
      <td>2</td>
      <td>3</td>
      <td>7</td>
      <td>15.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>473747</td>
      <td>1</td>
      <td>prior</td>
      <td>3</td>
      <td>3</td>
      <td>12</td>
      <td>21.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2254736</td>
      <td>1</td>
      <td>prior</td>
      <td>4</td>
      <td>4</td>
      <td>7</td>
      <td>29.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>431534</td>
      <td>1</td>
      <td>prior</td>
      <td>5</td>
      <td>4</td>
      <td>15</td>
      <td>28.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# 4. busiest hour for placing orders. DON'T KNOW HOW TO DO THAT
df_ords['order_hour_of_day'].value_counts(dropna = False)
```




    10    288418
    11    284728
    15    283639
    14    283042
    13    277999
    12    272841
    16    272553
    9     257812
    17    228795
    18    182912
    8     178201
    19    140569
    20    104292
    7      91868
    21     78109
    22     61468
    23     40043
    6      30529
    0      22758
    1      12398
    5       9569
    2       7539
    4       5527
    3       5474
    Name: order_hour_of_day, dtype: int64



The busiest hour for placing orders is 10am.


```python
# 5. determine meaning of 4 in 'department_id' columm. We can use steps 31 and 32 from the exercise
data_dict = df_dep_t_new.to_dict('index')
```


```python
# Meaning of department-id is "produce"
data_dict
```




    {'1': {'department': 'frozen'},
     '2': {'department': 'other'},
     '3': {'department': 'bakery'},
     '4': {'department': 'produce'},
     '5': {'department': 'alcohol'},
     '6': {'department': 'international'},
     '7': {'department': 'beverages'},
     '8': {'department': 'pets'},
     '9': {'department': 'dry goods pasta'},
     '10': {'department': 'bulk'},
     '11': {'department': 'personal care'},
     '12': {'department': 'meat seafood'},
     '13': {'department': 'pantry'},
     '14': {'department': 'breakfast'},
     '15': {'department': 'canned goods'},
     '16': {'department': 'dairy eggs'},
     '17': {'department': 'household'},
     '18': {'department': 'babies'},
     '19': {'department': 'snacks'},
     '20': {'department': 'deli'},
     '21': {'department': 'missing'}}




```python
# 6. subset for "breakfast" items
df_breakfast=df_prods[df_prods['department_id']==14]
```


```python
df_breakfast
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
      <th>product_id</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>27</th>
      <td>28</td>
      <td>Wheat Chex Cereal</td>
      <td>121</td>
      <td>14</td>
      <td>10.1</td>
    </tr>
    <tr>
      <th>33</th>
      <td>34</td>
      <td>NaN</td>
      <td>121</td>
      <td>14</td>
      <td>12.2</td>
    </tr>
    <tr>
      <th>67</th>
      <td>68</td>
      <td>Pancake Mix, Buttermilk</td>
      <td>130</td>
      <td>14</td>
      <td>13.7</td>
    </tr>
    <tr>
      <th>89</th>
      <td>90</td>
      <td>Smorz Cereal</td>
      <td>121</td>
      <td>14</td>
      <td>3.9</td>
    </tr>
    <tr>
      <th>210</th>
      <td>211</td>
      <td>Gluten Free Organic Cereal Coconut Maple Vanilla</td>
      <td>130</td>
      <td>14</td>
      <td>3.6</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49330</th>
      <td>49326</td>
      <td>Cereal Variety Fun Pack</td>
      <td>121</td>
      <td>14</td>
      <td>9.1</td>
    </tr>
    <tr>
      <th>49395</th>
      <td>49391</td>
      <td>Light and Fluffy Buttermilk Pancake Mix</td>
      <td>130</td>
      <td>14</td>
      <td>2.0</td>
    </tr>
    <tr>
      <th>49547</th>
      <td>49543</td>
      <td>Chocolate Cheerios Cereal</td>
      <td>121</td>
      <td>14</td>
      <td>10.8</td>
    </tr>
    <tr>
      <th>49637</th>
      <td>49633</td>
      <td>Shake 'N Pour Buttermilk Pancake Mix</td>
      <td>130</td>
      <td>14</td>
      <td>14.2</td>
    </tr>
    <tr>
      <th>49667</th>
      <td>49663</td>
      <td>Ultra Protein Power Crunch Peanut Butter N' Ho...</td>
      <td>57</td>
      <td>14</td>
      <td>10.2</td>
    </tr>
  </tbody>
</table>
<p>1116 rows × 5 columns</p>
</div>




```python
# 7. Details of customers & dinner parties (5-alcohol, 20-deli, 7-beverages, 12-meat seafood)
df_party=df_prods.loc[df_prods['department_id'].isin([5,20,7,12])]
```


```python
df_party
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
      <th>product_id</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>Robust Golden Unsweetened Oolong Tea</td>
      <td>94</td>
      <td>7</td>
      <td>4.5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>7</td>
      <td>Pure Coconut Water With Orange</td>
      <td>98</td>
      <td>7</td>
      <td>4.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>10</td>
      <td>Sparkling Orange Juice &amp; Prickly Pear Beverage</td>
      <td>115</td>
      <td>7</td>
      <td>8.4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>11</td>
      <td>Peach Mango Juice</td>
      <td>31</td>
      <td>7</td>
      <td>2.8</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17</td>
      <td>Rendered Duck Fat</td>
      <td>35</td>
      <td>12</td>
      <td>17.1</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49676</th>
      <td>49672</td>
      <td>Cafe Mocha K-Cup Packs</td>
      <td>26</td>
      <td>7</td>
      <td>6.5</td>
    </tr>
    <tr>
      <th>49679</th>
      <td>49675</td>
      <td>Cinnamon Dolce Keurig Brewed K Cups</td>
      <td>26</td>
      <td>7</td>
      <td>14.0</td>
    </tr>
    <tr>
      <th>49680</th>
      <td>49676</td>
      <td>Ultra Red Energy Drink</td>
      <td>64</td>
      <td>7</td>
      <td>14.5</td>
    </tr>
    <tr>
      <th>49686</th>
      <td>49682</td>
      <td>California Limeade</td>
      <td>98</td>
      <td>7</td>
      <td>4.3</td>
    </tr>
    <tr>
      <th>49688</th>
      <td>49684</td>
      <td>Vodka, Triple Distilled, Twist of Vanilla</td>
      <td>124</td>
      <td>5</td>
      <td>5.3</td>
    </tr>
  </tbody>
</table>
<p>7650 rows × 5 columns</p>
</div>



8. last data frame created row count: 7650


```python
# 9. Extract all information about "user_id" of 1
df_customer_1.describe()
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
      <th>user_id</th>
      <th>order_number</th>
      <th>orders_day_of_the_week</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>11.0</td>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>11.000000</td>
      <td>10.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>1.0</td>
      <td>6.000000</td>
      <td>2.636364</td>
      <td>10.090909</td>
      <td>19.000000</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.0</td>
      <td>3.316625</td>
      <td>1.286291</td>
      <td>3.477198</td>
      <td>9.030811</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1.0</td>
      <td>1.000000</td>
      <td>1.000000</td>
      <td>7.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1.0</td>
      <td>3.500000</td>
      <td>1.500000</td>
      <td>7.500000</td>
      <td>14.250000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>1.0</td>
      <td>6.000000</td>
      <td>3.000000</td>
      <td>8.000000</td>
      <td>19.500000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>1.0</td>
      <td>8.500000</td>
      <td>4.000000</td>
      <td>13.000000</td>
      <td>26.250000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>1.0</td>
      <td>11.000000</td>
      <td>4.000000</td>
      <td>16.000000</td>
      <td>30.000000</td>
    </tr>
  </tbody>
</table>
</div>



Based on this dataframe we can get to the conclusion that this customer orders from Monday to Thursday and never on Fri, Sat or Sun. Aslo we can see "customer #1' has never ordered later than 4pm (16) most orders are made around 10am. Finally we can see those orders are very spaced out in time. The shortest number of days between orders ia 14 and the longest 30. 


```python
df_ords.to_csv(os.path.join(path, '02 Data','Prepared Data', 'orders_wrangled.csv'))
```


```python
df_dep_t_new.to_csv(os.path.join(path, '02 Data','Prepared Data', 'departments_wrangled.csv'))
```


```python

```
