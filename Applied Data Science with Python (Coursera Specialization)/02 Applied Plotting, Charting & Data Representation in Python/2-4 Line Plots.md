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

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/049.png' alt='049' width='65%' />

Here, let's plot another series. We can use the regular `axes` functions creating labels for the axes and for the figure as a whole. And we can create a `legend` too. But note that since we didn't label the data points as we did with the scatter plot, we need to create legend entries when we add the legend itself:

```python
plt.xlabel('Some data')
plt.ylabel('Some other data')
plt.title('A title')
# add a legend with legend entries
#(because we didn't have labels when we plotted the data series)
plt.legend(['Baseline', 'Competition', 'Us'])
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/050.png' alt='050' width='65%' />

This is a good time to introduce the `fill_between` function of `matplotlib`. Now this function isn't specific to line plots, but you can see it commonly used with these plots, so I'll introduce it in this context. Let's imagine that we want to highlight the difference between the green and the blue curves. We could tell the axes to paint a color between these series using the fill between function. First we get the current axes object, then we indicate the range of x values we want to be filled. We didn't specify any x values in our call to plot, so we'll just use the same range of data points it's already using. Then we'll put in our lower bounds and our upper bounds along with the color we want painted and for fun I'll include a transparency value. And that's all there is to it. This is a great way to show, for instance, the standard deviation of results or error bars. More likely you'll have a series of x values and y values which you're looking to plot. Often with line plots this comes in the form of date time on the x axes:

```python
plt.figure()
# fill the area between the linear data and exponential data
plt.gca().fill_between(range(len(linear_data)), 
                       linear_data, exponential_data, 
                       facecolor='blue', 
                       alpha=0.25)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/051.png' alt='051' width='65%' />

Let's change our x axis to a series of eight date time instances in one day intervals. Let's first create a new image. Then the `numpy.arrange` function which you saw previously is really helpful at sampling some dates for us. We can ask for an arrangement of dates at daily intervals just by providing the start and end dates. We can now replot our linear and exponential data against this set of dates. That didn't seem to get us the effect that we were interested in:

```python
plt.figure()

observation_dates = np.arange('2017-01-01', '2017-01-09', dtype='datetime64[D]')

plt.plot(observation_dates, linear_data, '-o',  observation_dates, exponential_data, '-o')
```



The version of my Jupyter Notebook is higher than the tutorial, this part is good now.

\------

