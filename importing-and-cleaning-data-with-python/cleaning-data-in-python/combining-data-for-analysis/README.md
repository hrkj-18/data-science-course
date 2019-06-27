# Cleaning Data in Python

## Chapter 3 : Combining data for analysis

### Concatenating data
Multiple datasets can be concatinated by caoncating their DataFrames
```python
row_concatenated_dataset = pd.concat([dataset1,dataset2,....,datasetn])
column_concatenated_dataset = pd.concat([dataset1,dataset2,....,datasetn],axis=1)
```

### Finding and concatenating data
### Globbing
```python
import glob
import pandas as pd

pattern = '*.csv'
csv_files = glob.glob(pattern)

dataframes=[]
for csv_file in csv_files:
    dataframe=pd.read_csv(csv_file)
    dataframes.append(dataframe)

row_concatenated_dataset = pd.concat(dataframes)
```

### Merging Datsets OR Concatinating based on same set of columns
```python
merged_dataframe = pd.merge(left=first_dataset, right=second_dataset, left_on='column_of_left', right_on='column_of_right')
```
