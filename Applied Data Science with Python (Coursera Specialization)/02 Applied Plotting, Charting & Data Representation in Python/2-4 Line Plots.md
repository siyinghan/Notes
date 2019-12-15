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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/048.png' alt='048' width='65%' />

So there are a couple of things which are new about this versus the scatter plots:

- First, we only gave `y-axes` values to our plot call, no `x-axes` values. Instead, the `plot` function was smart enough to figure out that what we wanted was to use the **index** of the series as the x value. Which is pretty handy when you want to make quick plots.
- Second we see that the plot     identifies this as two series of data and that the colors of the data from     the series are different including the data points and the lines between     the data points. This is different from the scatter plot which required us     to label the lines directly.

Like all good `Python` libraries `matplotlib` invents *a string based mini language* for commonly used formatting. For instance, we could use an **s** inside of the formatting string which would plot another point using a **square marker**. Or we could use a series of dashes and dots to identify that a line should be dashed instead of solid:

```python
# plot another series with a dashed red line
plt.figure()
plt.plot([22,44,55], '--r')
```

