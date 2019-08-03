# Python Data Science Toolbox Part 3

## Chapter 2 : Multiprocessing

[Simplified Explanation on Multiprocessing](https://medium.com/@urban_institute/using-multiprocessing-to-make-python-code-faster-23ea5ef996ba)

### Multiprocessing
```python
import multiprocessing

def spawn(num):
    print(f'Spawned {num}')

if __name__ == '__main__':
    for i in range(5):
        p = multiprocessing.Process(target=spawn, args=(i,))
        p.start()
        p.join()
```
>>Spawn 0
>>Spawn 1
>>Spawn 2
>>Spawn 3
>>Spawn 4

The .join is the culprit here. It's waiting for the process to end.
```python
import multiprocessing

def spawn(num):
    print(f'Spawned {num}'')

if __name__ == '__main__':
    for i in range(5):
        p = multiprocessing.Process(target=spawn, args=(i,))
        p.start()
```
>>Spawn 2
>>Spawn 3
>>Spawn 1
>>Spawn 0
>>Spawn 4

If I change the range to 500, I go 0 to 100 real quick. You should also clearly see a bunch of Python processes spawning in your process lists.

Remember .join if you actually need to wait on a process. If you don't need to wait, then obviously you don't want to be using it.

### Getting Values from Multiprocessing Processes
```python
from multiprocessing import Pool

def job(num):
    return num * 2

if __name__ == '__main__':
    p = Pool(processes=20)
    data = p.map(job, [i for i in range(20)])
    p.close()
    print(data)
```
>>[0, 2, 4, 6, 8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28, 30, 32, 34, 36, 38]
