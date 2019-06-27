# Python Data Science Toolbox (Part 1)

## Chapter 2 : Default arguments, variable-length arguments and scope

### Scope and user-defined functions

```python
num = 5

def func1():
    num = 3
    print(num)

def func2():
    global num
    double_num = num * 2
    num = 6
    print(double_num)
    print(num)

print(num)
func1()
func2()
print(num)
```
>>5 <br> 3 <br> 10 <br> 6 <br> 6

### Nested Functions I

```python
def three_shouts(word1, word2, word3):
    def inner(word):
        return word + '!!!'

    return (inner(word1), inner(word2), inner(word3))

print(three_shouts('a', 'b', 'c'))
```
>>('a!!!', 'b!!!', 'c!!!')

### Nested Functions II

```python
def echo(n):
    def inner_echo(word1):        
        echo_word = word1 * n
        return echo_word

    return inner_echo

twice = echo(2)
thrice = echo(3)
print(twice('hello'), thrice('hello'))
```
>>hellohello hellohellohello

### The keyword nonlocal and nested functions

```python
def echo_shout(word):
    echo_word=word+word
    print(echo_word)
    
    def shout():
        nonlocal echo_word
        echo_word = echo_word+'!!!'
    
    shout()
    
    print(echo_word)

echo_shout('hello')
```
>>hellohello <br>
>hellohello!!!

```python
def shout_echo(word1, echo=1):
    echo_word = word1*echo

    shout_word = echo_word + '!!!'
    return shout_word

no_echo = shout_echo('Hey')
with_echo = shout_echo('Hey',5)

print(no_echo)
print(with_echo)
```
>>Hey!!!
>>HeyHeyHeyHeyHey!!!

### Functions with variable-length arguments (*args)
Flexible arguments enable you to pass a variable number of arguments to a function.

```python
def gibberish(*args):
    hodgepodge=''

    for word in args:
        hodgepodge += word
        
    return hodgepodge

one_word = gibberish('luke')
many_words = gibberish("luke", "leia", "han", "obi", "darth")

print(one_word)
print(many_words)
```
>>luke <br>
>>lukeleiahanobidarth
### Functions with variable-length keyword arguments (**kwargs)**

What makes ****kwargs** different is that it allows you to pass a variable number of keyword arguments to functions.

```python
# Define report_status
def report_status(**kwargs):
    print("\nBEGIN: REPORT\n")
    
    for key, value in kwargs.items():
        print(key + ": " + value)

    print("\nEND REPORT")

report_status(name="luke", affiliation="jedi", status="missing")
report_status(name='anakin', affiliation='sith lord', status='deceased')
```
>>BEGIN: REPORT <br>
>> <br>
>>name: luke <br>
>>affiliation: jedi <br>
>>status: missing <br>
>> <br>
>>END REPORT <br>
>> <br>
>>BEGIN: REPORT <br>
>> <br>
>>name: anakin <br>
>>affiliation: sith lord <br>
>>status: deceased <br>
>> <br>
>>END REPORT
