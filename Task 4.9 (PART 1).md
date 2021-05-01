```python
# Import analysis libraries
import pandas as pd
import numpy as np
import os
import matplotlib.pyplot as plt
import seaborn as sns
import scipy
```


```python
# Import customers dataframe
df = pd.read_csv(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Original Data/customers.csv',index_col = False)
```


```python
# create a path to make following steps easier
path = r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3'
```

# 4. Wrangle data.


```python
# check column names
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
      <th>user_id</th>
      <th>First Name</th>
      <th>Surnam</th>
      <th>Gender</th>
      <th>STATE</th>
      <th>Age</th>
      <th>date_joined</th>
      <th>n_dependants</th>
      <th>fam_status</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>26711</td>
      <td>Deborah</td>
      <td>Esquivel</td>
      <td>Female</td>
      <td>Missouri</td>
      <td>48</td>
      <td>1/1/2017</td>
      <td>3</td>
      <td>married</td>
      <td>165665</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33890</td>
      <td>Patricia</td>
      <td>Hart</td>
      <td>Female</td>
      <td>New Mexico</td>
      <td>36</td>
      <td>1/1/2017</td>
      <td>0</td>
      <td>single</td>
      <td>59285</td>
    </tr>
    <tr>
      <th>2</th>
      <td>65803</td>
      <td>Kenneth</td>
      <td>Farley</td>
      <td>Male</td>
      <td>Idaho</td>
      <td>35</td>
      <td>1/1/2017</td>
      <td>2</td>
      <td>married</td>
      <td>99568</td>
    </tr>
    <tr>
      <th>3</th>
      <td>125935</td>
      <td>Michelle</td>
      <td>Hicks</td>
      <td>Female</td>
      <td>Iowa</td>
      <td>40</td>
      <td>1/1/2017</td>
      <td>0</td>
      <td>single</td>
      <td>42049</td>
    </tr>
    <tr>
      <th>4</th>
      <td>130797</td>
      <td>Ann</td>
      <td>Gilmore</td>
      <td>Female</td>
      <td>Maryland</td>
      <td>26</td>
      <td>1/1/2017</td>
      <td>1</td>
      <td>married</td>
      <td>40374</td>
    </tr>
  </tbody>
</table>
</div>



I will drop 'First Name',Surnam' and 'Gender' as they do not add anything to the analysis. After checking the rest of the task (part2) requirements and the task for exercise 10 it looks like all the remaining columns will be needed for the final analyis therefore only those three can be dropped.

I also will change 'n_dependants' for 'number_of_dependants'

'fam_status' for 'family_status' and 'income' for 'annual_income'


```python
# Dropping columns
df = df.drop(columns = ['First Name','Surnam','Gender'])
```


```python
# Changing column names
df.rename(columns = {'n_dependants':'number_of_dependants','fam_status':'family_status','income':'annual_income'}, inplace = True)
```


```python
# Check dropped and new named columns
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
      <th>user_id</th>
      <th>STATE</th>
      <th>Age</th>
      <th>date_joined</th>
      <th>number_of_dependants</th>
      <th>family_status</th>
      <th>annual_income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>26711</td>
      <td>Missouri</td>
      <td>48</td>
      <td>1/1/2017</td>
      <td>3</td>
      <td>married</td>
      <td>165665</td>
    </tr>
    <tr>
      <th>1</th>
      <td>33890</td>
      <td>New Mexico</td>
      <td>36</td>
      <td>1/1/2017</td>
      <td>0</td>
      <td>single</td>
      <td>59285</td>
    </tr>
    <tr>
      <th>2</th>
      <td>65803</td>
      <td>Idaho</td>
      <td>35</td>
      <td>1/1/2017</td>
      <td>2</td>
      <td>married</td>
      <td>99568</td>
    </tr>
    <tr>
      <th>3</th>
      <td>125935</td>
      <td>Iowa</td>
      <td>40</td>
      <td>1/1/2017</td>
      <td>0</td>
      <td>single</td>
      <td>42049</td>
    </tr>
    <tr>
      <th>4</th>
      <td>130797</td>
      <td>Maryland</td>
      <td>26</td>
      <td>1/1/2017</td>
      <td>1</td>
      <td>married</td>
      <td>40374</td>
    </tr>
  </tbody>
</table>
</div>



# 5. Check for Quality and Consistency


```python
# Check and convert any mixed-type data

for col in df.columns.tolist():
  weird = (df[[col]].applymap(type) != df[[col]].iloc[0].apply(type)).any(axis = 1)
  if len (df[weird]) > 0:
    print (col)
```

By using the the above comand we see there isn't mixed-type data in this dataframe


```python
# Finding and addressing any missing values

df.isnull().sum()
```




    user_id                 0
    STATE                   0
    Age                     0
    date_joined             0
    number_of_dependants    0
    family_status           0
    annual_income           0
    dtype: int64



By using the above comand we see there aren't any missing values


```python
# Find and addressing duplicates
# We create a subset containig only duplicates

df_dups = df[df.duplicated()]
```


