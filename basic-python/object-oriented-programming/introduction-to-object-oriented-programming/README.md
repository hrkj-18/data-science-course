# Object Oriented Programming

## Chapter 1 : Introduction to Object Oriented Programming

### Classes
```python
class Human:
    
    def __init__(self, name, gender):
        self.name = name
        self.gender = gender
        self.hairColor = random.choice('Black Brown')        
```
>>
### 
```python
class Blob:
    
    def __init__(self, color):
        self.x = random.randrange(0, WIDTH)
        self.y = random.randrange(0, HEIGHT)
        self.size = random.randrange(4,8)
        self.color = color
    
    def move(self):
        self.move_x = random.randrange(-1,2)
        self.move_y = random.randrange(-1,2)
        self.x += self.move_x
        self.y += self.move_y
    
    def move(self):
        self.move_x = random.randrange(-1,2)
        self.move_y = random.randrange(-1,2)
        self.x += self.move_x
        self.y += self.move_y
        
        if self.x < 0: self.x = 0
        elif self.x > WIDTH: self.x = WIDTH
        
        if self.y < 0: self.y = 0
        elif self.y > HEIGHT: self.y = HEIGHT
```
>>
### 
```python
harsh = Human(name='Harsh', gender='Male')
```
>>
### 
```python

```
>>
### 
```python

```
>>
### 
```python

```
>>
### 
```python

```
>>
### 
```python

```
>>
