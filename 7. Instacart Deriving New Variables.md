```python
# Import libraries
import pandas as pd
import numpy as np
import os
```


```python
ords_prods_merge = pd.read_pickle(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/orders_products_merged1.pkl')
```


```python
df = ords_prods_merge[:1000000]
```


```python
df.shape
```




    (1000000, 16)




```python
df.head()
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
      <th>product_id</th>
      <th>add_to_cart_order</th>
      <th>reordered</th>
      <th>Unnamed: 0</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
      <th>_merge</th>
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
      <td>196</td>
      <td>1</td>
      <td>0</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Define the Function

def price_label(row):

  if row['prices'] <= 5:
    return 'Low-range product'
  elif (row['prices'] > 5) and (row['prices'] <= 15):
    return 'Mid-range product'
  elif row['prices'] > 15:
    return 'High range'
  else: return 'Not enough data'
```


```python
# Apply the Function
df['price_range'] = df.apply(price_label, axis=1)
```

    <ipython-input-7-8e36d5c14d44>:2: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      df['price_range'] = df.apply(price_label, axis=1)



```python
df['price_range'].value_counts(dropna = False)
```




    Mid-range product    756450
    Low-range product    243550
    Name: price_range, dtype: int64




```python
df['prices'].max()
```




    14.8




```python
df.loc[df['prices'] > 15, 'price_range_loc'] = 'High-range product'
```

    /Users/jlsanabria77/opt/anaconda3/lib/python3.8/site-packages/pandas/core/indexing.py:1596: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self.obj[key] = _infer_fill_value(value)
    /Users/jlsanabria77/opt/anaconda3/lib/python3.8/site-packages/pandas/core/indexing.py:1765: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      isetter(loc, value)



```python
df.loc[(df['prices'] <= 15) & (df['prices'] > 5), 'price_range_loc'] = 'Mid-range product'
```

    /Users/jlsanabria77/opt/anaconda3/lib/python3.8/site-packages/pandas/core/indexing.py:1765: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      isetter(loc, value)



```python
df.loc[df['prices'] <= 5, 'price_range_loc'] = 'Low-range product'
```

    /Users/jlsanabria77/opt/anaconda3/lib/python3.8/site-packages/pandas/core/indexing.py:1765: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: https://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      isetter(loc, value)



```python
df['price_range_loc'].value_counts(dropna = False)
```




    Mid-range product    756450
    Low-range product    243550
    Name: price_range_loc, dtype: int64




```python
ords_prods_merge.loc[ords_prods_merge['prices'] > 15, 'price_range_loc'] = 'High-range product'
```


```python
ords_prods_merge.loc[(ords_prods_merge['prices'] <= 15) & (df['prices'] > 5), 'price_range_loc'] = 'Mid-range product'
```


```python
ords_prods_merge.loc[ords_prods_merge['prices'] <= 5, 'price_range_loc'] = 'Low-range product'
```


```python
ords_prods_merge['price_range_loc'].value_counts(dropna = False)
```




    NaN                   21104410
    Low-range product     10126321
    Mid-range product       756450
    High-range product      417678
    Name: price_range_loc, dtype: int64




```python
for x in range(30, 45):
    print("My age is %d" % (x))
```

    My age is 30
    My age is 31
    My age is 32
    My age is 33
    My age is 34
    My age is 35
    My age is 36
    My age is 37
    My age is 38
    My age is 39
    My age is 40
    My age is 41
    My age is 42
    My age is 43
    My age is 44



```python
ords_prods_merge['order_dow'].value_counts(dropna = False)
```




    0    6204182
    1    5660230
    6    4496490
    2    4213830
    5    4205791
    3    3840534
    4    3783802
    Name: order_dow, dtype: int64




```python
result = []

for value in ords_prods_merge["order_dow"]:
  if value == 0:
    result.append("Busiest day")
  elif value == 4:
    result.append("Least busy")
  else:
    result.append("Regularly busy")
```


```python
result
```




    ['Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Busiest day',
     'Busiest day',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Least busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Least busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest day',
     'Busiest day',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     ...]




