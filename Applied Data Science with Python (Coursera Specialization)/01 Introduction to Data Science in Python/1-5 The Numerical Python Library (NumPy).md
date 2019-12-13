# 1-5 The Numerical Python Library (NumPy)

- [Creating Arrays](#creating-arrays)
- [Combining Arrays](#combining-arrays)
- [Operations](#operations)

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

Now, let's look into some of the operations you can do with `numpy` arrays. Use `+`, `-`, `*`, `/` and `**` to perform element wise addition, subtraction, multiplication, division and power.

```

