# 1-5 The Numerical Python Library (NumPy)

- [Creating Arrays](#creating-arrays)
- [Combining Arrays](#combining-arrays)
- [Operations](#operations)
- [Math Functions](#math-functions)
- [Indexing and Slicing](#indexing-and-slicing)
- [Copying Data](#copying-data)
- [Iterating Over Arrays](#iterating-over-arrays)

<br/>

## Creating Arrays

`numpy` is a package widely used in the data science community which lets us work efficiently with arrays and matrices in Python. First, let's import `numpy` as `np`. (This lets us use the shortcut np to refer to `numpy`.)
```python
import numpy as np
```

<br/>

Now let's make our first array. We can start by creating a list and converting it to an array. So here's our first `numpy array`:
```python
mylist = [1, 2, 3]
x = np.array(mylist)
x
```
```array([1, 2, 3])```

<br/>

We can do it more succinctly by passing the list directly:
```python
y = np.array([4, 5, 6])
y
```
```array([4, 5, 6])```

<br/>

Now let's make `multidimensional arrays` by passing in a list of lists. We passed in two lists with three elements each, and we get a two by three array:
```python
m = np.array([[7, 8, 9], [10, 11, 12]])
m
```
```
array([[ 7,  8,  9],
       [10, 11, 12]])
```

<br/>

We can check the dimensions by using the `shape` attribute:
```python
m.shape
```
```(2, 3)```

<br/>

For the `arange` function, we pass in a start, a stop, and a step size, and it returns evenly spaced values within a given interval:
```python
# start at 0 count up by 2, stop before 30
n = np.arange(0, 30, 2)
n
```
```array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18, 20, 22, 24, 26, 28])```

<br/>

So suppose we wanted to convert this array of numbers to a three by five array. We can use `reshape` to do that:
```python
# reshape array to be 3x5
n = n.reshape(3, 5)
n
```
```
array([[ 0,  2,  4,  6,  8],
       [10, 12, 14, 16, 18],
       [20, 22, 24, 26, 28]])
```

<br/>

The `linspace` function is similar to `arange`, except we tell it how many numbers we want returned, and it will split up the interval accordingly
```python
# return 9 evenly spaced values from 0 to 4
o = np.linspace(0, 4, 9)
o
```
```array([ 0. ,  0.5,  1. ,  1.5,  2. ,  2.5,  3. ,  3.5,  4. ])```

<br/>

We can use `resize` to change the dimensions in place:
```python
o.resize(3, 3)
o
```
```
array([[ 0. ,  0.5,  1. ],
       [ 1.5,  2. ,  2.5],
       [ 3. ,  3.5,  4. ]])
```

<br/>

`numpy` also has several built-in functions and shortcuts for creating arrays. `ones` returns an array of ones:
```python
np.ones((3, 2))
```
```
array([[ 1.,  1.],
       [ 1.,  1.],
       [ 1.,  1.]])
```

`zeros` an array of zeros:
```python
np.zeros((2, 3))
```
```
array([[ 0.,  0.,  0.],
       [ 0.,  0.,  0.]])
```

`eye` returns an array with ones on the diagonal and zeros everywhere else:
```python
np.eye(3)
```
```
array([[ 1.,  0.,  0.],
       [ 0.,  1.,  0.],
       [ 0.,  0.,  1.]])
```

And `diag` constructs a diagonal array:
```python
np.diag(y)
```
```
array([[4, 0, 0],
       [0, 5, 0],
       [0, 0, 6]])
```

<br/>

To create an array with repeated values, we can pass in a repeated list, or we can use numpy's repeat function. (Notice the difference between the two outputs.)

Create an array using repeating list (or see `np.tile`):
```python
np.array([1, 2, 3] * 3)
```
```array([1, 2, 3, 1, 2, 3, 1, 2, 3])```

Repeat elements of an array using repeat:
```python
np.repeat([1, 2, 3], 3)
```
```array([1, 1, 1, 2, 2, 2, 3, 3, 3])```

<br/>


## Combining Arrays

We can also combine arrays to create new ones:
```python
p = np.ones([2, 3], int)
p
```
```
array([[1, 1, 1],
       [1, 1, 1]])
```

<br/>

Let's create a two by three array of ones and stack it vertically with itself, multiplied by 2. Use `vstack` to stack arrays in sequence vertically (row wise):
```python
np.vstack([p, 2*p])
```
```
array([[1, 1, 1],
       [1, 1, 1],
       [2, 2, 2],
       [2, 2, 2]])
```

And here's the same thing, but stacking horizontally. Use `hstack` to stack arrays in sequence horizontally (column wise):
```python
np.hstack([p, 2*p])
```
```
array([[1, 1, 1, 2, 2, 2],
       [1, 1, 1, 2, 2, 2]])
```

<br/>


## Operations

Now, let's look into some of the operations you can do with `numpy` arrays. Use `+`, `-`, `*`, `/` and `**` to perform element wise addition, subtraction, multiplication, division and power:
```python
print(x + y) # elementwise addition     [1 2 3] + [4 5 6] = [5  7  9]
```
```[5 7 9]```
```python
print(x - y) # elementwise subtraction  [1 2 3] - [4 5 6] = [-3 -3 -3]
```
```[-3 -3 -3]```
```python
print(x * y) # elementwise multiplication  [1 2 3] * [4 5 6] = [4  10  18]
```
```[ 4 10 18]```
```python
print(x / y) # elementwise divison         [1 2 3] / [4 5 6] = [0.25  0.4  0.5]
```
```[ 0.25  0.4   0.5 ]```
```python
print(x**2) # elementwise power  [1 2 3] ^2 =  [1 4 9]
```
```[1 4 9]```

<br/>

For those familiar with `linear algebra`, the `dot` product can be done using the dot function:
```python
x.dot(y) # dot product  1*4 + 2*5 + 3*6
```
```32```

**Dot Product:**  
<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/01%20Introduction%20to%20Data%20Science%20in%20Python/Image/004.svg' alt='dot'/>

<br/>

Let's create a new array using a previous array `y` and its squared values:
```python
z = np.array([y, y**2])
z
```
```
array([[ 4,  5,  6],
       [16, 25, 36]])
```

The `shape` of this array is two by three:
```python
z.shape
```
```(2, 3)```

We can also take the transpose of an array using the `T` method, which swaps the rows and columns. The shape of the transposed array is three by two:
```python
z.T
```
```
array([[ 4, 16],
       [ 5, 25],
       [ 6, 36]])
```

The number of rows has swapped with the number of columns:
```python
z.T.shape
```
```(3, 2)```

Using `.dtype`, we can see what type of data the array has:
```python
z.dtype
```
```dtype('int64')```

And with `.astype`, cast an array to a different type:
```python
z = z.astype('f')
z.dtype
```
```dtype('float32')```

<br/>


## Math Functions

`numpy` has many built in math functions that can be performed on arrays.:
```python
a = np.array([-4, -2, 1, 3, 5])
```
```pythob
a.sum()
```
```3```
```python
a.max()
```
```5```
```python
a.min()
```
```-4```
```python
a.mean()
```
```0.59999999999999998```
```python
a.std()
```
```3.2619012860600183```

<br/>

`argmax` and `argmin` return the index of the maximum and minimum values in the array:
```python
a.argmax()
```
```4```
```python
a.argmin()
```
```0```

<br/>


## Indexing and Slicing

Let's create an array with the squares of 0 through 12:
```python
s = np.arange(13)**2
s
```
```array([  0,   1,   4,   9,  16,  25,  36,  49,  64,  81, 100, 121, 144])```

Use bracket notation to get the value at a specific index. Remember that indexing starts at 0:
```python
s[0], s[4], s[-1]
```
```(0, 16, 144)```

Use `:` to indicate a range. `array[start:stop]`

Leaving `start` or `stop` empty will default to the beginning/end of the array:
```python
s[1:5]
```
```array([ 1,  4,  9, 16])```

Use negatives to count from the back:
```python
s[-4:]
```
```array([ 81, 100, 121, 144])```

A second `:` can be used to indicate step-size. `array[start:stop:stepsize]`

Here we are starting 5th element from the end, and counting backwards by 2 until the beginning of the array is reached:
```python
s[-5::-2]
```
```array([64, 36, 16,  4,  0])```

<br/>

Let's look at a multidimensional array:
```python
r = np.arange(36)
r.resize((6, 6))
r
```
```
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23],
       [24, 25, 26, 27, 28, 29],
       [30, 31, 32, 33, 34, 35]])
```

Use bracket notation to slice: `array[row, column]`:
```python
r[2, 2]
```
```14```

And use `:` to select a range of rows or columns:
```python
r[3, 3:6]
```
```array([21, 22, 23])```

Here we are selecting all the rows up to (and not including) row 2, and all the columns up to (and not including) the last column:
```python
r[:2, :-1]
```
```
array([[ 0,  1,  2,  3,  4],
       [ 6,  7,  8,  9, 10]])
```

This is a slice of the last row, and only every other element:
```python
r[-1, ::2]
```
```array([30, 32, 34])```

We can also perform conditional indexing. Here we are selecting values from the array that are greater than 30. (Also see `np.where`):
```python
r[r > 30]
```
```array([31, 32, 33, 34, 35])```

Here we are assigning all values in the array that are greater than 30 to the value of 30:
```python
r[r > 30] = 30
r
```
```
array([[ 0,  1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10, 11],
       [12, 13, 14, 15, 16, 17],
       [18, 19, 20, 21, 22, 23],
       [24, 25, 26, 27, 28, 29],
       [30, 30, 30, 30, 30, 30]])
```

<br/>


## Copying Data

Be careful with copying and modifying arrays in NumPy!

`r2` is a slice of `r`:
```python
r2 = r[:3,:3]
r2
```
```
array([[ 0,  1,  2],
       [ 6,  7,  8],
       [12, 13, 14]])
```

Set this slice's values to zero (`[:]` selects the entire array):
```python
r2[:] = 0
r2
```
```
array([[0, 0, 0],
       [0, 0, 0],
       [0, 0, 0]])
```

`r` has also been changed!
```python
r
```
```
rray([[ 0,  0,  0,  3,  4,  5],
       [ 0,  0,  0,  9, 10, 11],
       [ 0,  0,  0, 15, 16, 17],
       [18, 19, 20, 21, 22, 23],
       [24, 25, 26, 27, 28, 29],
       [30, 31, 32, 33, 34, 35]])
```

To avoid this, use `r.copy` to create a copy that will not affect the original array:
```python
r_copy = r.copy()
r_copy
```
```
array([[ 0,  0,  0,  3,  4,  5],
       [ 0,  0,  0,  9, 10, 11],
       [ 0,  0,  0, 15, 16, 17],
       [18, 19, 20, 21, 22, 23],
       [24, 25, 26, 27, 28, 29],
       [30, 30, 30, 30, 30, 30]])
```

Now when `r_copy` is modified, `r` will not be changed:
```python
r_copy[:] = 10
print(r_copy, '\n')
print(r)
```
```
[[10 10 10 10 10 10]
 [10 10 10 10 10 10]
 [10 10 10 10 10 10]
 [10 10 10 10 10 10]
 [10 10 10 10 10 10]
 [10 10 10 10 10 10]] 

[[ 0  0  0  3  4  5]
 [ 0  0  0  9 10 11]
 [ 0  0  0 15 16 17]
 [18 19 20 21 22 23]
 [24 25 26 27 28 29]
 [30 30 30 30 30 30]]
```

<br/>


## Iterating Over Arrays

Let's create a new 4 by 3 array of random numbers 0-9：
```python
test = np.random.randint(0, 10, (4,3))
test
```
```
array([[1, 7, 8],
       [2, 8, 7],
       [4, 3, 9],
       [7, 8, 9]])
```

Iterate by row:
```python
for row in test:
    print(row)
```
```
[1 7 8]
[2 8 7]
[4 3 9]
[7 8 9]
```

Iterate by index:
```python
for i in range(len(test)):
    print(test[i])
```
```
[1 7 8]
[2 8 7]
[4 3 9]
[7 8 9]
```

Iterate by row and index:
```python
for i, row in enumerate(test):
    print('row', i, 'is', row)
```
```
row 0 is [1 7 8]
row 1 is [2 8 7]
row 2 is [4 3 9]
row 3 is [7 8 9]
```

Use `zip` to iterate over multiple iterables:
```python
test2 = test**2

for i, j in zip(test, test2):
    print(i,'+',j,'=',i+j)
```
```
[1 7 8] + [ 1 49 64] = [ 2 56 72]
[2 8 7] + [ 4 64 49] = [ 6 72 56]
[4 3 9] + [16  9 81] = [20 12 90]
[7 8 9] + [49 64 81] = [56 72 90]
```
