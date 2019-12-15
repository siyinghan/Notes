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
# convert the two lists into a list of pairwise tuples
zip_generator = zip([1,2,3,4,5], [6,7,8,9,10])
print(list(zip_generator))
```

```[(1, 6), (2, 7), (3, 8), (4, 9), (5, 10)]```

```python
# The single star * unpacks a collection into positional arguments
print(*zip_generator)
```

```(1, 6) (2, 7) (3, 8) (4, 9) (5, 10)```

Storing point data as tuples is common and you should be familiar with being able to convert data to and from this form. If we want to turn the data back into two lists, one with the **x component** and one with the **y component**, we can use parameter unpacking with zip. When you pass a list or an interval more generally to a function and prepend it with an asterisk, each item is taken out of the iterable and passed as a separate argument.

So we can do that here, passing into a new `zip` function five parameters, each of length two.`zip` will then create a new two value list which is identical to our original x and y values. If we want to get even fancier, we can unpack this result into two variables directly, **x** and **y**:

```python
# use zip to convert 5 tuples with 2 elements each to 2 tuples with 5 elements each
print(list(zip((1, 6), (2, 7), (3, 8), (4, 9), (5, 10))))
```

```[(1, 2, 3, 4, 5), (6, 7, 8, 9, 10)]```

```python
zip_generator = zip([1,2,3,4,5], [6,7,8,9,10])
# let's turn the data back into 2 lists
x, y = zip(*zip_generator) # This is like calling zip((1, 6), (2, 7), (3, 8), (4, 9), (5, 10))
print(x)
```

```(1, 2, 3, 4, 5)```

```python
print(y)
```

```(6, 7, 8, 9, 10)```

So that's a brief aside on a variable tool. When it comes to manipulating and cleaning data in the wild. Now, let's get back to plotting. Let's take these two lists and plot them to a new figure using `scatter`. Instead of plotting them as one data series, we'll slice the lists and plot them as two data series. You'll note that we can color each series with a single value if we want to. We can also do things like change the color or transparency of an entire series, or individual data points as well. Finally, we have the ability to label the data series, and I'll do that now (this will come in handy later when building a legend):

```python
plt.figure()
# plot a data series 'Tall students' in red using the first two elements of x and y
plt.scatter(x[:2], y[:2], s=100, c='red', label='Tall students')
# plot a second data series 'Short students' in blue using the last three elements of x and y 
plt.scatter(x[2:], y[2:], s=100, c='blue', label='Short students')
```

<img src='https://github.com/siyinghan/Notes/raw/master/Applied%20Data%20Science%20with%20Python%20(Coursera%20Specialization)/02%20Applied%20Plotting%2C%20Charting%20%26%20Data%20Representation%20in%20Python/Image/044.png' alt='044' width='65%' />

Now before we leave the scatter plot, let's talk a bit more about the properties of axis. The axis generally have labels to them to explain what they represent or the units that they describe. Charts tend to have titles as well, so let's put this in place now. Since `pyplot` mirrors much of the axis API, we can make calls directly on `pyplot`. Let's do this now, adding in an `xlabel`, a `ylabel`, and then a `title`:

```python
# add a label to the x axis
plt.xlabel('The number of times the child kicked a ball')
# add a label to the y axis
plt.ylabel('The grade of the student')
# add a title
plt.title('Relationship between ball kicking and grades')
```



