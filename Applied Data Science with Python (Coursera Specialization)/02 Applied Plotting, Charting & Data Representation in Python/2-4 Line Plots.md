# 2-4 Line Plots

We've already seen line plots a couple times, but they looked a lot like scatter plots. A **line plot** is created with the `plot` function. And plots a number of different series of data points. Connecting each series in a point with a line.

Let's jump right in. We can use `numpy` to use a linear series of data points one through eight. We'll also create a number of quadratically increasing values as the second series. Remember that you can use broadcasting in numpy to do this efficiently. Here we can plot this, and this time I'll use the **mini formatting language**, task map plot lib, to draw lines between data points. We'll see the result as a two data series, the linear one at the bottom and the quadratic one at the top. Both are using dots because we use the `-o` flag:

```python
import numpy as np
linear_data = np.array([1,2,3,4,5,6,7,8])
exponential_data = linear_data**2

plt.figure()
# plot the linear data and the exponential data
plt.plot(linear_data, '-o', exponential_data, '-o')
```

