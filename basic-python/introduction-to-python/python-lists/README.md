# Introduction to Python

## Chapter 2 : Python Lists

<p align = 'left'> [Chapter 1 : Python Basics](https://hrkj-18.github.io/data-science-course/basic-python/introduction-to-python/python-lists/)</p>
<p align = 'right'> [Chapter 3 : Functions and Packages](https://hrkj-18.github.io/data-science-course/basic-python/introduction-to-python/functions-and-packages/)</p>

### Lists

### Indexing
Start starts with 0<br>
End starts with -1

### Slicing of Lists
```python
A=['a','b','c','d','e','f']

print(A[1:3])
```
>>['b','c']
```python
print(A[2:])
```
>>['c','d','e','f']

### List Manipulation

### Replace list elements
```python
A=['a','b','c','d','e','f']

A[2]='g'
print(A)
```
>>['a','b','g','d','e','f']

### Extend a list
```python
A=['a','b','c']
B=['d','e','f']
print(A+B)
```
>>['a','b','g','d','e','f']

### Delete list elements
```python
A=['a','b','c','d','e','f']
del(A[1])
print(A)
```
>>['a','c','d','e','f']

### Inner workings of a list
```python
A=['a','b','c','d','e','f']
new_A = A[:]
print(new_A)

```
>>['a','b','c','d','e','f']

<p align = 'left'> [Chapter 1 : Python Basics](https://hrkj-18.github.io/data-science-course/basic-python/introduction-to-python/python-lists/)</p>
<p align = 'right'> [Chapter 3 : Functions and Packages](https://hrkj-18.github.io/data-science-course/basic-python/introduction-to-python/functions-and-packages/)</p>
