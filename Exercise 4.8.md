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
df = ords_prods_merge[:1000000]
```


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
      <th>price_range_loc</th>
      <th>busiest_day</th>
      <th>busiest_days</th>
      <th>busiest_period_of_day</th>
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
      <td>Average Orders</td>
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
      <td>Average Orders</td>
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
      <td>Most Orders</td>
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
      <td>Average Orders</td>
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
      <td>Most Orders</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('product_name')
```




    <pandas.core.groupby.generic.DataFrameGroupBy object at 0x1043ef9a0>




```python
df.groupby('department_id').agg({'order_number': ['mean']})
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
      <th>4</th>
      <td>18.825780</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17.472355</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17.993423</td>
    </tr>
    <tr>
      <th>14</th>
      <td>19.246334</td>
    </tr>
    <tr>
      <th>16</th>
      <td>19.463012</td>
    </tr>
    <tr>
      <th>17</th>
      <td>11.294069</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19.305237</td>
    </tr>
    <tr>
      <th>20</th>
      <td>17.599636</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.groupby('department_id')['order_number'].mean()
```




    department_id
    4     18.825780
    7     17.472355
    13    17.993423
    14    19.246334
    16    19.463012
    17    11.294069
    19    19.305237
    20    17.599636
    Name: order_number, dtype: float64




```python
df.groupby('department_id').agg({'order_number': ['mean', 'min', 'max']})

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
      <th colspan="3" halign="left">order_number</th>
    </tr>
    <tr>
      <th></th>
      <th>mean</th>
      <th>min</th>
      <th>max</th>
    </tr>
    <tr>
      <th>department_id</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>4</th>
      <td>18.825780</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>7</th>
      <td>17.472355</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>13</th>
      <td>17.993423</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>14</th>
      <td>19.246334</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>16</th>
      <td>19.463012</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>17</th>
      <td>11.294069</td>
      <td>1</td>
      <td>98</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19.305237</td>
      <td>1</td>
      <td>99</td>
    </tr>
    <tr>
      <th>20</th>
      <td>17.599636</td>
      <td>1</td>
      <td>99</td>
    </tr>
  </tbody>
</table>
</div>



2. Create a loyalty flag


```python
# Split the data into groups based on the “user_id” column.
# Apply the transform() function on the “order_number” column to generate the maximum orders for each user.
# Create a new column, “max_order,” into which you’ll place the results of your aggregation.