```python
ords_prods_merge['busiest_day'] = result
```


```python
ords_prods_merge['busiest_day'].value_counts(dropna = False)
```




    Regularly busy    22416875
    Busiest day        6204182
    Least busy         3783802
    Name: busiest_day, dtype: int64



# TASK 4.7

2. Change the Column to "Busiest days"


```python
# we will find the two busiest and slowest days.
ords_prods_merge['order_dow'].value_counts(dropna = False)
```




    0    6204182
    1    5660230
    6    4496490
    2    4213830
    5    4205791
    3    3840534
    4    3783802
    Name: order_dow, dtype: int64



-The two busiest days are 0 (Sunday) & 1 (Monday)

-The two slowest days are 3 (Wednesday) & 4 (Thursday)


```python
# Create a new column with 'two_busiest' and 'two_slowest'
result = []

for value in ords_prods_merge["order_dow"]:
  if value == 0 or value == 1:
    result.append("Busiest days")
  elif value == 3 or value == 4:
    result.append("Slowest days")
  else:
    result.append("Regularly busy")
```


```python
result
```




    ['Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Regularly busy',
     'Slowest days',
     'Slowest days',
     'Slowest days',
     'Busiest days',
     'Regularly busy',
     'Slowest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Busiest days',
     'Slowest days',
     'Busiest days',
     ...]




```python
ords_prods_merge['busiest_days'] = result
```


```python
ords_prods_merge['busiest_days'].value_counts(dropna = False)
```




    Regularly busy    12916111
    Busiest days      11864412
    Slowest days       7624336
    Name: busiest_days, dtype: int64




```python
# Check the new column has been created.
ords_prods_merge.head()
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
      <th>product_id</th>
      <th>add_to_cart_order</th>
      <th>reordered</th>
      <th>Unnamed: 0</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
      <th>_merge</th>
      <th>price_range_loc</th>
      <th>busiest_day</th>
      <th>busiest_days</th>
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
      <td>196</td>
      <td>1</td>
      <td>0</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
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
      <td>196</td>
      <td>1</td>
      <td>1</td>
      <td>195</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
    </tr>
  </tbody>
</table>
</div>



### 3. By comparing both frequencies from both columns we can see that the sum of Sunday and Monday equals the frequency for "busiest days"

### 4. Create a new column called "busiest_period_of_day"


```python
# First we will print the frequency to find out which are the busiest hours of the day.
ords_prods_merge['order_hour_of_day'].value_counts(dropna = False)
```




    10    2761760
    11    2736140
    14    2689136
    15    2662144
    13    2660954
    12    2618532
    16    2535202
    9     2454203
    17    2087654
    8     1718118
    18    1636502
    19    1258305
    20     976156
    7      891054
    21     795637
    22     634225
    23     402316
    6      290493
    0      218769
    1      115700
    5       87961
    2       69375
    4       53242
    3       51281
    Name: order_hour_of_day, dtype: int64



By looking at the frequency we can see that the period with most orders is is from 9h to 16h
The period with fewest orders is between midnight to 6am.


```python
# We will create a new column containing these labels.
result = []

for value in ords_prods_merge["order_hour_of_day"]:
  if value >= 9  and value <= 16:
    result.append("Most Orders")
  elif value >= 0 and value <= 6:
    result.append("Fewest Orders")
  else:
    result.append("Average Orders")
```


```python
# Let's check the values
result
```




    ['Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Fewest Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Fewest Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Fewest Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Fewest Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Fewest Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Most Orders',
     'Average Orders',
     ...]




```python
# we create a new column "busiest_period_of_day"
ords_prods_merge['busiest_period_of_day'] = result
```

### 5. Print the frequency for this new column.


```python
# We print the frequency for this column to check the results
ords_prods_merge['busiest_period_of_day'].value_counts(dropna = False)
```




    Most Orders       21118071
    Average Orders    10399967
    Fewest Orders       886821
    Name: busiest_period_of_day, dtype: int64




```python
# Export dataframe as pikle file to "Prepared Data" folder
ords_prods_merge.to_pickle(os.path.join(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/ords_prods_merge.pkl'))
```


```python

```
