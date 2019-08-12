# Merging Dataframes with Pandas

## Chapter 3 : Merging Data

### Merging company DataFrames
          city  revenue
0       Austin      100
1       Denver       83
2  Springfield        4

        city   manager
0     Austin  Charlers
1     Denver      Joel
2  Mendocino     Brett
```python
combined = pd.merge(revenue, managers, on='city')
print(combined)
```
>>     city  revenue   manager
0  Austin      100  Charlers
1  Denver       83      Joel



### Merging on a specific column
```python
print(revenue)
print(manager)
```
>>          city  branch_id  revenue
0       Austin         10      100
1       Denver         20       83
2  Springfield         30        4
3    Mendocino         47      200
          city  branch_id  manager
0       Austin         10  Charles
1       Denver         20     Joel
2    Mendocino         47    Brett
3  Springfield         31    Sally


```python
# Merge revenue with managers on 'city': merge_by_city
merge_by_city = pd.merge(revenue, managers, on='city')

# Print merge_by_city
print(merge_by_city)
```
>>          city  branch_id_x  revenue  branch_id_y  manager
0       Austin           10      100           10  Charles
1       Denver           20       83           20     Joel
2  Springfield           30        4           31    Sally
3    Mendocino           47      200           47    Brett


```python
# Merge revenue with managers on 'branch_id': merge_by_id
merge_by_id = pd.merge(revenue, managers, on='branch_id')

# Print merge_by_id
print(merge_by_id)
```
>>          city  branch_id_x  revenue  branch_id_y  manager
0       Austin           10      100           10  Charles
1       Denver           20       83           20     Joel
2  Springfield           30        4           31    Sally
3    Mendocino           47      200           47    Brett


### Merging on columns with non-matching labels
```python
# Merge revenue & managers on 'city' & 'branch': combined
combined = pd.merge(revenue, managers, left_on='city', right_on='branch')

# Print combined
print(combined)
```
>>          city  branch_id_x state_x  revenue       branch  branch_id_y state_y   manager
0       Austin           10      TX      100       Austin           10      TX  Charlers
1       Denver           20      CO       83       Denver           20      CO      Joel
2  Springfield           30      IL        4  Springfield           31      MO     Sally
3    Mendocino           47      CA      200    Mendocino           47      CA     Brett


### Merging on multiple columns
```python
# Add 'state' column to revenue: revenue['state']
revenue['state'] = ['TX','CO','IL','CA']

# Add 'state' column to managers: managers['state']
managers['state'] = ['TX','CO','CA','MO']

# Merge revenue & managers on 'branch_id', 'city', & 'state': combined
combined = pd.merge(revenue, managers, on=['branch_id', 'city', 'state'])

# Print combined
print(combined)
```
>>        city  branch_id  revenue state   manager
0     Austin         10      100    TX  Charlers
1     Denver         20       83    CO      Joel
2  Mendocino         47      200    CA     Brett


### Joining by Index
```python
print(revenue)
print(manager)
```
>>                  city state  revenue
branch_id                            
10              Austin    TX      100
20              Denver    CO       83
30         Springfield    IL        4
47           Mendocino    CA      200

                branch state   manager
branch_id                             
10              Austin    TX  Charlers
20              Denver    CO      Joel
47           Mendocino    CA     Brett
31         Springfield    MO     Sally


```python
pd.merge(revenue, managers, on='branch_id')
```
>>                city state_x  revenue     branch state_y   manager
branch_id                                                         
10            Austin      TX      100     Austin      TX  Charlers
20            Denver      CO       83     Denver      CO      Joel
47         Mendocino      CA      200  Mendocino      CA     Brett


```python
pd.merge(managers, revenue, how='left')
```
>>        branch state   manager       city  revenue
0       Austin    TX  Charlers     Austin    100.0
1       Denver    CO      Joel     Denver     83.0
2    Mendocino    CA     Brett  Mendocino    200.0
3  Springfield    MO     Sally        NaN      NaN


```python
revenue.join(managers, lsuffix='_rev', rsuffix='_mng', how='outer')
```
>>                  city state_rev  revenue       branch state_mng   manager
branch_id                                                                 
10              Austin        TX    100.0       Austin        TX  Charlers
20              Denver        CO     83.0       Denver        CO      Joel
30         Springfield        IL      4.0          NaN       NaN       NaN
31                 NaN       NaN      NaN  Springfield        MO     Sally
47           Mendocino        CA    200.0    Mendocino        CA     Brett


```python
managers.join(revenue, lsuffix='_mgn', rsuffix='_rev', how='left')
```
>>                branch state_mgn   manager       city state_rev  revenue
branch_id                                                               
10              Austin        TX  Charlers     Austin        TX    100.0
20              Denver        CO      Joel     Denver        CO     83.0
47           Mendocino        CA     Brett  Mendocino        CA    200.0
31         Springfield        MO     Sally        NaN       NaN      NaN

>>revenue
          city  branch_id state  revenue
0       Austin         10    TX      100
1       Denver         20    CO       83
2  Springfield         30    IL        4
3    Mendocino         47    CA      200

managers
        branch  branch_id state   manager