ords_prods_merge['max_order'] = ords_prods_merge.groupby(['user_id'])['order_number'].transform(np.max)
```


```python
ords_prods_merge.head(100)
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
    <tr>
      <th>5</th>
      <td>3367565</td>
      <td>1</td>
      <td>prior</td>
      <td>6</td>
      <td>2</td>
      <td>7</td>
      <td>19.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Average Orders</td>
      <td>10</td>
    </tr>
    <tr>
      <th>6</th>
      <td>550135</td>
      <td>1</td>
      <td>prior</td>
      <td>7</td>
      <td>1</td>
      <td>9</td>
      <td>20.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>10</td>
    </tr>
    <tr>
      <th>7</th>
      <td>3108588</td>
      <td>1</td>
      <td>prior</td>
      <td>8</td>
      <td>1</td>
      <td>14</td>
      <td>14.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>10</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2295261</td>
      <td>1</td>
      <td>prior</td>
      <td>9</td>
      <td>1</td>
      <td>16</td>
      <td>0.0</td>
      <td>196</td>
      <td>4</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2550362</td>
      <td>1</td>
      <td>prior</td>
      <td>10</td>
      <td>4</td>
      <td>8</td>
      <td>30.0</td>
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
      <th>10</th>
      <td>2968173</td>
      <td>15</td>
      <td>prior</td>
      <td>15</td>
      <td>1</td>
      <td>9</td>
      <td>7.0</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1870022</td>
      <td>15</td>
      <td>prior</td>
      <td>17</td>
      <td>2</td>
      <td>16</td>
      <td>8.0</td>
      <td>196</td>
      <td>6</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1911383</td>
      <td>15</td>
      <td>prior</td>
      <td>18</td>
      <td>2</td>
      <td>11</td>
      <td>7.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2715276</td>
      <td>15</td>
      <td>prior</td>
      <td>21</td>
      <td>1</td>
      <td>9</td>
      <td>7.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>14</th>
      <td>487368</td>
      <td>15</td>
      <td>prior</td>
      <td>22</td>
      <td>1</td>
      <td>10</td>
      <td>14.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2293453</td>
      <td>19</td>
      <td>prior</td>
      <td>2</td>
      <td>5</td>
      <td>14</td>
      <td>6.0</td>
      <td>196</td>
      <td>3</td>
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
      <td>Most Orders</td>
      <td>9</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1973799</td>
      <td>19</td>
      <td>prior</td>
      <td>5</td>
      <td>6</td>
      <td>12</td>
      <td>8.0</td>
      <td>196</td>
      <td>15</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>9</td>
    </tr>
    <tr>
      <th>17</th>
      <td>532817</td>
      <td>19</td>
      <td>prior</td>
      <td>7</td>
      <td>4</td>
      <td>17</td>
      <td>6.0</td>
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
      <td>9</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1573906</td>
      <td>21</td>
      <td>prior</td>
      <td>10</td>
      <td>3</td>
      <td>10</td>
      <td>6.0</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
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
      <td>33</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1593000</td>
      <td>31</td>
      <td>prior</td>
      <td>10</td>
      <td>3</td>
      <td>8</td>
      <td>7.0</td>
      <td>196</td>
      <td>17</td>
      <td>0</td>
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
      <td>20</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2231262</td>
      <td>31</td>
      <td>prior</td>
      <td>17</td>
      <td>3</td>
      <td>11</td>
      <td>8.0</td>
      <td>196</td>
      <td>14</td>
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
      <td>20</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2580647</td>
      <td>43</td>
      <td>prior</td>
      <td>6</td>
      <td>4</td>
      <td>16</td>
      <td>4.0</td>
      <td>196</td>
      <td>9</td>
      <td>0</td>
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
      <td>11</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2187180</td>
      <td>43</td>
      <td>prior</td>
      <td>9</td>
      <td>4</td>
      <td>12</td>
      <td>3.0</td>
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
      <td>11</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2497897</td>
      <td>52</td>
      <td>prior</td>
      <td>1</td>
      <td>1</td>
      <td>9</td>
      <td>NaN</td>
      <td>196</td>
      <td>4</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1318871</td>
      <td>52</td>
      <td>prior</td>
      <td>2</td>
      <td>1</td>
      <td>10</td>
      <td>7.0</td>
      <td>196</td>
      <td>5</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1261384</td>
      <td>52</td>
      <td>prior</td>
      <td>3</td>
      <td>1</td>
      <td>10</td>
      <td>7.0</td>
      <td>196</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>26</th>
      <td>580568</td>
      <td>52</td>
      <td>prior</td>
      <td>5</td>
      <td>2</td>
      <td>10</td>
      <td>8.0</td>
      <td>196</td>
      <td>6</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2428073</td>
      <td>52</td>
      <td>prior</td>
      <td>7</td>
      <td>2</td>
      <td>7</td>
      <td>8.0</td>
      <td>196</td>
      <td>5</td>
      <td>1</td>
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
      <td>27</td>
    </tr>
    <tr>
      <th>28</th>
      <td>342306</td>
      <td>52</td>
      <td>prior</td>
      <td>9</td>
      <td>1</td>
      <td>11</td>
      <td>7.0</td>
      <td>196</td>
      <td>5</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1520353</td>
      <td>52</td>
      <td>prior</td>
      <td>10</td>
      <td>2</td>
      <td>10</td>
      <td>8.0</td>
      <td>196</td>
      <td>4</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2542086</td>
      <td>52</td>
      <td>prior</td>
      <td>11</td>
      <td>2</td>
      <td>9</td>
      <td>7.0</td>
      <td>196</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>31</th>
      <td>944694</td>
      <td>52</td>
      <td>prior</td>
      <td>12</td>
      <td>1</td>
      <td>16</td>
      <td>6.0</td>
      <td>196</td>
      <td>7</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>32</th>
      <td>1268191</td>
      <td>52</td>
      <td>prior</td>
      <td>15</td>
      <td>2</td>
      <td>11</td>
      <td>8.0</td>
      <td>196</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>33</th>
      <td>1122089</td>
      <td>52</td>
      <td>prior</td>
      <td>17</td>
      <td>2</td>
      <td>10</td>
      <td>6.0</td>
      <td>196</td>
      <td>4</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>34</th>
      <td>1498922</td>
      <td>52</td>
      <td>prior</td>
      <td>18</td>
      <td>2</td>
      <td>10</td>
      <td>14.0</td>
      <td>196</td>
      <td>6</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>35</th>
      <td>180919</td>
      <td>52</td>
      <td>prior</td>
      <td>19</td>
      <td>3</td>
      <td>8</td>
      <td>8.0</td>
      <td>196</td>
      <td>4</td>
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
      <td>27</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2695875</td>
      <td>52</td>
      <td>prior</td>
      <td>21</td>
      <td>5</td>
      <td>10</td>
      <td>30.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>27</td>
    </tr>
    <tr>
      <th>37</th>
      <td>3205960</td>
      <td>67</td>
      <td>prior</td>
      <td>1</td>
      <td>3</td>
      <td>11</td>
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
      <td>Slowest day</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>38</th>
      <td>970922</td>
      <td>67</td>
      <td>prior</td>
      <td>2</td>
      <td>1</td>
      <td>15</td>
      <td>5.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>39</th>
      <td>596585</td>
      <td>67</td>
      <td>prior</td>
      <td>3</td>
      <td>1</td>
      <td>13</td>
      <td>7.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2037087</td>
      <td>67</td>
      <td>prior</td>
      <td>4</td>
      <td>2</td>
      <td>9</td>
      <td>8.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2474111</td>
      <td>67</td>
      <td>prior</td>
      <td>5</td>
      <td>3</td>
      <td>14</td>
      <td>8.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>24</td>
    </tr>
    <tr>
      <th>42</th>
      <td>1568481</td>
      <td>67</td>
      <td>prior</td>
      <td>6</td>
      <td>3</td>
      <td>12</td>
      <td>7.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>24</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2048527</td>
      <td>67</td>
      <td>prior</td>
      <td>8</td>
      <td>2</td>
      <td>11</td>
      <td>7.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2389031</td>
      <td>67</td>
      <td>prior</td>
      <td>9</td>
      <td>2</td>
      <td>14</td>
      <td>7.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>45</th>
      <td>2378562</td>
      <td>67</td>
      <td>prior</td>
      <td>10</td>
      <td>1</td>
      <td>10</td>
      <td>6.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>46</th>
      <td>1515698</td>
      <td>67</td>
      <td>prior</td>
      <td>11</td>
      <td>1</td>
      <td>11</td>
      <td>7.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>47</th>
      <td>1928050</td>
      <td>67</td>
      <td>prior</td>
      <td>12</td>
      <td>2</td>
      <td>12</td>
      <td>8.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>48</th>
      <td>1949274</td>
      <td>67</td>
      <td>prior</td>
      <td>13</td>
      <td>1</td>
      <td>10</td>
      <td>6.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>49</th>
      <td>551869</td>
      <td>67</td>
      <td>prior</td>
      <td>14</td>
      <td>1</td>
      <td>9</td>
      <td>7.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>50</th>
      <td>768572</td>
      <td>67</td>
      <td>prior</td>
      <td>16</td>
      <td>4</td>
      <td>10</td>
      <td>9.0</td>
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
      <td>24</td>
    </tr>
    <tr>
      <th>51</th>
      <td>150528</td>
      <td>67</td>
      <td>prior</td>
      <td>18</td>
      <td>5</td>
      <td>16</td>
      <td>4.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>52</th>
      <td>29758</td>
      <td>67</td>
      <td>prior</td>
      <td>19</td>
      <td>0</td>
      <td>14</td>
      <td>9.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>53</th>
      <td>1558976</td>
      <td>67</td>
      <td>prior</td>
      <td>21</td>
      <td>1</td>
      <td>9</td>
      <td>5.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>54</th>
      <td>863974</td>
      <td>67</td>
      <td>prior</td>
      <td>22</td>
      <td>1</td>
      <td>11</td>
      <td>14.0</td>
      <td>196</td>
      <td>3</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>55</th>
      <td>2308399</td>
      <td>67</td>
      <td>prior</td>
      <td>23</td>
      <td>1</td>
      <td>14</td>
      <td>14.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>24</td>
    </tr>
    <tr>
      <th>56</th>
      <td>2759128</td>
      <td>81</td>
      <td>prior</td>
      <td>3</td>
      <td>1</td>
      <td>9</td>
      <td>14.0</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>7</td>
    </tr>
    <tr>
      <th>57</th>
      <td>1812985</td>
      <td>81</td>
      <td>prior</td>
      <td>5</td>
      <td>2</td>
      <td>20</td>
      <td>30.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Average Orders</td>
      <td>7</td>
    </tr>
    <tr>
      <th>58</th>
      <td>1889835</td>
      <td>82</td>
      <td>prior</td>
      <td>1</td>
      <td>3</td>
      <td>15</td>
      <td>NaN</td>
      <td>196</td>
      <td>6</td>
      <td>0</td>
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
      <td>19</td>
    </tr>
    <tr>
      <th>59</th>
      <td>499460</td>
      <td>82</td>
      <td>prior</td>
      <td>3</td>
      <td>5</td>
      <td>10</td>
      <td>5.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>60</th>
      <td>2728456</td>
      <td>82</td>
      <td>prior</td>
      <td>4</td>
      <td>0</td>
      <td>11</td>
      <td>16.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>61</th>
      <td>2653743</td>
      <td>82</td>
      <td>prior</td>
      <td>6</td>
      <td>4</td>
      <td>9</td>
      <td>13.0</td>
      <td>196</td>
      <td>5</td>
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
      <td>19</td>
    </tr>
    <tr>
      <th>62</th>
      <td>1358880</td>
      <td>82</td>
      <td>prior</td>
      <td>9</td>
      <td>1</td>
      <td>10</td>
      <td>30.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>63</th>
      <td>343588</td>
      <td>82</td>
      <td>prior</td>
      <td>10</td>
      <td>2</td>
      <td>11</td>
      <td>1.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>64</th>
      <td>3034663</td>
      <td>82</td>
      <td>prior</td>
      <td>15</td>
      <td>2</td>
      <td>11</td>
      <td>12.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>65</th>
      <td>147262</td>
      <td>82</td>
      <td>prior</td>
      <td>18</td>
      <td>1</td>
      <td>13</td>
      <td>7.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>66</th>
      <td>3144004</td>
      <td>82</td>
      <td>prior</td>
      <td>19</td>
      <td>2</td>
      <td>15</td>
      <td>8.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>19</td>
    </tr>
    <tr>
      <th>67</th>
      <td>2126069</td>
      <td>98</td>
      <td>prior</td>
      <td>3</td>
      <td>0</td>
      <td>9</td>
      <td>25.0</td>
      <td>196</td>
      <td>7</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>14</td>
    </tr>
    <tr>
      <th>68</th>
      <td>2210120</td>
      <td>98</td>
      <td>prior</td>
      <td>7</td>
      <td>5</td>
      <td>14</td>
      <td>5.0</td>
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
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>14</td>
    </tr>
    <tr>
      <th>69</th>
      <td>681011</td>
      <td>98</td>
      <td>prior</td>
      <td>9</td>
      <td>3</td>
      <td>9</td>
      <td>30.0</td>
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
      <td>14</td>
    </tr>
    <tr>
      <th>70</th>
      <td>2846344</td>
      <td>98</td>
      <td>prior</td>
      <td>11</td>
      <td>4</td>
      <td>13</td>
      <td>15.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>14</td>
    </tr>
    <tr>
      <th>71</th>
      <td>747431</td>
      <td>98</td>
      <td>prior</td>
      <td>12</td>
      <td>6</td>
      <td>13</td>
      <td>30.0</td>
      <td>196</td>
      <td>4</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>14</td>
    </tr>
    <tr>
      <th>72</th>
      <td>2383054</td>
      <td>98</td>
      <td>prior</td>
      <td>13</td>
      <td>4</td>
      <td>11</td>
      <td>30.0</td>
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
      <td>14</td>
    </tr>
    <tr>
      <th>73</th>
      <td>1993729</td>
      <td>98</td>
      <td>prior</td>
      <td>14</td>
      <td>5</td>
      <td>8</td>
      <td>8.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
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
      <td>14</td>
    </tr>
    <tr>
      <th>74</th>
      <td>1403849</td>
      <td>109</td>
      <td>prior</td>
      <td>3</td>
      <td>3</td>
      <td>17</td>
      <td>9.0</td>
      <td>196</td>
      <td>5</td>
      <td>0</td>
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
      <td>6</td>
    </tr>
    <tr>
      <th>75</th>
      <td>520620</td>
      <td>120</td>
      <td>prior</td>
      <td>1</td>
      <td>3</td>
      <td>11</td>
      <td>NaN</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
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
      <td>3</td>
    </tr>
    <tr>
      <th>76</th>
      <td>3273029</td>
      <td>120</td>
      <td>prior</td>
      <td>3</td>
      <td>2</td>
      <td>8</td>
      <td>19.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
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
      <td>3</td>
    </tr>
    <tr>
      <th>77</th>
      <td>1861943</td>
      <td>185</td>
      <td>prior</td>
      <td>2</td>
      <td>1</td>
      <td>12</td>
      <td>25.0</td>
      <td>196</td>
      <td>10</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>6</td>
    </tr>
    <tr>
      <th>78</th>
      <td>2040988</td>
      <td>195</td>
      <td>prior</td>
      <td>1</td>
      <td>1</td>
      <td>14</td>
      <td>NaN</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>79</th>
      <td>1680569</td>
      <td>195</td>
      <td>prior</td>
      <td>8</td>
      <td>1</td>
      <td>9</td>
      <td>4.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>80</th>
      <td>276171</td>
      <td>195</td>
      <td>prior</td>
      <td>19</td>
      <td>5</td>
      <td>11</td>
      <td>3.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>81</th>
      <td>2744976</td>
      <td>195</td>
      <td>prior</td>
      <td>22</td>
      <td>5</td>
      <td>10</td>
      <td>7.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>82</th>
      <td>2781919</td>
      <td>195</td>
      <td>prior</td>
      <td>25</td>
      <td>1</td>
      <td>14</td>
      <td>4.0</td>
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
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>83</th>
      <td>1738718</td>
      <td>195</td>
      <td>prior</td>
      <td>31</td>
      <td>2</td>
      <td>8</td>
      <td>4.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
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
      <td>58</td>
    </tr>
    <tr>
      <th>84</th>
      <td>3058369</td>
      <td>195</td>
      <td>prior</td>
      <td>34</td>
      <td>3</td>
      <td>10</td>
      <td>6.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>58</td>
    </tr>
    <tr>
      <th>85</th>
      <td>1485596</td>
      <td>195</td>
      <td>prior</td>
      <td>37</td>
      <td>2</td>
      <td>15</td>
      <td>0.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>86</th>
      <td>417035</td>
      <td>195</td>
      <td>prior</td>
      <td>40</td>
      <td>3</td>
      <td>16</td>
      <td>2.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>58</td>
    </tr>
    <tr>
      <th>87</th>
      <td>1615297</td>
      <td>195</td>
      <td>prior</td>
      <td>47</td>
      <td>5</td>
      <td>10</td>
      <td>2.0</td>
      <td>196</td>
      <td>2</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>58</td>
    </tr>
    <tr>
      <th>88</th>
      <td>1765587</td>
      <td>195</td>
      <td>prior</td>
      <td>52</td>
      <td>3</td>
      <td>12</td>
      <td>2.0</td>
      <td>196</td>
      <td>3</td>
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
      <td>58</td>
    </tr>
    <tr>
      <th>89</th>
      <td>745908</td>
      <td>195</td>
      <td>prior</td>
      <td>57</td>
      <td>4</td>
      <td>11</td>
      <td>3.0</td>
      <td>196</td>
      <td>3</td>
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
      <td>58</td>
    </tr>
    <tr>
      <th>90</th>
      <td>2505656</td>
      <td>222</td>
      <td>prior</td>
      <td>17</td>
      <td>2</td>
      <td>12</td>
      <td>1.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>Most Orders</td>
      <td>70</td>
    </tr>
    <tr>
      <th>91</th>
      <td>3268370</td>
      <td>222</td>
      <td>prior</td>
      <td>38</td>
      <td>5</td>
      <td>15</td>
      <td>1.0</td>
      <td>196</td>
      <td>6</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>70</td>
    </tr>
    <tr>
      <th>92</th>
      <td>2016711</td>
      <td>290</td>
      <td>prior</td>
      <td>9</td>
      <td>5</td>
      <td>19</td>
      <td>6.0</td>
      <td>196</td>
      <td>8</td>
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
      <td>51</td>
    </tr>
    <tr>
      <th>93</th>
      <td>2706088</td>
      <td>290</td>
      <td>prior</td>
      <td>28</td>
      <td>6</td>
      <td>10</td>
      <td>7.0</td>
      <td>196</td>
      <td>16</td>
      <td>1</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Regularly busy</td>
      <td>Most Orders</td>
      <td>51</td>
    </tr>
    <tr>
      <th>94</th>
      <td>1952286</td>
      <td>331</td>
      <td>prior</td>
      <td>6</td>
      <td>5</td>
      <td>16</td>
      <td>30.0</td>
      <td>196</td>
      <td>8</td>
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
      <td>Most Orders</td>
      <td>8</td>
    </tr>
    <tr>
      <th>95</th>
      <td>3226575</td>
      <td>360</td>
      <td>prior</td>
      <td>1</td>
      <td>5</td>
      <td>12</td>
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
      <td>Most Orders</td>
      <td>3</td>
    </tr>
    <tr>
      <th>96</th>
      <td>1469869</td>
      <td>377</td>
      <td>prior</td>
      <td>3</td>
      <td>5</td>
      <td>17</td>
      <td>3.0</td>
      <td>196</td>
      <td>9</td>
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
      <td>3</td>
    </tr>
    <tr>
      <th>97</th>
      <td>1927023</td>
      <td>387</td>
      <td>prior</td>
      <td>2</td>
      <td>4</td>
      <td>10</td>
      <td>22.0</td>
      <td>196</td>
      <td>3</td>
      <td>0</td>
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
      <td>8</td>
    </tr>
    <tr>
      <th>98</th>
      <td>858092</td>
      <td>420</td>
      <td>prior</td>
      <td>4</td>
      <td>1</td>
      <td>19</td>
      <td>30.0</td>
      <td>196</td>
      <td>2</td>
      <td>0</td>
      <td>...</td>
      <td>Soda</td>
      <td>77</td>
      <td>7</td>
      <td>9.0</td>
      <td>both</td>
      <td>Mid-range product</td>
      <td>Busiest day</td>
      <td>Busiest days</td>
      <td>Average Orders</td>
      <td>22</td>
    </tr>
    <tr>
      <th>99</th>
      <td>119314</td>
      <td>420</td>
      <td>prior</td>
      <td>5</td>
      <td>3</td>
      <td>19</td>
      <td>16.0</td>
      <td>196</td>
      <td>2</td>
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
      <td>22</td>
    </tr>
  </tbody>
