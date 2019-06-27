# Cleaning Data in Python

## Chapter 1 : Exploring your data

### Diagnose data for cleaning

```python
df = pd.read_csv(csv_file)

print(df.shape)
print(df.columns)
print(df.info())
```
>>prints shape <br> prints list of columnm names <br> prints the data type of columns


```python
print(df.describe())
```
>>prints <br>      
>>count <br> 
>>mean <br> 
>>std <br> 
>>min <br> 
>>25% <br> 
>>50% <br> 
>>75%  <br> 
max

```python
print(df['Column_Name'].value_counts(dropna=False))
```
>>gives frequescy of all values in the specified column even the missing ones


### Visual Exploratory Data Analysis
```python
df['Column_Name'].plot(kind='hist')
````
>>plots a histogram of the column

```python
df.boxplot(column='Column_Name', by='column_name', rot=90)
```
>>shows boxplot
