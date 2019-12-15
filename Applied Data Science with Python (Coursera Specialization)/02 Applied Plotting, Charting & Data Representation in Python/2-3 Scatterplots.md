# 2-3 Scatterplots

In the previous lecture, I introduced the `plot` function, which generates a series of lines which get rendered against an axis object. Matplotlib actually has a number of useful plotting methods in the **scripting layer** which correspond to different kinds of plots. We are not going to go through all of them here but we'll touch on a few of the major ones. Regardless, there are a few things to keep in mind which we learned in the previous lecture:

* One, `pyplot` is going to retrieve the current figure with the function `gcf` and then get the current axis with the function `gca`. Pyplot is keeping track of the axis objects for you. But don't forget that they're there and we can get them when we want to get them.
* Two, also pyplot just mirrors the API of the axis objects. So you can call the `plot` function against the pyplot module. But this is calling the axis plot functions underneath, so be aware.
* And three, finally, remember that the function declaration from most of the functions in matplotlib end with an open set of keyword arguments. There are a lot of different properties you can control through these keyword arguments. And I'll start peppering in some of them this week to demostrate that the matplotlib documentation is really key in gaining a full understanding of the options available.

With that in mind let's move on to talk first about **scatterplots**.

A **scatterplot** is a two dimensional plot similar to the line plots I've shown. The scatter function takes an x-axis value as a first argument and y-axis value as the second. If the two arguments are the same, we get a nice diagonal alignment of points. Let's do this now. I'll bring in `numpy` as we're going to use it later and matplotlib is really based on numpy arrays. I'll create a short array for **x** and make **y** the same. Then create a new figure and scatterplot. You can see in this plot a nice diagonal line and `matplotlib` has sized our axises accordingly:

```python
import numpy as np
x = np.array([1,2,3,4,5,6,7,8])
y = x

plt.figure()
plt.scatter(x, y) # similar to plt.plot(x, y, '.'), but the underlying child objects in the axes are not Line2D
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/042.png' alt='042' width='65%' />

Now, `scatter` doesn't represent items as a series. Instead, we can pass it a list of colors which correspond to given points. Let's use some list arithmetic to create a new list just short of the number of data points we need and set all of the values to green. Then we'll add a final value of red. Then we'll plot this, and we'll set the size of the data points to 100 to make it a little easier to see. The separation of data points into lists, which describes them as components is a pretty common pattern in `matplotlib`:

```python
import numpy as np
x = np.array([1,2,3,4,5,6,7,8])
y = x

# create a list of colors for each point to have
# ['green', 'green', 'green', 'green', 'green', 'green', 'green', 'red']
colors = ['green']*(len(x)-1)
colors.append('red')

plt.figure()
# plot the point with size 100 and chosen colors
plt.scatter(x, y, s=100, c=colors)
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/043.png' alt='043' width='65%' />

You have some set of items, but they're actually described as the same slice across many different data sources. It's in one object-based language, but you might expect that each data point is represented with its own instance, which encapsulates all of its properties. For instance, it's called an x value and a y value and a color and a size. That's not the case here. This is where it's useful to have some knowledge of list comprehensions and lambdas as we talked about in the first course. Also important is the zip function and list unpacking. And because this is so common in the Python data science world, I'm going to take a brief aside and talk about that here. Recall that the zip method takes a number of iterables and creates tuples out of them, matching elements based on index. So if we have two lists of numbers, zip will take the first from each and create a tuple, then the second from each and create a tuple, and so on. Also remember that zip has lazy evaluation because it's actually a generator in Python 3 which means we need to use the list function if we want to see the results of iterating over zip. Let's demonstrate.

Here we'll create a new `zip` generator with a zip function passing in two lists of numbers. When we convert this generator to a list, we see there's a list of pairwise tuples:

```python

```