0       Austin         10    TX  Charlers
1       Denver         20    CO      Joel
2    Mendocino         47    CA     Brett
3  Springfield         31    MO     Sally

sales
          city state  units
0    Mendocino    CA      1
1       Denver    CO      4
2       Austin    TX      2
3  Springfield    MO      5
4  Springfield    IL      1
### 
```python
# Merge revenue and sales: revenue_and_sales
revenue_and_sales = pd.merge(revenue, sales, on=['city','state'], how='right')

# Print revenue_and_sales
print(revenue_and_sales)
```
>>          city  branch_id state  revenue  units
0       Austin       10.0    TX    100.0      2
1       Denver       20.0    CO     83.0      4
2  Springfield       30.0    IL      4.0      1
3    Mendocino       47.0    CA    200.0      1
4  Springfield        NaN    MO      NaN      5


### 
```python
# Merge sales and managers: sales_and_managers
sales_and_managers = pd.merge(sales, managers, left_on=['city','state'], right_on=['branch','state'], how='left')

# Print sales_and_managers
print(sales_and_managers)
```
>>          city state  units       branch  branch_id   manager
0    Mendocino    CA      1    Mendocino       47.0     Brett
1       Denver    CO      4       Denver       20.0      Joel
2       Austin    TX      2       Austin       10.0  Charlers
3  Springfield    MO      5  Springfield       31.0     Sally
4  Springfield    IL      1          NaN        NaN       NaN


### 
```python
# Perform the first merge: merge_default
merge_default = pd.merge(sales_and_managers, revenue_and_sales)

# Print merge_default
print(merge_default)
```
>>        city state  units     branch  branch_id   manager  revenue
0  Mendocino    CA      1  Mendocino       47.0     Brett    200.0
1     Denver    CO      4     Denver       20.0      Joel     83.0
2     Austin    TX      2     Austin       10.0  Charlers    100.0


### 
```python
# Perform the second merge: merge_outer
merge_outer = pd.merge(sales_and_managers, revenue_and_sales, how='outer')

# Print merge_outer
print(merge_outer)
```
>>          city state  units       branch  branch_id   manager  revenue
0    Mendocino    CA      1    Mendocino       47.0     Brett    200.0
1       Denver    CO      4       Denver       20.0      Joel     83.0
2       Austin    TX      2       Austin       10.0  Charlers    100.0
3  Springfield    MO      5  Springfield       31.0     Sally      NaN
4  Springfield    IL      1          NaN        NaN       NaN      NaN
5  Springfield    IL      1          NaN       30.0       NaN      4.0
6  Springfield    MO      5          NaN        NaN       NaN      NaN


### 
```python
# Perform the third merge: merge_outer_on
merge_outer_on = pd.merge(sales_and_managers, revenue_and_sales, on=['city','state'], how='outer')

# Print merge_outer_on
print(merge_outer_on)
```
>>          city state  units_x       branch  branch_id_x   manager  branch_id_y  revenue  units_y
0    Mendocino    CA        1    Mendocino         47.0     Brett         47.0    200.0        1
1       Denver    CO        4       Denver         20.0      Joel         20.0     83.0        4
2       Austin    TX        2       Austin         10.0  Charlers         10.0    100.0        2
3  Springfield    MO        5  Springfield         31.0     Sally          NaN      NaN        5
4  Springfield    IL        1          NaN          NaN       NaN         30.0      4.0        1

### Using merge_ordered()
>>austin
        date ratings
0 2016-01-01  Cloudy
1 2016-02-08  Cloudy
2 2016-01-17   Sunny

houston
        date ratings
0 2016-01-04   Rainy
1 2016-01-01  Cloudy
2 2016-03-01   Sunny


```python
# Perform the first ordered merge: tx_weather
tx_weather = pd.merge_ordered(austin, houston)

# Print tx_weather
print(tx_weather)
```
>>        date ratings
0 2016-01-01  Cloudy
1 2016-01-04   Rainy
2 2016-01-17   Sunny
3 2016-02-08  Cloudy
4 2016-03-01   Sunny


### 
```python
# Perform the second ordered merge: tx_weather_suff
tx_weather_suff = pd.merge_ordered(austin, houston, on='date', suffixes=['_aus', '_hus'])

# Print tx_weather_suff
print(tx_weather_suff)
```
>>        date ratings_aus ratings_hus
0 2016-01-01      Cloudy      Cloudy
1 2016-01-04         NaN       Rainy
2 2016-01-17       Sunny         NaN
3 2016-02-08      Cloudy         NaN
4 2016-03-01         NaN       Sunny


### 
```python
# Perform the third ordered merge: tx_weather_ffill
tx_weather_ffill = pd.merge_ordered(austin, houston, on='date', fill_method='ffill', suffixes=['_aus', '_hus'])

# Print tx_weather_ffill
print(tx_weather_ffill)
```
>>        date ratings_aus ratings_hus
0 2016-01-01      Cloudy      Cloudy
1 2016-01-04      Cloudy       Rainy
2 2016-01-17       Sunny       Rainy
3 2016-02-08      Cloudy       Rainy
4 2016-03-01      Cloudy       Sunny
