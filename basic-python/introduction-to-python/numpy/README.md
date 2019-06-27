# Introdution to Python

## Chapter 4 : NumPy
### NumPy
```python
baseball = [180, 215, 210, 210, 188, 176, 209, 200]
import numpy as np
np_baseball = np.array(baseball)

print(np_baseball)
```
>>[180 215 210 210 188 176 209 200]

```python
print(type(np_baseball))
<class 'numpy.ndarray'>

x = [4 , 9 , 6, 3, 1]
y = np.array(x)

high = y > 5
print(high)
```
>>[False  True  True False False]


```python
print(y[high])
```
>>[9,6]

### Addition of NumPy arrays
```python
A=np.array([1,2,3])
B=np.array([2,3,4])
```
>>A+B=np.array([3,5,7])


### Mean
```python
A=np.array([1,2,3])
print(np.mean(A))
```
>>2

### Median
```python
A=np.array([1,2,3])
print(np.mean(A))
```
>>2

### Standard Deviation
```python
np.std(A)
```

### Correlation
```python
np.corrcoef(A[:,0],B[:,1])
```
