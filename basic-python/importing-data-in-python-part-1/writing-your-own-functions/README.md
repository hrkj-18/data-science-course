# Python Data Science Toolbox (Part 1)

## Chapter 1 : Writing your own functions

### Strings in Python

```python
object1 = "data" + "analysis" + "visualization"
object2 = 1 * 3
object3 = "1" * 3
```
>>object1 contains "dataanalysisvisualization", object2 contains 3, object3 contains "111"

### Write a simple function

```python
def shout():
    shout_word='congratulations'+'!!!'
    print(shout_word)

shout()
```
>>congratulations!!!

### Single-parameter functions
```python
def shout(word):
    shout_word = word + '!!!'
    print(shout_word)

shout('congratulations')
```
>>congratulations!!!

### Functions that return single values

```python
def shout(word):
    shout_word=word+'!!!'
    return shout_word

yell=shout('congratulations')
print(yell)
```
>>congratulations!!!

### Functions with multiple parameters
```python
def shout(word1, word2):
    shout1=word1+'!!!'
    shout2=word2+'!!!'

    new_shout=shout1+shout2
    return new_shout

yell=shout('congratulations','you')
print(yell)
```
>>congratulations!!!you!!!

### A brief introduction to tuples
```python
nums=(3,4,6)
num1,num2,num3=nums
even_nums=(2,num2,num3)
print(even_nums)
```
>>(2,4,6)

### Functions that return multiple values

```python
def shout_all(word1, word2): 
    shout1=word1+'!!!'
    shout2=word2+'!!!'
    
    shout_words=(shout1,shout2)
    return shout_words

yell1,yell2 = shout_all('congratulations','you')

print(yell1)
print(yell2)
```
>>congratulations!!! <br>
>>you!!!
