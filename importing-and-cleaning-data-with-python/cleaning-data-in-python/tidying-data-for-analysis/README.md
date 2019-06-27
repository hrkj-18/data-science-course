# Cleaning Data in Python

## Chapter 2 : Tidying data for analysis

### Tidy Data

### Reshaping your Data using melt

```python
df_melt = pd.melt(df, id_vars=['Columns', 'You','dont_want_be', 'melted'],
                  value_vars=['Columns', 'You','want_be', 'melted'],
                  var_name='Name for the combined column', 
                  value_name='name of the value column'))
```

### Pivoting the data
```python
pivoted_table = table.pivot_table(index=['Columns', 'You','want_to', 'remain_same'], 
                                  columns='Column with columns', 
                                  values='value of those columns'
                                  aggfunc=np.mean)
```
>>we get pivoted dataframe with  hierarchical index 

```python
`pivoted_table_reset =  pivoted_table.reset_index()`
```
>>resets the whole index
