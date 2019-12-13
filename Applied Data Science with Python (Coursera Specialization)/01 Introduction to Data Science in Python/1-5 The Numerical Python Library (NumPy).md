# 1-5 The Numerical Python Library (NumPy)


## Creating Arrays

`numpy` is a package widely used in the data science community which lets us work efficiently with arrays and matrices in Python. First, let's import `numpy` as `np`. (This lets us use the shortcut np to refer to `numpy`.)
```python
import numpy as np
```

Now let's make our first array. We can start by creating a list and converting it to an array. So here's our first `numpy array`.
```python
mylist = [1, 2, 3]
x = np.array(mylist)
x
```
```array([1, 2, 3])```
