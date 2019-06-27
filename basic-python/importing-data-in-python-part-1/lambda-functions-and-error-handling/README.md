# Python Data Science Toolbox (Part 1)

## Chapter 3 : Lambda functions and error-handling

### Lambda Functions

```python
add_bangs = (lambda a: a + '!!!')

add_bangs('hello')
```
>>hello!!!

```python
echo_word = (lambda word1,echo:word1*echo)
result = echo_word('hey',5)
print(result)
```
>>heyheyheyheyhey

### Map() and lambda functions

map() applies a function over an object, such as a list. 

```python
spells = ["protego", "accio", "expecto patronum", "legilimens"]

shout_spells= map(lambda item : item+'!!!', spells)
shout_spells_list=list(shout_spells)

print(shout_spells)
print(shout_spells_list)
```
>><map object at 0x7fcdec43c1d0> <br>
>>['protego!!!', 'accio!!!', 'expecto patronum!!!', 'legilimens!!!']

### Filter() and lambda functions

The function filter() offers a way to filter out elements from a list that don't satisfy certain criteria.

```python
fellowship = ['frodo', 'samwise', 'merry', 'pippin', 'aragorn', 'boromir', 'legolas', 'gimli', 'gandalf']

result = filter(lambda  member:len(member)>6, fellowship)
result_list=list(result)

print(result)
print(result_list)
```
>><filter object at 0x7fcdec43acf8> <br>
>>['samwise', 'aragorn', 'boromir', 'legolas', 'gandalf'] 

### Reduce() and lambda functions

The reduce() function is useful for performing some computation on a list and, unlike map() and filter(), returns a single value as a result. <br> 
To use reduce(), you must import it from the functools module.

```python
from functools import reduce
stark = ['robb', 'sansa', 'arya', 'brandon', 'rickon']

result = reduce(lambda item1,item2:item1+item2, stark)
print(result)
```
>>'robbsansaaryabrandonrickon'

### Introduction to error handling

```python
def shout_echo(word1, echo=1):
    echo_word=''
    shout_words=''

    try:
        echo_word = word1*echo
        shout_words = echo_word+'!!!'
   
   except:
        print("word1 must be a string and echo must be an integer.")

    return shout_words

shout_echo("particle", echo="accelerator")
```
>>word1 must be a string and echo must be an integer.

```python
# Define shout_echo
def shout_echo(word1, echo=1):

    if echo<0:
        raise ValueError('echo must be greater than 0')

    echo_word = word1 * echo
    shout_word = echo_word + '!!!'
    return shout_word

shout_echo("particle", echo=5)
```
>> 'particleparticleparticleparticleparticle!!!'

