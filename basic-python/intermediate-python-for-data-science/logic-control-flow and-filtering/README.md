# Intermediate Python for Data Science

## Chapter 3 : Logic Control And Flow

### Comparison of Arrays

```python
my_house = np.array([18.0, 20.0, 10.75, 9.50])
your_house = np.array([14.0, 24.0, 14.25, 9.0])

print(my_house>=18)
```
>>[ True  True False False]

```python
print(my_house<your_house)
```
>>[False  True  True False]

### Boolean operators with Numpy

```python
my_house = np.array([18.0, 20.0, 10.75, 9.50])
your_house = np.array([14.0, 24.0, 14.25, 9.0])

print(np.logical_or(my_house>18.5, my_house<10)
```
>>[False  True False  True]


```python
print(np.logical_and(my_house<11, your_house<11))
```
>>[False False False  True]

### Filtering Pandas DataFrame

```python
cars = pd.read_csv('cars.csv', index_col = 0)

dr=cars["drives_right"]
print(dr)
```
>>US &nbsp;&nbsp;&nbsp;&nbsp;      True<br>
>>AUS &nbsp;&nbsp;&nbsp;&nbsp;    False<br>
>>JAP &nbsp;&nbsp;&nbsp;&nbsp;  False<br>
>>IN &nbsp;&nbsp;&nbsp;&nbsp;   False<br>
>>RU &nbsp;&nbsp;&nbsp;&nbsp;    True<br>
>>MOR &nbsp;&nbsp;&nbsp;&nbsp;    True<br>
>>EG &nbsp;&nbsp;&nbsp;&nbsp;     True<br>
>>Name: drives_right, dtype: bool

```python
sel=cars[dr]
print(sel)
```
>>|   |  cars_per_cap|        country|  drives_right|
>>|---|---|---|---|
>>|US|            809|  United States|          True|
>>|RU|            200|         Russia|          True|
>>|MOR|            70|        Morocco|          True|
>>|EG|             45|          Egypt|          True|
