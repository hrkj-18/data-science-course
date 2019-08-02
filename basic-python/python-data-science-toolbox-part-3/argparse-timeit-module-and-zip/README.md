# Python Data Science Toolbox Part 3

## Chapter 1 : Argparse , Timeit module and Zip

### Argparse

```python
import argparse
import sys

def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('--x', type=float, default=1.0,
                        help='What is the first number?')
    parser.add_argument('--y', type=float, default=1.0,
                        help='What is the second number?')
    parser.add_argument('--operation', type=str, default='add',
                        help='What operation? Can choose add, sub, mul, or div')
    args = parser.parse_args()
    sys.stdout.write(str(calc(args)))
    
def calc(args):
    if args.operation == 'add':
        return args.x + args.y
    elif args.operation == 'sub':
        return args.x - args.y
    elif args.operation == 'mul':
        return args.x * args.y
    elif args.operation == 'div':
        return args.x / args.y

if __name__ == '__main__':
    main()
```
>>python argparse_example.py --x=5 --y=3 --operation=mul
>>15.0

>>python argparse_example.py -h
>>usage: argparse_example.py [-h] [--x X] [--y Y] [--operation OPERATION]
>>
>>optional arguments:
>>  -h, --help            show this help message and exit
>>  --x X                 What is the first number?
>>  --y Y                 What is the second number?
>>  --operation OPERATION
>>                        What operation? Can choose add, sub, mul, or div

### Timeit Module
This tells us how long it took to run 500,000 iterations of 1+3
```python
import timeit
print(timeit.timeit('1+3', number=500000))
```
>>0.006161588492280894

### For Generator
```python
print(timeit.timeit('''input_list = range(100)

def div_by_two(num):
    if (num/2).is_integer():
        return True
    else:
        return False

# generator:
xyz = i for i in input_list if div_by_two(i)
''', number=50000))
```
>>0.03889649630650638

### For List Comprehension
```python
print(timeit.timeit('''input_list = range(100)

def div_by_two(num):
    if (num/2).is_integer():
        return True
    else:
        return False

# generator:
xyz = [i for i in input_list if div_by_two(i)]''', number=50000))
```
>>1.5278349260021287

### Zip function
```python
x = [1,2,3,4]
y = [7,8,3,2]
z = ['a','b','c','d']

for a,b,c in zip(x,y,z):
    print(a,b,c)

print(zip(x,y,z))
```
>>1 7 a
>>2 8 b
>>3 3 c
>>4 2 d
>><zip object at 0x000001BDA0F31E08>

```python
for i in zip(x,y,z):
    print(i)
```
>>(1, 7, 'a')
>>(2, 8, 'b')
>>(3, 3, 'c')
>>(4, 2, 'd')

```python
names = ['Jill','Jack','Jeb','Jessica']
grades = [99,56,24,87]

d = dict(zip(names,grades))
print(d)
```
>>{'Jeb': 24, 'Jack': 56, 'Jessica': 87, 'Jill': 99}
