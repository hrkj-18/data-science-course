#Introduction to python
###Chapter 1
    print(7 + 10)
    13
###Why we use python
* You want to do some quick calculations.
* For your new business, you want to develop a database-driven website.
* Your boss asks you to clean and analyze the results of the latest satisfaction survey.

###Operators
<table>
  <thead>
    <tr>
      <th>Operator</th>
      <th>Description</th>
      <th>Syntax</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>+</td>
      <td>Addition: adds two operands</td>
      <td>x+y</td>
    </tr>
    <tr>
      <td>-</td>
      <td>Subtraction: subtracts two operands</td>
      <td>x-y</td>
    </tr>
    <tr>
      <td>*</td>
      <td>Multiplication: multiplies two operands</td>
      <td>x*y</td>
    </tr>
    <tr>
      <td>/</td>
      <td>Division (float): divides the first operand by the second</td>
      <td>x/y</td>
    </tr>
    <tr>
      <td>//</td>
      <td>Division (floor): divides the first operand by the second</td>
      <td>x//y</td>
    </tr>
    <tr>
      <td>%</td>
      <td>Modulus: returns the remainder when first operand is divided by the second</td>
      <td>x%y</td>
    </tr>
    <tr>
      <td>******</td>
      <td>Expnentiation : raises the number to its left to the power of the number to its right</td>
      <td>x****y</td>
    </tr>
  </tbody>
</table>

###Variables & Types
    a=1.0
    print(type(a))
    <class 'float'>
* int()
* float()
* str()
* bool()

###Chapter 2
###Lists
###Indexing
    Start starts with 0
    End starts with -1
###Slicing of Lists
    A=['a','b','c','d','e','f']
    
    print(A[1:3])
    ['b','c']

    print(A[2:])
    ['c','d','e','f']

###List Manipulation
###Replace list elements
    A=['a','b','c','d','e','f']

    A[2]='g'
    print(A)
    ['a','b','g','d','e','f']

###Extend a list
    A=['a','b','c']
    B=['d','e','f']
    print(A+B)
    ['a','b','g','d','e','f']

###Delete list elements
    A=['a','b','c','d','e','f']
    del(A[1])
    print(A)
    ['a','c','d','e','f']

###Inner workings of a list
    A=['a','b','c','d','e','f']
    new_A = A[:]
    print(new_A)
    ['a','b','c','d','e','f']

###Chapter 3
###Functions
###Help function
    help(max)
    ?max

    Help on built-in function max in module builtins:

    max(...)
        max(iterable, *[, default=obj, key=func]) -> value
        max(arg1, arg2, *args, *[, key=func]) -> value

        With a single iterable argument, return its biggest item. The default keyword-only argument specifies an 
        object to return if the provided iterable is empty. 
        With two or more arguments, return the largest argument.    

###Methods
###String Methods
    room = "poolhouse"

####Upper
    room_up=room.upper()

    print(room)
    print(room_up)
    poolhouse
    POOLHOUSE

####Count
    print(room.count("o"))
    3

###List Methods        
    areas = [11.25, 18.0, 20.0, 10.75, 9.50]

####Index
    print(areas.index(20.0))
    2

####Count
    print(areas.count(14.5))
    0

####Append
    areas.append(24.5)
    areas.append(15.45)
    print(areas)
    [11.25, 18.0, 20.0, 10.75, 9.5, 24.5, 15.45]

####Reverse
    areas.reverse()
    print(areas)
    [15.45, 24.5, 9.5, 10.75, 20.0, 18.0, 11.25]

####Remove
    areas.remove(24.5)
    print(areas)
    [15.45, 24.5, 9.5, 10.75, 20.0, 18.0, 11.25]

###Chapter 4
###NumPy
    baseball = [180, 215, 210, 210, 188, 176, 209, 200]
    import numpy as np
    np_baseball = np.array(baseball)
    
    print(np_baseball)
    [180 215 210 210 188 176 209 200]
    
    print(type(np_baseball))
    <class 'numpy.ndarray'>

    x = [4 , 9 , 6, 3, 1]
    y = np.array(x)

    high = y > 5
    print(high)
    [False  True  True False False]

    print(y[high])
    [9,6]

###Addition of NumPy arrays
    A=np.array([1,2,3])
    B=np.array([2,3,4])
    A+B=np.array([3,5,7])

    Same results with - * /

###Mean
    A=np.array([1,2,3])
    print(np.mean(A))
    2

###Median
    A=np.array([1,2,3])
    print(np.mean(A))
    2

###Standard Deviation
    np.std(A)

###Correlation
    np.corrcoef(A[:,0],B[:,1])
