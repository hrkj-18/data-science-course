# Importing Data in Python (Part 1)

## Chapter 1 : Introduction and flat files

### Importing Data in Python
Starting a line with ! gives you complete system shell access. <br> 
This means that the IPython magic command ! ls will display the contents of your current directory

### Importing entire text files
```python
file = open('moby_dick.txt', mode='r')

print(file.read())
print(file.closed)
```
>>Call me Ishmael. Some years ago--never mind how long precisely... <br>
>>False

```python
file.close()
print(file.closed)
```
>>True

### Importing text files line by line

```python
`with open('moby_dick.txt') as file:` #with is the context manager
    `print(file.readline())`
    `print(file.readline())`
    `print(file.readline())`
```
>>CHAPTER 1. Loomings.

>> 

>>Call me Ishmael. Some years ago--never mind how long precisely--having


### Using NumPy to import flat files
```python
`file = 'digits.csv'

`digits = np.loadtxt(file, delimiter=',')`
`print(type(digits))`
```
>><class 'numpy.ndarray'>

```python
im = digits[21, 1:]`
im_sq = np.reshape(im, (28, 28))`
```

```python
`plt.imshow(im_sq, cmap='Greys', interpolation='nearest')`
`plt.show()`
```
>>![Number 6 from MNIST dataset](/img/6.png "Number 6 from MNIST dataset")

### Customizing your NumPy import
There are a number of arguments that np.loadtxt() takes that you'll find useful: 
1. delimiter changes the delimiter that loadtxt() is expecting, for example, you can use ',' and '\t' for comma-delimited and tab delimited respectively; 
2. skiprows allows you to specify how many rows (not indices) you wish to skip; 
3. usecols takes a list of the indices of the columns you wish to keep.
```python
`data = np.loadtxt(file, delimiter='\t', skiprows=1, usecols=[0,2])`
```
>>Prints the contents of the file skipping the first row and using columns 0th and 2nd which was tab delimited 

### Working with mixed datatypes
Here, the first argument is the filename, <br>
the second specifies the delimiter ,  <br>
and the third argument names tells us there is a header. <br> 
Because the data are of different types, data is an object called a structured array.
```python
`data = np.genfromtxt('titanic.csv', delimiter=',', names=True, dtype=None)`
```
>>data=numpy array with tuples of rows

```python
`data = np.recfromcsv('titanic.csv', delimiter=',', names=True, dtype=None)`
```
>>np.recfromcsv() that behaves similarly to np.genfromtxt(), except that its default dtype is None

### Using pandas to import flat files as DataFrames

```python
`df = pd.read_csv(file)`
print(df.head())`
```
>>prints first 5 rows of the DataFrame

```python
`data=pd.read_csv(file,nrows=5,header=None)` #takes first 5 rows only
`data_array=data.values`
```
>>data_array contains only the data and is not the DataFrame

```python
`data = pd.read_csv(file, sep='\t', comment='#', na_values='Nothing')`
```
