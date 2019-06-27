# Cleaning Data in Python

## Chapter 4 : Cleaning data for analysis

### Data Types

### Change Data type of a column
```pthon
dataframe.column = dataframe.column.astype('new_data_type')
```
### Object to numeric
```python
dataframe['column'] = pd.to_numeric(dataframe['column'], errors='coerce')
```
>>converts all values to numeric and gives NaN to missing values

### Using regular expressions to clean strings

### String parsing with regular expressions

```python
import re
prog = re.compile('\d{3}-\d{3}-\d{4}')

result = prog.match('123-456-7890')
print(bool(result))
```
>>True

### Extracting numerical values from strings
```python
matches = re.findall('\d+', 'the recipe calls for 10 strawberries and 1 banana')
print(matches)
```
>>['10', '1']

### Applying functions on DataFrame
```python
dataframe['new_column'] = datatframe.column.apply(function)
```
>>New column created according to the function

### Duplicate and missing data

### Dropping duplicate data
```python
dataframe_with_no_dups = dataframe_with_dups.drop_duplicates()
```
>>Deletes all the exact duplicates of rows

### Filling missing data
```python
dataframe['column'] = dataframe['column'].fillna(dataframe['column'].mean())
```
>>All missing values are now filled with the columns mean

### Testing with asserts
```python
assert pd.notnull(dataframe).all().all()
```
>> if true then no op else error