</table>
<p>100 rows × 21 columns</p>
</div>




```python
pd.options.display.max_rows = None
```

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




```python
ords_prods_merge[['user_id','loyalty_flag','order_number']].head(60)
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
      <th>loyalty_flag</th>
      <th>order_number</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>New customer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>New customer</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>New customer</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>New customer</td>
      <td>4</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>New customer</td>
      <td>5</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1</td>
      <td>New customer</td>
      <td>6</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1</td>
      <td>New customer</td>
      <td>7</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1</td>
      <td>New customer</td>
      <td>8</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1</td>
      <td>New customer</td>
      <td>9</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1</td>
      <td>New customer</td>
      <td>10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>15</td>
      <td>Regular customer</td>
      <td>15</td>
    </tr>
    <tr>
      <th>11</th>
      <td>15</td>
      <td>Regular customer</td>
      <td>17</td>
    </tr>
    <tr>
      <th>12</th>
      <td>15</td>
      <td>Regular customer</td>
      <td>18</td>
    </tr>
    <tr>
      <th>13</th>
      <td>15</td>
      <td>Regular customer</td>
      <td>21</td>
    </tr>
    <tr>
      <th>14</th>
      <td>15</td>
      <td>Regular customer</td>
      <td>22</td>
    </tr>
    <tr>
      <th>15</th>
      <td>19</td>
      <td>New customer</td>
      <td>2</td>
    </tr>
    <tr>
      <th>16</th>
      <td>19</td>
      <td>New customer</td>
      <td>5</td>
    </tr>
    <tr>
      <th>17</th>
      <td>19</td>
      <td>New customer</td>
      <td>7</td>
    </tr>
    <tr>
      <th>18</th>
      <td>21</td>
      <td>Regular customer</td>
      <td>10</td>
    </tr>
    <tr>
      <th>19</th>
      <td>31</td>
      <td>Regular customer</td>
      <td>10</td>
    </tr>
    <tr>
      <th>20</th>
      <td>31</td>
      <td>Regular customer</td>
      <td>17</td>
    </tr>
    <tr>
      <th>21</th>
      <td>43</td>
      <td>Regular customer</td>
      <td>6</td>
    </tr>
    <tr>
      <th>22</th>
      <td>43</td>
      <td>Regular customer</td>
      <td>9</td>
    </tr>
    <tr>
      <th>23</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>3</td>
    </tr>
    <tr>
      <th>26</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>5</td>
    </tr>
    <tr>
      <th>27</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>7</td>
    </tr>
    <tr>
      <th>28</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>9</td>
    </tr>
    <tr>
      <th>29</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>10</td>
    </tr>
    <tr>
      <th>30</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>11</td>
    </tr>
    <tr>
      <th>31</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>12</td>
    </tr>
    <tr>
      <th>32</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>15</td>
    </tr>
    <tr>
      <th>33</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>17</td>
    </tr>
    <tr>
      <th>34</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>18</td>
    </tr>
    <tr>
      <th>35</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>19</td>
    </tr>
    <tr>
      <th>36</th>
      <td>52</td>
      <td>Regular customer</td>
      <td>21</td>
    </tr>
    <tr>
      <th>37</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>38</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>2</td>
    </tr>
    <tr>
      <th>39</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>3</td>
    </tr>
    <tr>
      <th>40</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>4</td>
    </tr>
    <tr>
      <th>41</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>5</td>
    </tr>
    <tr>
      <th>42</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>6</td>
    </tr>
    <tr>
      <th>43</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>8</td>
    </tr>
    <tr>
      <th>44</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>9</td>
    </tr>
    <tr>
      <th>45</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>10</td>
    </tr>
    <tr>
      <th>46</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>11</td>
    </tr>
    <tr>
      <th>47</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>12</td>
    </tr>
    <tr>
      <th>48</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>13</td>
    </tr>
    <tr>
      <th>49</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>14</td>
    </tr>
    <tr>
      <th>50</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>16</td>
    </tr>
    <tr>
      <th>51</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>18</td>
    </tr>
    <tr>
      <th>52</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>19</td>
    </tr>
    <tr>
      <th>53</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>21</td>
    </tr>
    <tr>
      <th>54</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>22</td>
    </tr>
    <tr>
      <th>55</th>
      <td>67</td>
      <td>Regular customer</td>
      <td>23</td>
    </tr>
    <tr>
      <th>56</th>
      <td>81</td>
      <td>New customer</td>
      <td>3</td>
    </tr>
    <tr>
      <th>57</th>
      <td>81</td>
      <td>New customer</td>
      <td>5</td>
    </tr>
    <tr>
      <th>58</th>
      <td>82</td>
      <td>Regular customer</td>
      <td>1</td>
    </tr>
    <tr>
      <th>59</th>
      <td>82</td>
      <td>Regular customer</td>
      <td>3</td>
    </tr>
  </tbody>
</table>
</div>




```python

```
