# Intermediate Python for Data Science

## Chapter 4 : Loops

### Enumerate Function
If you also want to access the index information, so where the list element you're iterating over is located, you can use enumerate()
```python
areas = [11.25, 18.0, 20.0, 10.75, 9.50]

for index, a in enumerate(areas) :
    print("room " + str(index) + ": " + str(a))
```
>>room 0: 11.25 <br>
>>room 1: 18.0 <br>
>>room 2: 20.0 <br>
>>room 3: 10.75 <br>
>>room 4: 9.5

### Loop over dictionary
```python
europe = {'spain':'madrid', 'france':'paris', 'germany':'berlin',
          'norway':'oslo', 'italy':'rome', 'poland':'warsaw', 'austria':'vienna' }
          
for x, y in europe.items() :
    print("the capital of " + x + " is " + y)
```
>>the capital of france is paris <br>
>>the capital of germany is berlin <br>
>>the capital of spain is madrid <br>
>>the capital of italy is rome <br>
>>the capital of poland is warsaw <br>
>>the capital of norway is oslo <br>
>>the capital of austria is vienna

### Loop over Numpy array

```python
for x in my_1d_array :
    ...
```
```python
for x in np.nditer(my_2d_array) : 
    ...
```
>>Column wise iteration

```python
for calls, row in cars.iterrows() :
    print(calls)
    print(row)
```

```python
for lab, row in cars.iterrows() :
    print(str(lab)+': '+str(row['cars_per_cap']))
```
>>US: 809 <br>
>>AUS: 731 <br>
>>JAP: 588 <br>
>>IN: 18 <br>
>>RU: 200 <br>
>>MOR: 70 <br>
>>EG: 45
