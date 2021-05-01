```python
# Import libraries

import pandas as pd
import numpy as np
import os
```


```python
ords_prods_merge = pd.read_pickle(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/ords_prods_merge.pkl')
```


```python
ords_prods_merge.groupby('department_id').agg({'order_number': ['mean']})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th>order_number</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
    </tr>
    <tr>
      <th>department_id</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>15.457838</td>
    </tr>
    <tr>
      <th>2</th>
      <td>17.277920</td>
    </tr>
    <tr>
      <th>3</th>
      <td>17.170395</td>
    </tr>
    <tr>
      <th>4</th>
      <td>17.811403</td>
    </tr>
    <tr>
      <th>5</th>
      <td>15.215751</td>
    </tr>
    <tr>
      <th>6</th>
      <td>16.439806</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17.225802</td>
    </tr>
    <tr>
      <th>8</th>
      <td>15.340650</td>
    </tr>
    <tr>
      <th>9</th>
      <td>15.895474</td>
    </tr>
    <tr>
      <th>10</th>
      <td>20.197148</td>
    </tr>
    <tr>
      <th>11</th>
      <td>16.170638</td>
    </tr>
    <tr>
      <th>12</th>
      <td>15.887671</td>
    </tr>
    <tr>
      <th>13</th>
      <td>16.583536</td>
    </tr>
    <tr>
      <th>14</th>
      <td>16.773669</td>
    </tr>
    <tr>
      <th>15</th>
      <td>16.165037</td>
    </tr>
    <tr>
      <th>16</th>
      <td>17.665606</td>
    </tr>
    <tr>
      <th>17</th>
      <td>15.694469</td>
    </tr>
    <tr>
      <th>18</th>
      <td>19.310397</td>
    </tr>
    <tr>
      <th>19</th>
      <td>17.177343</td>
    </tr>
    <tr>
      <th>20</th>
      <td>16.473447</td>
    </tr>
    <tr>
      <th>21</th>
      <td>22.902379</td>
    </tr>
  </tbody>
</table>
</div>



3. When analyzing the results there are few aspects worth to mention. First the enire dataframe produces 21 departments while the subset only showed eight. Also When looking at the mean from each deapartment we can see that those are slightly lower. For example, department_id 7 has a mean of 17.472355 in the subset but a mean of 17.225802 in the entire dataframe.

2. Create a Loyalty flag


```python
# 1st. I will split the data into groups based on the “user_id” column.
# 2nd. I will apply the transform() function on the “order_number” column to generate the maximum orders for each user.
# 3rd. I will create a new column, “max_order,” into which I will place the results of the aggregation.

ords_prods_merge['max_order'] = ords_prods_merge.groupby(['user_id'])['order_number'].transform(np.max)
```


```python
# Check the new column has been created
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
      <th>...</th>
      <th>product_name</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
      <th>_merge</th>
      <th>price_range_loc</th>
      <th>busiest_day</th>
      <th>busiest_days</th>
      <th>busiest_period_of_day</th>
      <th>max_order</th>
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
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Average Orders</td>
      <td>10</td>
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
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
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
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
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
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
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
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 21 columns</p>
</div>



Create a flag that assigns a “loyalty” label to a user ID based on its corresponding max order value


```python
ords_prods_merge.loc[ords_prods_merge['max_order'] > 40, 'loyalty_flag'] = 'Loyal customer'
```


```python
ords_prods_merge.loc[(ords_prods_merge['max_order'] <= 40) & (ords_prods_merge['max_order'] > 10), 'loyalty_flag'] = 'Regular customer'
```


```python
ords_prods_merge.loc[ords_prods_merge['max_order'] <= 10, 'loyalty_flag'] = 'New customer'
```


```python
ords_prods_merge['loyalty_flag'].value_counts(dropna = False)
```




    Regular customer    15876776
    Loyal customer      10284093
    New customer         6243990
    Name: loyalty_flag, dtype: int64



5. Determine whether prices of products purchased by loyal customers differ from those purchased by regular or new customers


```python
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
      <th>...</th>
      <th>aisle_id</th>
      <th>department_id</th>
      <th>prices</th>
      <th>_merge</th>
      <th>price_range_loc</th>
      <th>busiest_day</th>
      <th>busiest_days</th>
      <th>busiest_period_of_day</th>
      <th>max_order</th>
      <th>loyalty_flag</th>
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
      <td>...</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
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
      <td>...</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
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
      <td>...</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
      <td>New customer</td>
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
      <td>...</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
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
      <td>...</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
      <td>New customer</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>




```python
# By using the groupby I will do multiple aggregations to find out the maximum, minimum and average price of products bought by these three type of customers
ords_prods_merge.groupby('loyalty_flag').agg({'prices': ['mean','max','min']})
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead tr th {
        text-align: left;
    }

    .dataframe thead tr:last-of-type th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr>
      <th></th>
      <th colspan="3" halign="left">prices</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>max</th>
      <th>min</th>
    </tr>
    <tr>
      <th>loyalty_flag</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Loyal customer</th>
      <td>10.386336</td>
      <td>99999.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>New customer</th>
      <td>13.294670</td>
      <td>99999.0</td>
      <td>1.0</td>
    </tr>
    <tr>
      <th>Regular customer</th>
      <td>12.495717</td>
      <td>99999.0</td>
      <td>1.0</td>
    </tr>
  </tbody>
</table>
</div>



We can see that all three groups buy from the cheapest (1.0) to the most expensive (99999.0) product. 
Also we observe that Loyal Customers buy on average less expensive products than the other two groups. 

6. Create a spending flag for each user based on the average price across all their orders using the following criteria:


```python
# 1st. I will create a column of mean spend by user_id
ords_prods_merge['mean_spend'] = ords_prods_merge.groupby(['user_id'])['prices'].transform(np.mean)
```


```python
# 2nd. I will create a spend flag for "Low Spender"
ords_prods_merge.loc[ords_prods_merge['mean_spend'] < 10, 'spend_flag'] = 'Low Spender'
```


```python
# 3rd. I will create a spend flag for "High Spender"
ords_prods_merge.loc[ords_prods_merge['mean_spend'] >= 10, 'spend_flag'] = 'High Spender'
```


```python
# 4th. I will check all values 
ords_prods_merge['spend_flag'].value_counts(dropna = False)
```

7. Determine frequent versus non-frequent customers. Create an order frequency flag that marks the regularity of a user’s ordering behavior according to the median in the “days_since_prior_order” column.


```python
# 1st. I will create a column of median for days_since_prior_order column
ords_prods_merge['median_ordering'] = ords_prods_merge.groupby(['user_id'])['days_since_prior_order'].transform(np.median)
```


```python
# 2nd. I will create a frequency flag for "Non-frequent-customer"
ords_prods_merge.loc[ords_prods_merge['median_ordering'] > 20, 'frequency_flag'] = 'Non-frequent customer'
```


```python
# 3th. I will create a frequency flag for "Regular customer"
ords_prods_merge.loc[(ords_prods_merge['median_ordering'] > 10) & (ords_prods_merge['median_ordering'] <= 20), 'frequency_flag'] = 'Regular customer'
```


```python
# 4th. I will create a frequenct flag for "Frequent customer"
ords_prods_merge.loc[ords_prods_merge['median_ordering'] <= 10, 'frequency_flag'] = 'Frequent customer'
```


```python
# 5th. I will check all values
ords_prods_merge['frequency_flag'].value_counts(dropna = False)
```


```python
# Export dataframe as pikle file to "Prepared Data" folder
ords_prods_merge.to_pickle(os.path.join(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/ords_prods_merge.pkl'))
```
