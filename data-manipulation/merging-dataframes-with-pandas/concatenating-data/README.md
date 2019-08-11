# Merging Dataframes with Pandas

## Chapter 2 : Concatenating Data

### Appending Series with nonunique Indices
bronze
Country
United States     1052.0
Soviet Union       584.0
United Kingdom     505.0
France             475.0
Germany            454.0
Name: Total, dtype: float64

silver
Country
United States     1195.0
Soviet Union       627.0
United Kingdom     591.0
France             461.0
Italy              394.0
Name: Total, dtype: float64
```python
combined = bronze.append(silver)
print(combined)
```
>>Country
United States     1052.0
Soviet Union       584.0
United Kingdom     505.0
France             475.0
Germany            454.0
United States     1195.0
Soviet Union       627.0
United Kingdom     591.0
France             461.0
Italy              394.0
Name: Total, dtype: float64


```python
combined.loc['United States']
```
>>Country
United States    1052.0
United States    1195.0
Name: Total, dtype: float64


### Appending pandas Series
```python
jan = pd.read_csv('sales-jan-2015.csv', index_col='Date', parse_dates=True)
feb = pd.read_csv('sales-feb-2015.csv', index_col='Date', parse_dates=True)
mar = pd.read_csv('sales-mar-2015.csv', index_col='Date', parse_dates=True)

jan_units = jan['Units']
feb_units = feb['Units']
mar_units = mar['Units']

# Append feb_units and then mar_units to jan_units: quarter1
quarter1 = jan_units.append(feb_units).append(mar_units)
```

### Concatenating pandas Series along row axis
```python
# Initialize empty list: units
units = []

# Build the list of Series
for month in [jan, feb, mar]:
    units.append(month['Units'])

# Concatenate the list: quarter1
quarter1 = pd.concat(units, axis='rows')
```
>>


### Appending DataFrames with ignore_index
```python
combined_names = names_1881.append(names_1981, ignore_index=True)
combined_names = names_1881.append(names_1981)
```
>>1
>>2
>>3
>>4
>>5
>>1
>>2
>>3
>>1
>>2


### Concatenating pandas DataFrames along column axis
```python
# Create a list of weather_max and weather_mean
weather_list = [weather_max, weather_mean]

# Concatenate weather_list horizontally
weather = pd.concat(weather_list, axis=1)

# Print weather
print(weather)
```
>>     Max TemperatureF  Mean TemperatureF
Apr              89.0          53.100000
Aug               NaN          70.000000
Dec               NaN          34.935484


### Reading multiple files to build a DataFrame
```python
# Concatenate medals horizontally: medals_df
medals_df = pd.concat([bronze,silver,gold], axis='columns')

# Print medals_df
print(medals_df)
```
>>                bronze  silver    gold
France           475.0   461.0     NaN
Germany          454.0     NaN   407.0
Italy              NaN   394.0   460.0
Soviet Union     584.0   627.0   838.0
United Kingdom   505.0   591.0   498.0
United States   1052.0  1195.0  2088.0


### Concatenating vertically to get MultiIndexed rows
```python
# Concatenate medals: medals
medals = pd.concat([bronze,silver,gold], keys=['bronze', 'silver', 'gold'])

# Print medals
print(medals)
```
>>                        Total
       Country               
bronze United States   1052.0
       Soviet Union     584.0
       United Kingdom   505.0
       France           475.0
       Germany          454.0
silver United States   1195.0
       Soviet Union     627.0
       United Kingdom   591.0
       France           461.0
       Italy            394.0
gold   United States   2088.0
       Soviet Union     838.0
       United Kingdom   498.0
       Italy            460.0
       Germany          407.0


### 
```python
# Concatenate dataframes: february
february = pd.concat(dataframes, keys=['Hardware','Software','Service'], axis=1)

# Print february.info()
print(february.info())

# Assign pd.IndexSlice: idx
idx = pd.IndexSlice

# Create the slice: slice_2_8
slice_2_8 = february.loc['2015-2-2':'2015-2-8', idx[:,'Company']]

# Print slice_2_8
print(slice_2_8)
```
>>                            Hardware         Software Service
                             Company          Company Company
Date                                                         
2015-02-02 08:33:01              NaN            Hooli     NaN
2015-02-02 20:54:49        Mediacore              NaN     NaN
2015-02-03 14:14:18              NaN          Initech     NaN
2015-02-04 15:36:29              NaN        Streeplex     NaN
2015-02-04 21:52:45  Acme Coporation              NaN     NaN
2015-02-05 01:53:06              NaN  Acme Coporation     NaN
2015-02-05 22:05:03              NaN              NaN   Hooli
2015-02-07 22:58:10  Acme Coporation              NaN     NaN


### Concatenating DataFrames from a dict
```python
# Make the list of tuples: month_list
month_list = [('january', jan), ('february', feb), ('march', mar)]

# Create an empty dictionary: month_dict
month_dict = {}

for month_name, month_data in month_list:

    # Group month_data: month_dict[month_name]
    month_dict[month_name] = month_data.groupby('Company').sum()

# Concatenate data in month_dict: sales
sales = pd.concat(month_dict)

# Print sales
print(sales)

# Print all sales by Mediacore
idx = pd.IndexSlice
print(sales.loc[idx[:, 'Mediacore'], :])
```
>>                    Units
         Company         
february Mediacore     45
january  Mediacore     15
march    Mediacore     68


### Concatenating DataFrames with inner join
```python
# Create the list of DataFrames: medal_list
medal_list = [bronze, silver, gold]

# Concatenate medal_list horizontally using an inner join: medals
medals = pd.concat(medal_list, keys=['bronze', 'silver', 'gold'], axis=1, join='inner')

# Print medals
print(medals)
```
>>                bronze  silver    gold
                 Total   Total   Total
Country                               
United States   1052.0  1195.0  2088.0
Soviet Union     584.0   627.0   838.0
United Kingdom   505.0   591.0   498.0
