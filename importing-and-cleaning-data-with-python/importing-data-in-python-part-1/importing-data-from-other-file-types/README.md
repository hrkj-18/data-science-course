# Importing Data in Python (Part 1)

## Chapter 2 : Importing data from other file types

### Loading a pickled file

```python
`import pickle`

`with open('data.pkl', 'rb') as file:`
    `d = pickle.load(file)`

`print(d)`
```
>>{'June': '69.4', 'Aug': '85', 'Airline': '8', 'Mar': '84.4'}

```python
`print(type(d))`
```
>><class 'dict'>

### Listing sheets in Excel files

```python
`xls = pd.ExcelFile(file)
print(xls.sheet_names)`
```
```python
`df1 = xls.parse('Sheet_name')`
`df2=xls.parse(Index of sheet)`
```

```python
`df1 = xls.parse(0, skiprows=[1], names=['Country','AAM due to War (2002)'])`
`print(df1.head())`
```
>>|  |             Country|  AAM due to War (2002)|
>>|---|---|---|
>>|0|              Albania|               0.128908|
>>|1|              Algeria|              18.314120|
>>|2|              Andorra|               0.000000|
>>|3|               Angola|              18.964560|
>>|4|  Antigua and Barbuda|               0.000000|

### Importing SAS files
```python
`from sas7bdat import SAS7BDAT`

`with SAS7BDAT('sales.sas7bdat') as file:`
    `df_sas=file.to_data_frame()`
`print(df_sas.head())`
```
>>| |    YEAR|     P|           S|
>>|---|---|---|---|
>>|0|  1950.0|  12.9|  181.899994|
>>|1|  1951.0|  11.9|  245.000000|
>>|2|  1952.0|  10.7|  250.199997|
>>|3|  1953.0|  11.3|  265.899994|
>>|4|  1954.0|  11.2|  248.500000|

### Importing Stata files
```python
`import pandas as pd`
`df=pd.read_stata('disarea.dta')`
```

### Importing HDF5 files
```python
`import numpy as np`
`import h5py`

`data = h5py.File('LIGO_data.hdf5', 'r')`
`print(type(data))`
```
>><class 'h5py._hl.files.File'>

```python
`for key in data.keys():`
    `print(key)`
```
>>meta <br> quality <br> strain

```python
`group=data['strain']`
print(group)

for key in group.keys():
    print(key)
```
>><HDF5 group "/strain" (1 members)> <br>
>>Strain

```python
`strain=data['strain']['Strain'].value`
print(strain)
print(np.shape(strain))
print(type(strain))
```
>>[-1.77955839e-18 -1.76552067e-18 -1.71049117e-18 ... -1.76375155e-18 -1.72364846e-18 -1.71969299e-18]
>>(131072,) <br>
>><class 'numpy.ndarray'>


```python
`num_samples=10000`
`time = np.arange(0, 1, 1/num_samples)`

`plt.plot(time, strain[:num_samples])`
`plt.xlabel('GPS Time (s)')`
`plt.ylabel('strain')`
`plt.show()`
```
>>![](img/hdf5-file-example.png)

### Importing MATLAB files

```python
import scipy.io
mat=scipy.io.loadmat('albeck_gene_expression.mat')
print(type(mat))`
```
>><class 'dict'>

```python
`print(mat.keys())`
```
>>dict_keys(['__header__', '__version__', '__globals__', 'rfpCyt', 'rfpNuc', 'cfpNuc', 'cfpCyt', 'yfpNuc', 'yfpCyt', 'CYratioCyt'])

```python
`print(type(mat['CYratioCyt']))`
`print(np.shape(mat['CYratioCyt']))`
```
>><class 'numpy.ndarray'> <br> (200, 137)

