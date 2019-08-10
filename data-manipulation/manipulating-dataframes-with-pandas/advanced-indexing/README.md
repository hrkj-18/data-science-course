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

### Hierarchical indexing
```python
sales = sales.set_index(['state', 'month'])

# Sort the MultiIndex: sales
sales = sales.sort_index()

# Print the sales DataFrame
print(sales)
```
>>
