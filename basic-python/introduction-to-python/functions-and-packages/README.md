# Introduction to Python

## Chapter 3 : Functions And Packages

### Functions

### Help function
```python
help(max)
?max
```
>>Help on built-in function max in module builtins:<br>
>><br>
>>max(...)<br>
>>    max(iterable, *[, default=obj, key=func]) -> value
>>    max(arg1, arg2, *args, *[, key=func]) -> value
>><br>
>>    With a single iterable argument, return its biggest item. The default keyword-only argument specifies an<br> 
>>    object to return if the provided iterable is empty. <br>
>>    With two or more arguments, return the largest argument.<br>    

### Methods
### String Methods
```python
room = "poolhouse"
```
#### Upper
```python
room_up=room.upper()

print(room)
print(room_up)
```
>>poolhouse<br>
>>POOLHOUSE

#### Count
```python
print(room.count("o"))
```
>>3

### List Methods        
```python
areas = [11.25, 18.0, 20.0, 10.75, 9.50]
```
#### Index
```python
print(areas.index(20.0))
```
>>2

#### Count
```python
print(areas.count(14.5))
```
>>0

#### Append
```python
areas.append(24.5)
areas.append(15.45)
print(areas)
```
>>[11.25, 18.0, 20.0, 10.75, 9.5, 24.5, 15.45]

#### Reverse
```python
areas.reverse()
print(areas)
```
>>[15.45, 24.5, 9.5, 10.75, 20.0, 18.0, 11.25]

#### Remove
```python
areas.remove(24.5)
print(areas)
```
>>[15.45, 24.5, 9.5, 10.75, 20.0, 18.0, 11.25]
