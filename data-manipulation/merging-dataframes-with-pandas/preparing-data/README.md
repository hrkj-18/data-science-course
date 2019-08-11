# Merging DataFrames with pandas

## Chapter 1 : Preparing data

### Reading DataFrames from multiple files
```python
# Import pandas
import pandas as pd

# Read 'Bronze.csv' into a DataFrame: bronze
bronze = pd.read_csv('Bronze.csv')

# Read 'Silver.csv' into a DataFrame: silver
silver = pd.read_csv('Silver.csv')

# Read 'Gold.csv' into a DataFrame: gold
gold = pd.read_csv('Gold.csv')
```

```python
# Create the list of file names: filenames
filenames = ['Gold.csv', 'Silver.csv', 'Bronze.csv']

# Create the list of three DataFrames: dataframes
dataframes = []
for filename in filenames:
    dataframes.append(pd.read_csv(filename))
```
>>


### Sorting DataFrame with the Index & columns
```python
# Import pandas
import pandas as pd

# Read 'monthly_max_temp.csv' into a DataFrame: weather1
weather1 = pd.read_csv('monthly_max_temp.csv', index_col='Month')

# Print the head of weather1
print(weather1.head())
```
>>       Max TemperatureF
Month                  
Jan                  68
Feb                  60
Mar                  68
Apr                  84
May                  88


```python
# Sort the index of weather1 in alphabetical order: weather2
weather2 = weather1.sort_index()

# Print the head of weather2
print(weather2.head())
```
>>       Max TemperatureF
Month                  
Apr                  84
Aug                  86
Dec                  68
Feb                  60
Jan                  68


```python
# Sort the index of weather1 in reverse alphabetical order: weather3
weather3 = weather1.sort_index(ascending=False)

# Print the head of weather3
print(weather3.head())
```
>>       Max TemperatureF
Month                  
Sep                  90
Oct                  84
Nov                  72
May                  88
Mar                  68

```python
# Sort weather1 numerically using the values of 'Max TemperatureF': weather4
weather4 = weather1.sort_values('Max TemperatureF')

# Print the head of weather4
print(weather4.head())
```
>>       Max TemperatureF
Month                  
Feb                  60
Jan                  68
Mar                  68
Dec                  68
Nov                  72

### Reindexing DataFrame from a list
```python
print(weather1)
print(year)
```
>>       Mean TemperatureF
Month                   
Apr            61.956044
Jan            32.133333
Jul            68.934783
Oct            43.434783
['Jan','Feb','Mar','Apr','May','Jun','Jul','Aug','Sep','Oct','Nov','Dec']


```python
# Reindex weather1 using the list year: weather2
weather2 = weather1.reindex(year)

# Print weather2
print(weather2)
```
>>       Mean TemperatureF
Month                   
Jan            32.133333
Feb                  NaN
Mar                  NaN
Apr            61.956044
May                  NaN
Jun                  NaN
Jul            68.934783
Aug                  NaN
Sep                  NaN
Oct            43.434783
Nov                  NaN
Dec                  NaN


```python
# Reindex weather1 using the list year with forward-fill: weather3
weather3 = weather1.reindex(year).ffill()

# Print weather3
print(weather3)
```
>>       Mean TemperatureF
Month                   
Jan            32.133333
Feb            32.133333
Mar            32.133333
Apr            61.956044
May            61.956044
Jun            61.956044
Jul            68.934783
Aug            68.934783
Sep            68.934783
Oct            43.434783
Nov            43.434783
Dec            43.434783

### Reindexing using another DataFrame Index
```python
common_names = names_1981.reindex(names_1881.index)
```

### Adding unaligned DataFrames
```python
print(january)
print(february)
```
>>january
                  Units
Company                
Acme Corporation     19
Hooli                17
Initech              20
Mediacore            10
Streeplex            13

february
                  Units
Company                
Acme Corporation     15
Hooli                 3
Mediacore            13
Vandelay Inc         25


### 
```python
total = january + february
print(total)
```
>>                  Units
Company                
Acme Corporation   34.0
Hooli              20.0
Initech             NaN
Mediacore          23.0
Streeplex           NaN
Vandelay Inc        NaN


### Broadcasting in arithmetic formulas
```python
# Extract selected columns from weather as new DataFrame: temps_f
temps_f = weather[['Min TemperatureF','Mean TemperatureF','Max TemperatureF']]

# Convert temps_f to celsius: temps_c
temps_c = (temps_f - 32) * 5/9

# Rename 'F' in column names with 'C': temps_c.columns
temps_c.columns = temps_c.columns.str.replace('F', 'C')
```
>>


### Computing percentage growth of GDP
```python
gdp = pd.read_csv('GDP.csv', index_col='DATE', parse_dates=True)

# Slice all the gdp data from 2008 onward: post2008
post2008 = gdp['2008':]

# Print the last 8 rows of post2008
print(post2008.tail(8))
```
>>              VALUE
DATE               
2008-01-01  14668.4
2008-04-01  14813.0
2008-07-01  14843.0
2008-10-01  14549.9
2009-01-01  14383.9
2009-04-01  14340.4
2009-07-01  14384.1
2009-10-01  14566.5
2010-01-01  14681.1
2010-04-01  14888.6
2010-07-01  15057.7
2010-10-01  15230.2
2011-01-01  15238.4
2011-04-01  15460.9
2011-07-01  15587.1
2011-10-01  15785.3
2012-01-01  15973.9
2012-04-01  16121.9
2012-07-01  16227.9
2012-10-01  16297.3
2013-01-01  16475.4
2013-04-01  16541.4
2013-07-01  16749.3
2013-10-01  16999.9
2014-01-01  17025.2
2014-04-01  17285.6
2014-07-01  17569.4
2014-10-01  17692.2
2015-01-01  17783.6
2015-04-01  17998.3
2015-07-01  18141.9
2015-10-01  18222.8
2016-01-01  18281.6
2016-04-01  18436.5


### 
```python
# Resample post2008 by year, keeping last(): yearly
yearly = post2008.resample('A').last()

# Print yearly
print(yearly)
```
>>              VALUE
DATE               
2008-12-31  14549.9
2009-12-31  14566.5
2010-12-31  15230.2
2011-12-31  15785.3
2012-12-31  16297.3
2013-12-31  16999.9
2014-12-31  17692.2
2015-12-31  18222.8
2016-12-31  18436.5


### 
```python
# Compute percentage growth of yearly: yearly['growth']
yearly['growth'] = yearly.pct_change() * 100

# Print yearly again
print(yearly)
```
>>              VALUE    growth
DATE                         
2008-12-31  14549.9       NaN
2009-12-31  14566.5  0.114090
2010-12-31  15230.2  4.556345
2011-12-31  15785.3  3.644732
2012-12-31  16297.3  3.243524
2013-12-31  16999.9  4.311144
2014-12-31  17692.2  4.072377
2015-12-31  18222.8  2.999062
2016-12-31  18436.5  1.172707
