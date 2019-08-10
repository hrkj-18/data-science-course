# Manipulating Dataframes with Pandas

## Chapter 2 : Advanced Indexing

Indices are immutable
### Changing index name labels
```python
sales.index.name = 'MONTHS'

# Print the sales DataFrame
print(sales)

# Assign the string 'PRODUCTS' to sales.columns.name 
sales.columns.name = 'PRODUCTS'

# Print the sales dataframe again
print(sales)
```
>>Changes name of index and columns

### Extracting data with a MultiIndex
```python
# Print sales.loc[['CA', 'TX']]
print(sales.loc[['CA', 'TX']])

# Print sales['CA':'TX']
print(sales.loc['CA':'TX'])
```
>>             eggs  salt  spam
>>state month                  
>>CA    1        47  12.0    17
>>      2       110  50.0    31
>>TX    1       132   NaN    52
>>      2       205  60.0    55
>>             eggs  salt  spam
>>state month                  
>>CA    1        47  12.0    17
>>      2       110  50.0    31
>>NY    1       221  89.0    72
>>      2        77  87.0    20
>>TX    1       132   NaN    52
>>      2       205  60.0    55

### Hierarchical indexing
```python
sales = sales.set_index(['state', 'month'])

# Sort the MultiIndex: sales
sales = sales.sort_index()

# Print the sales DataFrame
print(sales)
```
>>             eggs  salt  spam
>>state month                  
>>CA    1        47  12.0    17
>>      2       110  50.0    31
>>NY    1       221  89.0    72
>>      2        77  87.0    20
>>TX    1       132   NaN    52
>>      2       205  60.0    55