```python
df_dups
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
      <th>STATE</th>
      <th>Age</th>
      <th>date_joined</th>
      <th>number_of_dependants</th>
      <th>family_status</th>
      <th>annual_income</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>



By using the above comand we see there aren't any duplicates (the subset has no duplicate rows)

# 6. Combine customer data with rest of prepared data


```python
# First we will export prepared customer dataframe

df.to_csv(os.path.join(path, '02 Data','Prepared Data','customers_prepared.csv'))
```

Import Already Prepared data and new prepared data (customers_prepared.csv)


```python
# Import Instacart prepared data 
df1 = pd.read_pickle(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/ords_prods_merge8.pkl')
```


```python
df1.head()
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
      <th>order_number</th>
      <th>order_day_of_week</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
      <th>product_id</th>
      <th>product_name</th>
      <th>department_id</th>
      <th>prices</th>
      <th>price_range_loc</th>
      <th>busiest_days</th>
      <th>busiest_period_of_day</th>
      <th>max_order</th>
      <th>loyalty_flag</th>
      <th>mean_spend</th>
      <th>spend_flag</th>
      <th>median_ordering</th>
      <th>frequency_flag</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2539329</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>Mid-range product</td>
      <td>Regularly busy</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
      <td>6</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2398795</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>7</td>
      <td>15.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>Mid-range product</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
      <td>6</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
    </tr>
    <tr>
      <th>2</th>
      <td>473747</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>12</td>
      <td>21.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>Mid-range product</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
      <td>New customer</td>
      <td>6</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2254736</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>7</td>
      <td>29.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>Mid-range product</td>
      <td>Slowest days</td>
      <td>Average Orders</td>
      <td>10</td>
      <td>New customer</td>
      <td>6</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
    </tr>
    <tr>
      <th>4</th>
      <td>431534</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>15</td>
      <td>28.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>Mid-range product</td>
      <td>Slowest days</td>
      <td>Most Orders</td>
      <td>10</td>
      <td>New customer</td>
      <td>6</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
    </tr>
  </tbody>
</table>
</div>




```python
# By looking at both Df, only user_id is a link to create a merge
df3_merged = df1.merge(df, on = 'user_id', indicator = True)
```


```python
# Export the new dataframe
df3_merged.to_pickle(os.path.join(r'/Users/jlsanabria77/Desktop/17-02.2021 Instacat Basket Analysis 3/02 Data/Prepared Data/ords_prods_merged88.pkl'))
```


```python
df3_merged.head()
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
      <th>order_number</th>
      <th>order_day_of_week</th>
      <th>order_hour_of_day</th>
      <th>days_since_prior_order</th>
      <th>product_id</th>
      <th>product_name</th>
      <th>department_id</th>
      <th>prices</th>
      <th>...</th>
      <th>spend_flag</th>
      <th>median_ordering</th>
      <th>frequency_flag</th>
      <th>STATE</th>
      <th>Age</th>
      <th>date_joined</th>
      <th>number_of_dependants</th>
      <th>family_status</th>
      <th>annual_income</th>
      <th>_merge</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2539329</td>
      <td>1</td>
      <td>1</td>
      <td>2</td>
      <td>8</td>
      <td>NaN</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>...</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
      <td>Alabama</td>
      <td>31</td>
      <td>2/17/2019</td>
      <td>3</td>
      <td>married</td>
      <td>40423</td>
      <td>both</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2398795</td>
      <td>1</td>
      <td>2</td>
      <td>3</td>
      <td>7</td>
      <td>15.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>...</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
      <td>Alabama</td>
      <td>31</td>
      <td>2/17/2019</td>
      <td>3</td>
      <td>married</td>
      <td>40423</td>
      <td>both</td>
    </tr>
    <tr>
      <th>2</th>
      <td>473747</td>
      <td>1</td>
      <td>3</td>
      <td>3</td>
      <td>12</td>
      <td>21.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>...</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
      <td>Alabama</td>
      <td>31</td>
      <td>2/17/2019</td>
      <td>3</td>
      <td>married</td>
      <td>40423</td>
      <td>both</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2254736</td>
      <td>1</td>
      <td>4</td>
      <td>4</td>
      <td>7</td>
      <td>29.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>...</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
      <td>Alabama</td>
      <td>31</td>
      <td>2/17/2019</td>
      <td>3</td>
      <td>married</td>
      <td>40423</td>
      <td>both</td>
    </tr>
    <tr>
      <th>4</th>
      <td>431534</td>
      <td>1</td>
      <td>5</td>
      <td>4</td>
      <td>15</td>
      <td>28.0</td>
      <td>196</td>
      <td>Soda</td>
      <td>7</td>
      <td>9</td>
      <td>...</td>
      <td>Low Spender</td>
      <td>20.5</td>
      <td>Non-frequent customer</td>
      <td>Alabama</td>
      <td>31</td>
      <td>2/17/2019</td>
      <td>3</td>
      <td>married</td>
      <td>40423</td>
      <td>both</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 26 columns</p>
</div>



We can see all rows from the new merged dataframe


```python
# using the "merge flag" we can see that there is a full match of values
df3_merged['_merge'].value_counts()
```




    both          17027529
    right_only           0
    left_only            0
    Name: _merge, dtype: int64


