# Pandas Foundation

## Chapter 2 : Exploratory data analysis

### Visual exploratory data analysis

### pandas line plots

```python
df.plot(x='column_name' , y='column_name or list of column_names')

plt.xlabel('Xaxis description')
plt.ylabel('Yaxis description')
plt.title('Title')

plt.show()
```
### pandas scatter plots

```python
df.plot(kind='scatter', x ='column_name', y ='column_name', s=size)
```
### pandas box plots
```python
cols = ['requiured','columns']
df[cols].plot(kind='box',subplots=True)
plt.show()
```

### pandas hist, pdf and cdf

```python
# This formats the plots such that they appear on separate rows
fig, axes = plt.subplots(nrows=2, ncols=1)

# Plot the PDF
df.fraction.plot(ax=axes[0], kind='hist', normed=True, bins=30, range=(0,.3))
plt.show()

# Plot the CDF
df.fraction.plot(ax=axes[1], kind='hist', normed=True, bins=30, cumulative=True, range=(0,.3))
plt.show()
```
### Statistical exploratory data analysis
#### Describe
```python
df.describe()
```
>>Prints all the min max and quartiles of all the columns
 #### Min & Max
```python
df.min() or df.max()
```
>>Gives min or max of all the columns

#### Count
```python
print(df.count())
```
>>prints the number of non missing values in all columns


#### Quantiles
```python
print(df.quantile([0.05, 0.95]))
```
### Separating populations with Boolean indexing

```python
filtered_df=df.loc[df[column_name]='Value']
```
