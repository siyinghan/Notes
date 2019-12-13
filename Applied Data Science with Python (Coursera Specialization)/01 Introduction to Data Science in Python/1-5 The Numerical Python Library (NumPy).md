# 1-5 The Numerical Python Library (NumPy)

- [Creating Arrays](#creating-arrays)
- [Combining Arrays](#combining-arrays)
- [Operations](#operations)
- [Math Functions](#math-functions)

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
<img src='http://latex.codecogs.com/gif.latex?%24%20%5Cbegin%7Bbmatrix%7Dx_1%20%5C%20x_2%20%5C%20x_3%5Cend%7Bbmatrix%7D%20%5Ccdot%20%5Cbegin%7Bbmatrix%7Dy_1%20%5C%5C%20y_2%20%5C%5C%20y_3%5Cend%7Bbmatrix%7D%20%3D%20x_1%20y_1%20&plus;%20x_2%20y_2%20&plus;%20x_3%20y_3%24' alt='dot'/>

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
